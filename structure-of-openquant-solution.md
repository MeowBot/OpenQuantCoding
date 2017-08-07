# OpenQuant 策略代码的结构

---

## OpenQuant策略示例中的代码结构分析

![](/icons/icon_labtubeBlue.ico)打开OpenQuant中的SMACrossover策略，这是一个经典的SMA交叉策略，打开后可以直接运行看到回测结果。这里我们着重看一下这个例子的代码结构和调用关系。

![](/assets/SMACrossoverSolutionExplorer.png)

这个解决方案中，有四个工程

**Backtest**        ：回测，定义回测时的场景，引入的数据，回测的起始及结束日期，构造K线生成要素  
**MyStrategy**    ：策略逻辑主体，定义均线，绘制K线及均线的主要图表，处理交易逻辑，处理成交事件，处理持仓等等  
**Optimization** ：策略优化参数定义，及策略优化的起始及结束日期  
**Realtime**        ：实盘交易的场景，引入的合约，行情源及交易通道定义

这样的结构如图所示：

![](/assets/SMACrossoverCodeMap.png)图：OpenQuant策略示例SMACrossover的代码结构

## OpenQuant策略的驱动机制

OpenQuant的策略运行机制是构造出扑捉市场数据的处理逻辑后，静静地等待各种事件发生，来驱动整体逻辑的运行。例如：当订阅的合约有最新报价变动时，或当行情的变动幅度超过定义时，当下单部分成交时，或发出的撤单指令成功时等等，当然有的时候也需要自己依据定时间隔去进行驱动。由于这种处理机制，可以让量化交易者精细地定义逻辑并清晰地执行。

下面就是一个成交事件处理的代码，你可以在SMACrossover策略解决方案中的MyStrategy工程的MyStrategy.cs代码中找到：

```
	protected override void OnFill(Fill fill)
		{
			// Add fill to group.
			Log(fill, "Fills");
		}


```









