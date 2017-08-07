# OpenQuant 策略代码的结构

---

![](/icons/icon_labtubeBlue.ico)打开OpenQuant中的SMACrossover策略，这是一个经典的SMA交叉策略，打开后可以直接运行看到回测结果。这里我们着重看一下这个例子的代码结构和调用关系。

![](/assets/SMACrossoverSolutionExplorer.png)

这个解决方案中，有四个工程 

Backtest        ：回测，定义回测时的场景，引入的数据，回测的起始及结束日期，构造K线生成要素  
MyStrategy    ：策略逻辑主体，定义均线，绘制K线及均线的主要图表，处理交易逻辑，处理成交事件，处理持仓等等  
Optimization ：策略优化参数定义，及策略优化的起始及结束日期  
Realtime        ：实盘交易的场景，引入的合约，行情源及交易通道定义

这样的结构如图所示：





