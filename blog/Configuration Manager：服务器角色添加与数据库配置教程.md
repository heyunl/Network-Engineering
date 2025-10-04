# Configuration Manager：服务器角色添加与数据库配置教程
本系列教程聚焦**Configuration Manager** 的完整部署流程，第一篇已完成**SQL Server 2019**的安装与配置（[点击查看第一篇](https://www.yinyuee.com/tutorial/windows/sql-server-2019-installation-configuration-manager)）。本文作为系列第二篇，我们将介绍**通过服务器管理器添加Configuration Manager所需角色**及**数据库连接配置**的关键步骤。

一、前置条件（需提前完成）
-------------

在开始本文步骤前，请确保已完成以下准备（若未完成，请先参考对应教程）：

1.  完成**SQL Server 2019**及**SSMS**安装（[详见第一篇教程](https://www.yinyuee.com/tutorial/windows/sql-server-2019-installation-configuration-manager)）；
2.  安装**微软常用运行库**（[下载链接](https://www.yinyuee.com/software/tools/windows-runtime-library)）；
3.  启用 **.NET Framework 3.5**（通过服务器管理器→“添加角色和功能”→勾选“.NET Framework 3.5 功能”）；
4.  安装**Windows ADK**及**ADK附加组件**（[下载链接](https://learn.microsoft.com/zh-cn/windows-hardware/get-started/adk-install)，选择与系统版本匹配的版本）。

二、步骤1：安装SQL Server ODBC驱动
-------------------------

Configuration Manager需要通过**ODBC驱动**连接SQL Server数据库，必须安装与SQL Server 2019兼容的**64位ODBC驱动**。

### 操作步骤：

1.  访问微软官方下载页（[ODBC Driver for SQL Server](https://learn.microsoft.com/zh-cn/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-ver16)）；
2.  选择**64位版本**（如图），下载安装程序；
3.  运行安装程序，勾选“我接受许可条款”，点击“安装”；
4.  等待安装完成（约1-2分钟），点击“完成”。

 ![](https://pkg.changjiu365.cn/assets/2405782b.webp) 

微软官方下载页图示

三、步骤2：通过服务器管理器添加Configuration Manager所需角色
-----------------------------------------

Configuration Manager的安装需要依赖服务器的一些**核心角色**，需通过**服务器管理器**添加。

### 操作步骤：

1.  打开**服务器管理器**（通过开始菜单搜索“服务器管理器”）；
    
2.  点击顶部“添加角色和功能”（进入角色添加向导）；
    
3.  在“选择安装类型”界面，选择“基于角色或基于功能的安装”，点击“下一步”；
    
4.  在“选择服务器角色”界面，**勾选以下Configuration Manager 必需角色**（根据图片提示调整，示例如下）：
    
     ![](https://pkg.changjiu365.cn/assets/bbad4516.webp) 
    
    服务器管理器→添加角色和功能：勾选Configuration Manager所需角色
    
     ![](https://pkg.changjiu365.cn/assets/7615b203.webp) 
    
    勾选 BITS
    
5.  点击“下一步”，按照向导提示完成角色安装（无需修改默认设置）；
    
6.  安装完成后，点击“关闭”退出向导。
    

四、步骤3：WSUS 数据库配置
----------------

### 操作步骤：

1.  在“数据库实例”窗口，**数据库服务器** 输入`localhost`（默认SQL实例，若为命名实例需填写“计算机名\\实例名”，如`localhost\SQL2019`）；
2.  若成功连接，说明数据库连接正常（Configuration Manager后续安装也将使用此连接信息）。

 ![](https://pkg.changjiu365.cn/assets/0f40ed05.webp) 

SSMS连接验证：服务器名称输入“localhost”

五、步骤4：SQL Server后续配置（满足Configuration Manager先决条件）
-------------------------------------------------

Configuration Manager的**先决条件检查**对SQL Server有严格要求，需完成以下两项配置：

### 1\. 启用SQL Server TCP/IP协议

Configuration Manager需通过**TCP/IP协议**连接SQL Server，必须启用该协议：

1.  打开**SQL Server Configuration Manager**；
2.  导航至“SQL Server 网络配置”→“MSSQLSERVER的协议”（默认实例），**双击“TCP/IP”** ，在“常规”选项卡中选择“启用”；  
    ​ ![](https://pkg.changjiu365.cn/assets/2d70eb7c.webp) 
    
    SQL Server网络配置：双击“TCP/IP”并启用（Configuration Manager依赖TCP/IP连接数据库）
    
3.  重启SQL Server服务（右键→“重启”）。

### 2\. 修改SQL Server服务登录身份为“Local System”

Configuration Manager要求SQL Server服务使用**本地系统账户**（Local System）运行，否则先决条件检查会失败：

1.  在“SQL Server 服务”界面，右键点击“SQL Server (MSSQLSERVER)”，选择“属性”；
2.  切换至“登录”选项卡，**登录身份**选择“Local System”，点击“应用”→“确定”；  
    ​ ![](https://pkg.changjiu365.cn/assets/25e18ac0.webp) 
    
    SQL Server服务属性：登录身份选择“Local System”（满足Configuration Manager先决条件）
    
3.  重启SQL Server服务。

六、关键注意事项
--------

1.  **角色选择**：必须勾选Configuration Manager所需的服务器角色，否则后续先决条件检查会无法通过；
2.  **SQL实例名**：若SQL Server为命名实例（如`SQL2019`），数据库连接时需填写“服务器名\\实例名”（如`localhost\SQL2019`）；
3.  **TCP/IP协议**：必须启用SQL Server的TCP/IP协议，否则Configuration Manager无法通过网络连接数据库；
4.  **登录身份**：SQL Server服务必须使用“Local System”账户，否则Configuration Manager先决条件检查会失败。

七、后续步骤
------

本文完成了**服务器角色添加**和**数据库配置**的关键步骤，满足了Configuration Manager **先决条件检查**的核心要求。下一教程将继续介绍**Configuration Manager正式安装流程**，敬请关注。