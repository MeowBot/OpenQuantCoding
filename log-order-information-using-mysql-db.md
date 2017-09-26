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

* ### 第二步-在策略工程中引入MySQL的DLL库

在MyStrategy工程中，先引入Mysql的库：MySql.Data.dll ，在安装插件后，你可以在OpenQuant的安装目录中即可以找到这个动态链接库。或者在MySQL的安装目录中也可以找到。

* ### 第三步-编写日志存储功能OmniLog.cs

在 





通过Mysql的Workbench工具可以监控数据库的状态，Dashboard工具如下图所示：

![](/assets/MysqlDashboard01.png)我们会发现这样写日志的效率还是有些慢，但对于没有做高频交易（HFT）的情况，这些工具是适用的。

