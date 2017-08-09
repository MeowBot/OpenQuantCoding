# 编写一个OpenQuant的HelloWorld!

---

# 用OpenQuant创建一个基础代码框架

![](/icons/icon_labtubeBlue.ico)打开OpenQuant中的**File**菜单，**New**一个新的**solution**, 这里有一些解决方案类别选项，这个例子中，我们选择第一种“SmartQuant Instrument Strategy Solution”， 命名为_HelloWorld，_在OpenQuant的Solution Explorer窗口中，我们可以发现当前有两个工程，**Backtest**和**MyStratey**.这就是最基础的代码框架了，一个回测场景定义工程，一个策略主体工程。

# 增加一个场景工程-Realtime

![](/icons/icon_labtubeBlue.ico)现在，我们按照设计，再增加一个实盘交易场景工程Realtime。在OpenQuant的Solution Explorer中找到刚刚建立的解决方案HelloWorld，在HelloWorld上鼠标右键，**Add**一个**New Project... ** 我们增加一个场景工程， 选择SmartQuant Scenario Project， 命名为 _**Realtime **_

# 开始编写代码

现在我们按照设计，这个解决方案（Solution）中已经有了三个工程：一个回测场景，一个实盘场景，一个策略主体; 让我们来加入代码:

![](/icons/icon_labtubeBlue.ico)在回测场景工程（Backtest）中，增加回测场景的定义，包括测试的合约，我们引入螺纹钢期货rb1709合约，我们假设你已经在OpenQuant中引入了rb1709合约，同时使用历史数据插件导入了2017年1月1日至2017年3月1日的Tick级别的历史数据。

在Backtest工程中的MyScenario.cs文件中，编写代码如下





```

```







Coming soon... ...

