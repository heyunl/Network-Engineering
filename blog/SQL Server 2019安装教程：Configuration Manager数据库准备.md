# SQL Server 2019安装教程：Configuration Manager数据库准备
本系列教程将聚焦 Configuration Manager 的安装与配置，而 SQL Server 作为其核心依赖组件，需优先部署。由于 Configuration Manager 对 SQL Server 2022 需开启兼容模式，为简化流程，我们选择直接安装 **SQL Server 2019**。本文将详细介绍 SQL Server 2019 Developer 版及管理工具（SSMS）的安装步骤，确保满足 Configuration Manager 的运行要求。

> **注意**：SQL Server 2019 Developer 版仅授权用于**非生产环境**（开发/测试），生产环境需使用 Enterprise 或 Standard 版。

准备工作
----

### 1\. 系统要求

*   **操作系统**：Windows Server 2016/2019/2022 或 Windows 10/11（64位）
*   **硬件**：至少 4GB 内存（推荐 8GB+）、10GB 可用磁盘空间
*   **权限**：管理员权限（用于安装服务及配置系统）

### 2\. 下载安装程序

*   **SQL Server 2019**：通过微软官网获取评估版安装程序（[下载链接](https://www.microsoft.com/zh-cn/evalcenter/download-sql-server-2019)）

一、SQL Server 2019 安装步骤
----------------------

### 步骤 1：启动安装程序并选择“自定义安装”

1.  运行下载的 SQL Server 2019 安装程序，首次弹窗选择 **“自定义”** 安装模式（而非“基本”），点击“安装”开始下载安装介质（需等待几分钟，取决于网络速度）。
    
    > **原因**：Configuration Manager 对数据库排序规则有严格要求，“基本安装”无法自定义排序规则，因此必须选择“自定义”。
    

 ![](https://pkg.changjiu365.cn/assets/515367b0.webp) 

SQL Server 2019安装程序初始界面：选择“自定义”安装模式以启动安装介质下载

### 步骤 2：进入安装中心并选择“全新安装”

下载完成后，安装中心自动弹出，点击左侧 **“安装”** 选项卡，选择 **“全新 SQL Server 独立安装或向现有安装添加功能”** 。

 ![](https://pkg.changjiu365.cn/assets/5da136ae.webp) 

SQL Server 2019安装中心“安装”选项卡：选择“全新SQL Server独立安装或向现有安装添加功能”以启动新实例部署

### 步骤 3：选择版本并接受许可条款

1.  在“产品密钥”界面，选择 **“Developer 版”** （免费，非生产环境使用），点击“下一步”。
2.  勾选“我接受许可条款”，点击“下一步”。

 ![](https://pkg.changjiu365.cn/assets/508cfaf6.webp) 

SQL Server 2019产品密钥配置界面：选择“Developer版”（非生产环境适用，免费授权）

### 步骤 4：安装规则检查

安装程序会自动进行“安装规则”检查（如操作系统兼容性、网络服务状态等）。

 ![](https://pkg.changjiu365.cn/assets/e06b3e71.webp) 

SQL Server 2019安装前规则检查界面：系统自动检测前置条件（如操作系统版本、服务状态等）

若提示“防火墙警告”（如未对外提供数据库服务），可直接点击“下一步”忽略（后续如需远程访问，需手动配置防火墙允许 SQL Server 端口）。

 ![](https://pkg.changjiu365.cn/assets/c62d8a5c.webp) 

SQL Server 2019安装规则检查结果：防火墙警告提示（非远程访问场景可直接忽略）

### 步骤 5：选择要安装的功能

在“功能选择”界面，**仅勾选“数据库引擎服务”** （Configuration Manager 核心依赖组件），其他功能（如 SQL Server复制、全文和语义提取搜索等）按需安装，点击“下一步”。

 ![](https://pkg.changjiu365.cn/assets/0e98d8ff.webp) 

SQL Server 2019功能选择界面：仅勾选“数据库引擎服务”（Configuration Manager运行必需组件）

### 步骤 6：配置实例

“实例配置”界面选择 **“默认实例”** （推荐，实例名称默认为 `MSSQLSERVER`，便于后续 Configuration Manager 自动识别），点击“下一步”。

> **注意**：若需安装命名实例，需记录实例名称，后续配置 Configuration Manager 时需手动指定。

 ![](https://pkg.changjiu365.cn/assets/63e82778.webp) 

SQL Server 2019实例配置界面：选择“默认实例”（实例名称为MSSQLSERVER，简化后续系统识别流程）

### 步骤 7：配置排序规则

“数据库引擎配置”界面，**必须将排序规则设置为** **​`SQL_Latin1_General_CP1_CI_AS`​**（Configuration Manager 强制要求，不要修改为其他排序规则），点击“下一步”。

 ![](https://pkg.changjiu365.cn/assets/c2b75ed9.webp) 

SQL Server 2019数据库引擎配置界面：排序规则设置选项卡入口

​

 ![](https://pkg.changjiu365.cn/assets/87a70a01.webp) 

SQL Server 2019排序规则配置：选择“SQL\_Latin1\_General\_CP1\_CI\_AS”（Configuration Manager强制兼容要求）

### 步骤 8：添加管理员账户并配置内存

1.  在“数据库引擎配置”的“身份验证模式”选项卡，点击 **“添加当前用户”** ，将登录用户添加为 SQL Server 管理员（便于后续管理数据库）。

 ![](https://pkg.changjiu365.cn/assets/27996062.webp) 

SQL Server 2019数据库引擎配置（身份验证模式）：点击“添加当前用户”授予登录用户管理员权限

1.  切换到“内存”选项卡，**勾选“使用推荐的内存设置”** （避免 SQL Server 无限制占用系统内存，导致服务器性能下降），点击“下一步”。

 ![](https://pkg.changjiu365.cn/assets/6bb0793d.webp) 

SQL Server 2019数据库引擎配置（内存选项卡）：勾选“使用推荐的内存设置”以限制内存占用比例

### 步骤 9：完成安装

确认所有配置无误后，点击“安装”开始部署 SQL Server 2019。等待安装完成（约 5-10 分钟，取决于硬件性能）。

 ![](https://pkg.changjiu365.cn/assets/39ee12c4.webp) 

SQL Server 2019安装配置确认界面：点击“安装”启动数据库服务及组件部署

出现“安装成功”提示后，点击“关闭”。

 ![](https://pkg.changjiu365.cn/assets/446c60e2.webp) 

SQL Server 2019安装结果界面：显示“安装成功”及所有组件部署完成

二、SQL Server 管理工具（SSMS）安装步骤
---------------------------

为管理 SQL Server 数据库，需安装 **SQL Server Management Studio (SSMS)** 。

### 步骤 1：下载 SSMS

1.  返回 SQL Server 安装中心，点击左侧 **“安装”** 选项卡，选择 **“安装 SQL Server 管理工具”** ，自动跳转至微软下载页；

 ![](https://pkg.changjiu365.cn/assets/32c48e97.webp) 

SQL Server 2019安装中心“安装”选项卡：选择“安装SQL Server管理工具”以跳转至SSMS下载页面

或直接访问 [SSMS 下载链接](https://learn.microsoft.com/zh-cn/ssms/install/install?redirectedfrom=MSDN)，下载 **SSMS 21**。

 ![](https://pkg.changjiu365.cn/assets/592f043c.webp) 

SQL Server Management Studio (SSMS)官方下载页面：选择下载SSMS 21版本（最新稳定版）

### 步骤 2：安装 SSMS

1.  运行下载的 SSMS 安装程序，点击“继续”（默认安装路径即可，或自定义路径）。

 ![](https://pkg.changjiu365.cn/assets/7fe10728.webp) 

SQL Server Management Studio (SSMS)安装程序启动界面：点击“继续”确认安装路径并开始部署

1.  等待文件提取并自动安装，完成后点击“关闭”。

 ![](https://pkg.changjiu365.cn/assets/727b685c.webp) 

SQL Server Management Studio (SSMS)安装过程：文件自动提取与组件部署中

​

 ![](https://pkg.changjiu365.cn/assets/30df5c8f.webp) 

SQL Server Management Studio (SSMS)安装结果界面：显示“安装成功”

安装验证
----

1.  打开 SSMS（通过开始菜单搜索“SQL Server Management Studio”）；
2.  在“连接到服务器”窗口，服务器名称输入 `localhost`（默认实例），身份验证选择“Windows 身份验证”，点击“连接”。
3.  若成功连接到数据库引擎，说明 SQL Server 2019 及 SSMS 安装完成。

注意事项
----

1.  **版本限制**：Developer 版仅用于开发/测试，生产环境需使用正版授权的 Enterprise/Standard 版。
2.  **排序规则**：`SQL_Latin1_General_CP1_CI_AS` 为 Configuration Manager 强制要求，安装时若选错需卸载重装。
3.  **内存设置**：务必勾选“推荐内存设置”，否则 SQL Server 可能占用 80% 以上系统内存。
4.  **防火墙**：如需远程访问数据库，需在防火墙中允许 SQL Server 默认端口（1433）或实例对应端口。

后续步骤
----

SQL Server 2019 及 SSMS 安装完成后，下一教程将继续介绍 Configuration Manager 的前置配置（如数据库权限、组件安装等）。

‍