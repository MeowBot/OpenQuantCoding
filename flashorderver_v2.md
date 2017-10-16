# 7.5 同时处理多个合约 FlashOrder v2

---

在策略中通道要处理多个合约，根据实际情况我们有简单的方法和优化的方法。

## 简单的方法

简单的方法就是在场景文件Scenario.cs中，直接定义新的合约变量，复制相关代码即可， 主策略代码不用改变，策略运行时，你会发现一个合约就是策略的一个实例，它们都在并行的运行。

```
            //定义合约
            Instrument instrument1 = InstrumentManager.Instruments["au1712"];
            Instrument instrument2 = InstrumentManager.Instruments["rb1801"];
            Instrument instrument3 = InstrumentManager.Instruments["c1801"];
            ... ... 


        //引入合约到主策略工程
            strategy.AddInstrument(instrument1);
            strategy.AddInstrument(instrument2);
            strategy.AddInstrument(instrument3);
            ... ... 

        //定义K线类型：时间型K线，barSize秒生成一个Bar
            BarFactory.Clear();
            BarFactory.Add(instrument1, BarType.Time, barSize);
            BarFactory.Add(instrument2, BarType.Time, barSize);
            BarFactory.Add(instrument3, BarType.Time, barSize);
            ... ...
```

优雅的方法

在场景文件Scenario.cs中，可以定义一个变量数组， 采用循环代码进行加载，但这个方法中， 会出现你想加入的合约信息并没有在OpenQuant引入过，代码会报出提示， 如果有这样的情况，你应该先在OpenQuant中手动引入相关的合约信息（过程详见1.5 导入合约信息）

