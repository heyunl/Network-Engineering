# Configuration Manager 2403基线版本安装教程：分步图解部署
**系列文章导航**：

*   [第一篇：SQL Server 2019安装教程：Configuration Manager数据库准备](https://www.yinyuee.com/tutorial/windows/sql-server-2019-installation-configuration-manager)
*   [第二篇：Configuration Manager：服务器角色添加与数据库配置教程](https://www.yinyuee.com/tutorial/windows/configuration-manager-prerequisites-server-role-db-setup)
*   \[第三篇：Configuration Manager 基线版本安装教程（本文）\]

一、引言
----

在前两篇教程中，我们已经完成了 **SQL Server 2019 数据库准备**（[第一篇链接](https://www.yinyuee.com/tutorial/windows/sql-server-2019-installation-configuration-manager)）和 **ConfigMgr 先决条件配置**（[第二篇链接](https://www.yinyuee.com/tutorial/windows/configuration-manager-prerequisites-server-role-db-setup)），解决了服务器角色添加、数据库排序规则设置、ODBC驱动安装等关键问题。本文作为系列第三篇，将聚焦于 **Configuration Manager 基线版本的实际安装过程**。

二、准备工作：获取 Configuration Manager 基线安装包
-------------------------------------

安装 ConfigMgr 的核心前提是获取**基线版本安装媒体**（Baseline Media）——这类版本包含完整安装文件，无需依赖前置更新，是全新部署的必备包。关键操作如下：

### 1\. 下载基线版本安装媒体

请阅读微软官方文档（[获取安装媒体 - Configuration Manager | Microsoft Learn](https://learn.microsoft.com/zh-cn/intune/configmgr/core/servers/deploy/install/get-install-media)）下载基线版本，**2403版本（版本号5.00.9128）** ——这是当前可用的**基线版本**（下表中“基线”列标记为“是”），适合全新部署。

### 2\. 版本说明（含基线标记）

根据微软官方文档，当前与基线版本相关的信息如下（重点关注“基线”列）：

| 版本 | 可用性日期 | 支持结束日期 | 基线 | 控制台内更新 |
| --- | --- | --- | --- | --- |
| **2503** | 2025 年 3 月 31 日 | 2026 年 9 月 30 日 | 否 | 是 |
| **2409** | 2024 年 12 月 4 日 | 2026 年 6 月 4 日 | 否 | 是 |
| **2403** | 2024 年 4 月 22 日 | 2025 年 10 月 22 日 | 是（注释1） | 是 |

**注**：表格中“基线”列标记为“是”的版本（如2403）包含完整安装文件，无需依赖其他更新包，是全新安装的首选。

三、开始安装：分步图解 Configuration Manager 部署过程
--------------------------------------

### 1\. 启动安装程序

进入解压后的文件夹，找到 `splash.hta` 文件（ConfigMgr 安装启动器），双击打开。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/32df8992.webp) 

Configuration Manager 安装程序初始界面 - 点击「安装」开始

### 2\. 选择安装类型：典型 vs 自定义（新手建议选典型）

安装程序会提示选择「安装类型」，默认分为**典型安装**和**自定义安装**：

*   **典型安装**：自动配置数据库、站点角色（管理点、分发点）等，适合新手快速部署；
*   **自定义安装**：允许手动调整数据库实例、存储路径、角色配置等，适合有经验的管理员。

**本文选择**：为演示细节，选择「自定义安装」（若追求速度，新手可直接勾选「典型安装」，跳过后续部分配置步骤）。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/e6ff36e6.webp) 

选择安装类型 - 演示自定义安装流程

### 3\. 选择许可证类型：评估版本（180天试用期）

ConfigMgr 提供**评估版本**（Evaluation）和**正式版本**（Retail/Volume License）两种选择：

*   **评估版本**：无需激活，可免费使用 180 天，适合测试或学习；
*   **正式版本**：需要输入产品密钥，用于生产环境。

**本文选择**：评估版本。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/26dacc79.webp) 

选择评估版本 - 180天免费试用

### 4\. 接受许可条款（必须勾选）

阅读微软软件许可条款后，勾选「我接受许可条款和条件」，点击「下一步」。

**注意**：若未勾选，安装程序将无法继续。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/2f40c298.webp) 

接受许可条款 - 继续安装的必要步骤

### 5\. 设置安装文件下载路径

选择一个**空闲空间充足的磁盘**，这里大概会下载1.4G的文件，用于存储安装过程中下载的依赖文件。

**示例路径**：`D:\MCM`。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/5fd35686.webp) 

选择安装文件存储路径 - 建议使用非系统盘

### 6\. 选择语言（默认即可）

安装程序会自动勾选**英文**（基础语言）和**当前系统语言**（如中文），无需额外调整。

**说明**：若需支持其他语言，可在安装后通过「Configuration Manager 控制台」添加语言包。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/35c49b54.webp) 

语言设置 - 默认包含英文和系统语言

### 7\. 配置站点信息（关键标识）

*   **站点名称**：输入名称（如 `CJJ`），用于区分不同站点；
*   **站点代码**：自动生成（如 `CJJ`），无需修改（需确保唯一性）。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/fb71eea6.webp) 

