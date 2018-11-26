# 2. 需要涉及的工作

## 2.1 管理未来所有的代码...

在正式进行量化交易工作前，应该先着手规划如何管理你未来所有的策略代码。构建起一个明确的工作流程及管理体系，能让你的策略设计文档、策略程序代码及配置信息等诸多文件井井有条，这将极大的帮助你形成轻松高效并且稳定的开发管理体系。毕竟，稳定的过程导致稳定的质量。

![](/.gitbook/assets/icon_paw.png)建立程序化交易开发管理体系，用SVN或者Git这样的版本控制系统管理你所有的代码及文档。相关内容请参考相关资料。

## 2.2 建立一个适用的IT构架

量化交易需要一个即稳固又便于扩展的IT构建，因为很多量化交易所需要的功能模块、数据来源、处理方式、运算能力及未来的机器学习和人工智能，这些都不是一个产品能够全部完成的，就量化交易中的数据源一项就有可能涉及Wind，Bloomberg数据终端，也有可能涉及各种各样的商业数据库。而模型建立很多交易员和研究员又有着不同的工具使用偏好，比如Matlab 或者Python。这就需要通过IT构架从全局的高度来进行设计，采用分层、模块化的构架来解决我们面临的复杂问题，而OpenQuant可以很好地在嵌入各种IT构架中。这也是专业金融交易机构的解决方案。为此，我们未来的量化交易构架未来很有可能会涉及多台服务器及较为复杂的运维工作。



我们这里给出一个能担负数据管理、策略研发、策略回测及优化及策略执行的IT构架示例，总体结构如下图所示：
