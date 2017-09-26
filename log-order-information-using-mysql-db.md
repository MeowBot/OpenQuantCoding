# 7.4  将交易记录存入MySQL

---

对于一个完善的IT系统，无论是交易系统，还是业务管理系统，我们都会按照层次结构来规划。作为一个交易系统，我们需要将交易日志存入数据，以提供业务监控、问题排查、数据统计分析。

现在我们就将FlashOrder下单的记录全部存入Mysql数据库。大致过程分为五步，第一步建立数据库及日志表；第二步在FlashOrder中引入相关的MySQL动态链接库；第三步编写一个日志存储功能的方法，让主策略代码可以调用日志功能。这个文件我们命名为OmniLog.cs，这个文件我们和主策略代码放在一个工程代码中； 第四步，我们在主策略的下单代码后面，插入调用日志存储的方法；第五步，使用MySQL工具及性能工具进行日志存储的查看和监控。

* ### 第一步-安装MySQL数据库及建立交易日志表

第一步，我们安装好MySQL数据库，并建立交易报单日志表LogOrder表，建表SQL如下：

    CREATE TABLE `logorder` (
        `id` INT(11) NOT NULL AUTO_INCREMENT,
        `logdatetime` DATETIME(6) NULL DEFAULT NULL COMMENT 'log记录时间',
        `StrategyName` VARCHAR(20) NULL DEFAULT NULL COMMENT '策略名字' COLLATE 'utf8mb4_unicode_ci',
        `OrdId` INT(11) NULL DEFAULT NULL,
        `OrdDateTime` DATETIME(6) NULL DEFAULT NULL,
        `Symbol` VARCHAR(10) NULL DEFAULT NULL COLLATE 'latin1_swedish_ci',
        `TradeDay` DATE NULL DEFAULT NULL,
        `Side` VARCHAR(10) NULL DEFAULT NULL COLLATE 'latin1_swedish_ci',
        `Type` VARCHAR(10) NULL DEFAULT NULL COLLATE 'latin1_swedish_ci',
        `Qty` INT(11) NULL DEFAULT NULL,
        `Price` FLOAT NULL DEFAULT NULL,
        `Status` VARCHAR(16) NULL DEFAULT NULL COLLATE 'latin1_swedish_ci',
        `note` VARCHAR(50) NULL DEFAULT NULL COMMENT '备注' COLLATE 'utf8mb4_unicode_ci',
        PRIMARY KEY (`id`)
    )
    COMMENT='定单日志表，存储所有交易记录'
    COLLATE='utf8mb4_unicode_ci'
    ENGINE=InnoDB
    AUTO_INCREMENT=72969
    ;

在MySQL中记录定单日志如下：

![](/assets/Table_logorder.png)

* ### 第二步-在策略工程中引入MySQL的DLL库及建立MySQL访问代码

在FlashOrder解决方案的在MyStrategy工程中，先引入Mysql的库：MySql.Data.dll 。这个动态链接库文件你可以在OpenQuant的安装目录中即可以找到，或者在MySQL的安装目录中也可以找到。

再在MyStrategy工程中增加MySQL访问功能的公共方法代码，文件名MysqlMan.cs ，该文件代码如下：

```
/*
 *      Purpose:    MySQL DB Access  
 *          
 *      Created:    2017/09/12 
 * 
 * 
 */

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

using MySql.Data.MySqlClient;


namespace OpenQuant
{
	class MysqlMan
	{


		/// <summary>
		/// 建立mysql数据库链接
		/// </summary>
		/// <returns></returns>
		public static MySqlConnection getMySqlCon()
		{
			String mysqlStrQBMD = "";
			//Mysql Server at Lab
			mysqlStrQBMD = "Database=MySQL01;Data Source=127.0.0.1;User Id=root;Password=yourPassword;pooling=false;CharSet=utf8;port=3306;Allow Zero Datetime=True";
			//MySQL Server at Home
			//mysqlStrQBMD = "Database=MySQL02;Data Source=127.0.0.1;User Id=root;Password=yourPassword;pooling=false;CharSet=utf8;port=3306;Allow Zero Datetime=True";
            


			MySqlConnection mysql = new MySqlConnection(mysqlStrQBMD);
			return mysql;
		}

		/// <summary>
		/// 建立执行命令语句对象
		/// </summary>
		/// <param name="sql"></param>
		/// <param name="mysql"></param>
		/// <returns></returns>
		public static MySqlCommand getSqlCommand(String sql, MySqlConnection mysql)
		{
			MySqlCommand mySqlCommand = new MySqlCommand(sql, mysql);
			return mySqlCommand;
		}

		/// <summary>
		/// 添加数据
		/// </summary>
		/// <param name="mySqlCommand"></param>
		public static void getInsert(MySqlCommand mySqlCommand)
		{
			try
			{
				mySqlCommand.ExecuteNonQuery();
			}
			catch (Exception ex)
			{
				String message = ex.Message;
				Console.WriteLine("插入数据失败了！" + message);

			}

		}

		/// <summary>
		/// 删除数据
		/// </summary>
		/// <param name="mySqlCommand"></param>
		public static void getDel(MySqlCommand mySqlCommand)
		{
			try
			{
				mySqlCommand.ExecuteNonQuery();
			}
			catch (Exception ex)
			{
				String message = ex.Message;
				Console.WriteLine("删除数据失败了！" + message);
			}
		}

		/// <summary>
		/// 修改数据
		/// </summary>
		/// <param name="mySqlCommand"></param>
		public static void getUpdate(MySqlCommand mySqlCommand)
		{
			try
			{
				mySqlCommand.ExecuteNonQuery();
			}
			catch (Exception ex)
			{

				String message = ex.Message;
				Console.WriteLine("修改数据失败了！" + message);
			}
		}



		public static int ExecuteNonQuery(string sql) 
		{
			MySqlConnection mysql = null;
			try
			{
				mysql = getMySqlCon();
				mysql.Open();
				MySqlCommand mySqlCommand = new MySqlCommand(sql, mysql);
				int result = mySqlCommand.ExecuteNonQuery();
				mysql.Close();
				return result;
			}
			catch (Exception ex)
			{
				if (mysql != null && mysql.State != System.Data.ConnectionState.Closed)
					mysql.Close();
				String message = ex.Message;
				Console.WriteLine("ExecuteNonQuery失败了！" + message);
				return 0;
			}
		}

		public static object ExecuteScalar(string sql) 
		{
			MySqlConnection mysql=null;
			try
			{
				mysql = getMySqlCon();
				MySqlCommand mySqlCommand = new MySqlCommand(sql, mysql);
				mysql.Open();
				object result = mySqlCommand.ExecuteScalar();
				mysql.Close();
				return result;

			}
			catch (Exception ex)
			{
				if(mysql!=null && mysql.State != System.Data.ConnectionState.Closed)
					mysql.Close();
				String message = ex.Message;
				Console.WriteLine("ExecuteNonQuery失败了！" + message);
				return null;
			}
		}
	}
}

```

* ### 第三步-编写日志存储功能OmniLog.cs

在FlashOrder解决方案的MyStrategy工程中，



通过Mysql的Workbench工具可以监控数据库的状态，Dashboard工具如下图所示：

![](/assets/MysqlDashboard01.png)我们会发现这样写日志的效率还是有些慢，但对于没有做高频交易（HFT）的情况，这些工具是适用的。

