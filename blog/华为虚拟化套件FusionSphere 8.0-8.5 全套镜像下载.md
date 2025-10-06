# 华为虚拟化套件FusionSphere 8.0-8.5 全套镜像下载
FusionSphere 虚拟化解决方案由服务器虚拟化产品（FusionCompute）、虚拟化管理软件（FusionManager）、备份软件（eBackup）和容灾软件（UltraVR）组成。主要实现硬件资源的虚拟化，以及对虚拟化资源集中管理，提高基础备份、容灾，轻量级运营，云基础服务，性能管理等能力。

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/0ce088aa-038f-472b-905c-8116450d7cbe.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/06/img_6479b22bab7a8.png)

FusionSphere架构特点
----------------

*   应用按需分配资源：提供虚拟机资源的可扩展能力，使用户可以按照应用需求随时随地调整虚拟机资源，并且无需中断应用。
*   虚拟资源SLA保障：提供虚拟机资源的控制能力，使用户可以按照应用的重要程度合理地分配物理资源。
*   统一虚拟化数据中心管理：提供虚拟机的创建、部署、转移、迁移等管理能力，并且可以异构管理业界流的第三方虚拟化平台，从管理层屏蔽虚拟化平台差异，实现统一纳管。
*   自动化调度：根据预先设定策略进行工作负载的自动迁移，最终使资源分配达到最优化，保证系统良好的用户体验和业务系统的最佳响应。
*   丰富的运维管理：提供多种运营工具，实现业务的可控、可管，提高整个系统运营的效率。
*   云安全：采用多种安全措施，并遵从信息安全法律法规，对用户接入、管理维护、数据、物理、粗你好等提供端到端的业务保护。
*   应用智能管理：基于完整的审批流程级制提供服务目录和用户自定义模板，方便用户自定义快速部署私有应用。
*   完善的权限管理：根据不同的角色、权限等，提供完善的权限管理功能，授权用户对系统内容的资源进行管理。

FusionSphere 应用场景
-----------------

*   单虚拟化场景：只采用FusionCompute作为统一的操作维护管理平台对整个系统进行操作与维护的应用场景。
*   多虚拟化场景：多套虚拟化环境需要进行统一管理。
*   统一管理和维护：支持同时接入FusionCompute和VMware虚拟化环境，对多虚拟化环境的资源和业务进行统一的管理和维护。
*   统一监控告警：支持对多个虚拟化环境、多种物理设备的告警进行统一接入、监控和管理。

然而，同样作为虚拟化解决方案，我们必然会拿VMware vSphere与华为 FusionSphere进行比较。这里主要作以下说明。

一、虚拟化架构

*   vSphere的核心是由ESXi和vCenter组成。

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/a349f94f-4a69-44e4-8cef-e301710c9d8d.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644cae5aba7f3.png)

*   FusionSphere的核心是FusionCompute，FusionCompute由CNA和VRM组成，对应ESXI和vCenter。

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/38c9b967-a9cc-4e03-9ad5-93458f908d32.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644cae6f7fb5a.png)

二、超融合架构

*   VMware超融合HCI有两种实施方式，一种是通过Dell EMC VxRail超融合一体机部署，另一种是以虚拟化vSphere+软件分布式存储vSAN的部署方式，vSAN是VMware超融合的核心。

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/5d6cdf37-1dab-4291-8f9b-39e6c3073ba2.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644cae834a1e7.png)

*   华为超融合是以FusionCube HCI超融合一体机的形式存在，华为提供的是一体化解决方案。

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/4f747546-b33e-48ce-9d74-d8247a721fff.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644cae8ab9e52.png)

三、软件定义存储

*   当vSAN使用RAID1镜像方式存储，副本数为3时，原始数据为100G，占用空间为300G。

注意，当vSAN允许故障数为1（FTT=1），需要2n+1台主机，即3台才能保证数据安全，若要实现数据自我修复，则需要2n+1+1台，即4台才能保证一台完全损坏后vSAN仍然持续正常运行。

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/00d67a0b-9c47-4fc6-956d-0da60aad2244.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644caea545d9d.png)

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/0c35a223-6c49-4338-9417-844e3799188d.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644caead405eb.png)

*   FusionStorage华为分布式存储，最小节点为3，提供多副本和硬盘级、节点级、机柜级安全策略，与vSAN基本相同。

四、管理层级

*   VMware超融合一切以vCenter为顶层，统一管理。

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/51ff7367-38b8-4e95-98c4-ccf84369623c.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644caed81beff.png)

*   华为超融合以FusionCube控制台为最顶层，FusionCube控制台下是FusionSphere、FusionStorage，FusionSphere下是FusionCompute、备份、容灾，FusionCompute下是VRM和CNA以及对资源的管理。

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/b399e368-034a-4c65-b0f8-4f670339423b.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644caee50f60d.png)

五、其他

*   HA高可用性、DRS资源调度、QOS资源分配等功能双方均支持，但FusionSphere无单机虚拟化能力，最少需要CNA+VRM才能运行。
*   在虚拟机备份上，VMware拥有更大的优势，几乎所有备份软件都支持接入vSphere，而华为只能使用FusionSphere中独立安装的eBackup。
*   群晖Active Backup for Business，提供VMware vSphere和Microsoft Hyper-V虚拟机备份。

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/48615013-b416-4f5c-86d7-c13badaaa914.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644caf003467a.png)

