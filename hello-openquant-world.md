# 开始一个OpenQuant的HelloWorld！

---

OpenQuant的开发体系是基于标准的微软C\#编程语言及.NET开发框架。下面的文档中，默认读者已经可以使用C\#编程语言及使用过Visual Studio开发工具。

## 创建第一个解决方案（C\# solution）

打开OpenQuant中的**File**菜单，**New**一个新的**solution**, 这里有一些解决方案类别选项，这个例子中，我们选择第一种“SmartQuant Instrument Strategy Solution”， 命名为_myFirstStrategy_， 保持目录应该保存在你的SVN代码版本管理体系中, 生成的解决方案（Solution）结构如下：

![](/assets/myFirstStrategyTreeDos.png)      ![](/assets/myFirstStrategyFilesTreeOQ.png)

图：一个默认解决方案包含的文件结构

在Instrument Strategy Solution类型默认代码中，主要有4个核心文件：

Backtest目录中的

-**Program.cs** --------------------------

-**MyScenario.cs** ---------------------

-**MyScenario.Designer.cs** -------

MyStrategy目录中的

-**MyStrategy.cs** -----------------------    



## OpenQuant的解决方案中代码的运行关系

这是一个标准的微软C\#解决方案，在这个_myFirstStrategy_解决方案（Solution）中有两个项目（Project）：Backtest，MyStrategy，Backtest项目是默认的启动项目。代码关系如下图的所示：

![](/assets/myFirstStrategyCodeMap.png)为了掌握OpenQuant解决方案代码运行中的调用关系，我们在该项目文件中增加输出信息，使得程序运行时，可以呈现代码运行顺序和调用关系。



