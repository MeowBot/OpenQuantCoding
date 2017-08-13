# 计算机运行环境的选择与准备

---

## 基础操作系统的选择{#runningos}

目前的OpenQuant需要微软Windows运行环境，支持微软最新版本的OpenQuant支持Windows7，Windows8，Windows10及Windows Server 2008，Windows Server 2012等主流的Windows 64位操作系统。

安装OpenQuant软件时，OpenQuant安装程序会自动检测是否有合适的.NET Framework基础软件，如果需要安装程序会自动进行升级安装。

![](/icons/icon_paw.png) 建议采用Windows Server 2012以上的面向服务器的操作系统软件。

## 下载OpenQuant软件及插件 {#downloadoqandplugins}

---

* ### **OpenQuant最新版本下载地址：**

[http://www.smartquant.com](http://www.smartquant.com) 英文官方网站

[http://www.smartquant.cn](http://www.smartquant.cn)   中文服务网站

* ### **OpenQuant国内市场插件下载地址：**

[http://www.smartquant.cn](http://www.smartquant.cn)

[http://www.quantbox.cn/download](http://www.quantbox.cn/download)

## 安装OpenQuant软件及国内市场插件 {#installoqandplugins}

---

* ### **OpenQuant安装及国内市场插件安装过程**

![](/icons/icon_bookbig.png)详见[http://www.smartquant.cn/book/installing.html](http://www.smartquant.cn/book/installing.html)



## 配置插件让OpenQuant接入市场 {#configplugins}

---

##### ![](/icons/icon_labtubeBlue.ico)**简要OpenQuant安装过程及配置插件记录**

* [ ] 安装OpenQuant最新版本;

* [ ] 安装国内市场插件;

* [ ] 配置国内市场插件:

* 交易用户名及密码信息\(UserList\)

* CTP服务器地址信息\(ServerList\)

* 交易通道组合信息\(ApiList\)

![](/assets/ApiManagerForm.png)                         图： 配置国内市场插件 -- 天风期货CTP

配置完成后，连接插件应该能看见小小的绿色通道灯亮起。

![](/assets/OQProvidersGreenLight.png)



![](/icons/icon_paw.png)现在，我们已经下载并安装了OpenQuant最新版本及国内市场插件。插件正确配置后可以正常连接至交易通道，可以导入当前期货合约代码，在市场开盘时段，打开OpenQuant中的QuoteMonitor界面，从Instruments窗口拖拽当前合约到QuoteMonitor界面中，可以看到该合约的当前市场报价。