配置站点名称 - 建议使用辨识度高的名称

### 8\. 选择站点类型：独立主站点（首次安装必选）

首次部署 ConfigMgr 时，必须选择**以独立站点形式安装主站点**（Standalone Primary Site），这是最常见的部署模式（后续可添加子站点或管理中心站点）。

**说明**：若选择「子站点」，需先部署主站点，因此首次安装必选独立主站点。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/4ba4389d.webp) 

选择站点类型 - 首次安装必选独立主站点

### 9\. 数据库配置（默认即可，除非有命名实例）

*   **SQL Server 实例**：默认使用「默认实例」（`MSSQLSERVER`），若之前安装了命名实例（如 `SQL2019`），需手动输入；
*   **数据库名称**：自动生成（如 `CM_CJJ`），无需修改。

**注意**：若数据库实例未正确配置（如排序规则不符合要求），前两篇教程已解决，此处可直接下一步。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/b72e3f6a.webp) 

数据库实例配置 - 默认使用MSSQLSERVER实例

### 10\. 设置 SQL 数据与日志存储路径（默认即可）

安装程序会自动将 SQL 数据文件（.mdf）和日志文件（.ldf）存储在 SQL Server 的默认路径（如 `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA`）。

**说明**：若需调整，可点击「浏览」选择其他路径，此处保持默认。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/043b2d11.webp) 

SQL 数据与日志存储路径 - 默认配置即可

### 11\. 配置 SMS 提供程序（默认即可）

SMS 提供程序是 ConfigMgr 控制台与数据库之间的接口，默认安装在**本地服务器**（即当前部署 ConfigMgr 的服务器）。

**说明**：若需将 SMS 提供程序安装在其他服务器，需确保该服务器已满足先决条件（如 .NET Framework 4.8、SQL Server 客户端工具等）。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/c820b0c7.webp) 

SMS 提供程序设置 - 默认安装在本地服务器

### 12\. 客户端通信设置（灵活配置）

选择**针对每个站点系统角色配置通信方法**（兼容性更好），这样可以为不同角色（如管理点、分发点）设置不同的通信协议（如 EHTTP/HTTPS）。

**说明**：若选择「使用 EHTTP 进行客户端通信」，所有角色将统一使用 EHTTP，适合测试环境；若需安全通信，可后续配置 HTTPS。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/44dc5c70.webp) 

客户端通信配置 - 推荐灵活设置每个角色的通信方式

### 13\. 安装站点系统角色（默认勾选关键角色）

安装程序会自动勾选**管理点**（Management Point）和**分发点**（Distribution Point），这两个角色是 ConfigMgr 运行的核心：

*   **管理点**：负责客户端与站点服务器之间的通信（如配置下发、状态报告等）；
*   **分发点**：负责存储和分发软件包、更新等内容。

**说明**：若需安装其他角色（如软件更新点、应用程序目录），可在安装后添加。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/f133b699.webp) 

站点角色安装 - 默认包含管理点和分发点

### 14\. 跳过云服务连接（暂时不配置）

选择**暂时跳过连接云服务**。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/3c17efa5.webp) 

云服务配置 - 暂时跳过，后续可再设置

### 15\. 先决条件检查（必须通过）

安装程序会自动检查所有先决条件（如服务器角色、数据库配置、ODBC 驱动等），若有失败，需回到前两篇教程解决。

**常见失败项**：

*   服务器角色未添加（如 Web 服务器、远程差分压缩）；
*   SQL Server 排序规则不符合要求（需为 `SQL_Latin1_General_CP1_CI_AS`）；
*   ODBC 驱动未安装（需安装 SQL Server Native Client 11.0）。

**解决方法**：根据失败提示，参考前两篇教程逐一修复，修复后点击「重新运行检查」，直至所有项显示「通过」。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/159db9a0.webp) 

先决条件检查 - 全部通过后可开始安装

### 16\. 开始安装（等待完成）

点击「开始安装」后，安装程序将开始复制文件、配置数据库、安装角色等操作，耗时约 30-60 分钟（取决于服务器性能）。

**注意**：安装过程中请勿关闭安装程序或重启服务器，否则可能导致安装失败。

### 17\. 安装完成（验证成功）

当安装程序显示「安装完成」时，点击「关闭」，即可打开 Configuration Manager 控制台验证部署结果：

*   打开「Configuration Manager 控制台」，检查「Administration」→「Site Configuration」→「Sites」中的站点状态（应为「正常」）；
*   查看安装日志（路径：`SMSSETUP\LOGS\setup.log`），确认无错误信息。

**图片说明**：  
​

 ![](https://pkg.changjiu365.cn/assets/f408118d.webp) 

安装完成 - 点击关闭即可开始使用

四、总结
----

本文详细讲解了 Configuration Manager 基线版本的安装过程，覆盖了从获取安装包到验证部署的每一步。通过前两篇的先决条件准备和本文的安装步骤，你已成功部署了 ConfigMgr 主站点。下一步，你可以开始探索 ConfigMgr 的核心功能（如软件部署、更新管理、设备管理等）。

若在安装过程中遇到问题，可参考前两篇教程或查看 ConfigMgr 安装日志（`SMSSETUP\LOGS`），也可以在评论区留言讨论。