安装说明
----

*   使用vm桌面端虚拟机安装，仅能演示CNA安装、VRM安装和FusionCompute8平台添加主机。
*   无序列号情况下，FusionCompute8仅支持6CPU，超过6CPU会变为90天试用。
*   受环境限制，VRM无法安装进CNA中，只能独立安装。

1、安装CNA，最小内存要求8G，最小硬盘空间80G

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/123230bd-4e4e-4464-937c-cedb452dca80.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644caf95f298c.png)

2、配置完选项保存重启即可

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/bb7aba64-7d10-4011-b920-42c3044dfc39.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644cafbbd6aa1.png)

3、安装VRM，最小内存要求6G，最小硬盘空间120G。安装过程相同。

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/1cc4f335-08a5-4896-8052-552f4c2a53e1.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644cafdd799ba.png)

4、进入FusionCompute控制台，默认账号admin，密码IaaS@PORTAL-CLOUD8!

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/b538c457-4116-497d-8bfd-9391bb39b25e.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644caffd4ebe9.png)

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/bd337580-acde-4c62-99a4-0819e9f3dd57.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644cb00e5524b.png)

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/00fd136d-c5c2-4726-b948-efb1cc479be1.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644cb01c2adb6.png)

[![](https://github.com/heyunl/Network-Engineering/blob/main/blog/2025-10-6%2016-09-34/38cdbf1b-373d-4256-a046-62e2c604bfe5.png?raw=true)
](https://www.ittel.cn/wp-content/uploads/2023/04/img_644cb02365fe6.png)

相关文件下载
------

[FusionSphere 8.0 下载地址](https://pan.baidu.com/s/1gbFgOAPw96-avqezED82Fg?pwd=tcz3)

[华为FusionCompute 8.2 虚拟化套件镜像下载](https://pan.baidu.com/s/1mc6kN_BQ2cIW3Mi8dyhDtg)

提取码：

温馨提示：此处有隐藏内容，点击下方按钮进行查看！

免费

[华为FusionCompute 8.3 虚拟化套件镜像下载](https://pan.baidu.com/s/1UKr26qK4xvnWnDJ3kxsYnA)

提取码：

温馨提示：此处有隐藏内容，点击下方按钮进行查看！

免费

### 华为FusionCompute 8.5 虚拟化套件镜像下载

文件包含：

FusionCompute\_CNA-8.5.0.SPC100-X86\_64.iso
FusionCompute\_CNA-8.5.0-ARM\_64.iso
FusionCompute\_VRM-8.5.0.SPC100-X86\_64.zip
FusionCompute\_VRM-8.5.0-ARM\_64.iso
FusionCompute\_VRM-8.5.0-ARM\_64.zip
FusionCompute\_8.5.0\_Upgrade.zip
FusionComputeUpdateTool\_8.5.0.zip
FusionCompute 8.5.0 产品文档 03.zip
FusionCompute\_VRM-8.5.0.SPC100-X86\_64.iso
FusionCompute\_SIA-8.1.0.1-GuestOSDriver\_X86.zip
FusionCompute-LinuxInstaller-8.5.0.SPC100-X86\_64.zip
FusionCompute-LinuxInstaller-8.5.0-ARM\_64.zip
FusionCompute-K8S-OSImage-EulerOS-2.11-64bit-fc.8.5.0-X86\_64.zip
FusionCompute-K8S-OSImage-EulerOS-2.11-64bit-fc.8.5.0-ARM\_64.zip
FusionCompute-K8S-Software-1.22.1-fc.8.5.0-X86\_64.zip
FusionCompute-K8S-Software-1.22.1-fc.8.5.0-aarch64.zip
FusionCompute-K8S-VMImage-EulerOS-2.11-64bit-fc.8.5.0-X86\_64.zip
FusionCompute-K8S-VMImage-EulerOS-2.11-64bit-fc.8.5.0-ARM.zip
FusionCompute 8.5.0文档
+FusionCompute 8.5.0 升级指导书 01.docx
+FusionCompute 8.5.0 升级错误码和常见问题处理 01.docx

链接：[https://pan.baidu.com/s/1USUhcYX1nxi1e1iclF9M6w?pwd=](https://pan.baidu.com/s/1USUhcYX1nxi1e1iclF9M6w?pwd=)

温馨提示：本处有隐藏内容，点击下方按钮进行查看！

60积分

注：本站统一解压密码为**www.ittel.cn**

1、如果您发现本站资源已经失效或无法下载可以评论留言反馈  
2、本站提供的软件均为 “试用版” 或者 “免费版”，仅供学习和研究使用  
3、友情提醒:内容全部来自网络，安装教程参照压缩包内的Readme.txt编写  
4、如有内容不慎侵犯了您的权益，请速与我联系!  
如有转载请注明出处：[https://www.ittel.cn/archives/18457.html](https://www.ittel.cn/archives/18457.html)