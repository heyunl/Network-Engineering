## Proxmox VE Bundle  Proxmox VE 套装
  Training content  培训内容

- The course provides a mix of theory and practical work, helping participants build competence and confidence in deploying, managing, 和 troubleshooting Proxmox VE clusters:
  该课程提供理论和实践相结合的课程，帮助参与者建立部署、管理和故障排除 Proxmox VE 集群的能力和信心：

# Training content 培训内容

The course provides a mix of theory and practical work, helping participants build competence and confidence in deploying, managing, and troubleshooting Proxmox VE clusters:  
该课程提供理论和实践相结合的课程，帮助参与者建立部署、管理和故障排除 Proxmox VE 集群的能力和信心：

---

## Module 1: Deployment and Management  
### 模块 1：部署和管理

- Understanding the architecture of Proxmox VE with a focus on a single server deployment.  
  了解 Proxmox VE 的架构，重点关注单服务器部署。

- Installing and setting up Proxmox VE: system requirements, installation, updates, and network configuration.  
  安装和设置 Proxmox VE：系统要求、安装、更新和网络配置。

- Exploring the management interfaces (web GUI, CLI).  
  探索管理界面（Web GUI、CLI）。

- Configuring and managing networks in Proxmox VE: Bridging and bonding network interfaces, VLANs, software-defined networking.  
  在 Proxmox VE 中配置和管理网络：桥接和绑定网络接口、VLAN、软件定义网络。

- Storage management: Storage options in Proxmox VE with a focus on single server deployments.  
  存储管理：Proxmox VE 中的存储选项，侧重于单服务器部署。

- Virtual guest management: Creating, managing, and understanding the various options and possibilities for VMs and Linux OS containers (LXC).  
  虚拟来宾管理：创建、管理和了解 VM 和 Linux OS 容器 （LXC） 的各种选项和可能性。

- Migration to Proxmox VE from other hypervisors (V2V) and bare-metal machines (P2V) and recommended post-migration steps.  
  从其他虚拟机管理程序 （V2V） 和裸机计算机 （P2V） 迁移到 Proxmox VE 以及建议的迁移后步骤。

- Backup and restore strategies: Backing up guests with the out-of-the-box backup functionality, exploring the integration with the Proxmox Backup Server, retention management, and restore possibilities.  
  备份和恢复策略：使用开箱即用的备份功能备份来宾，探索与 Proxmox 备份服务器的集成、保留管理和恢复的可能性。

- Authentication and Permissions: Users, groups, authentication realms, and permission schemes.  
  身份验证和权限：用户、组、身份验证领域和权限方案。

- Integrated firewall  
  集成防火墙

- Troubleshooting common issues  
  排查常见问题

---

## Module 2: Clustering and Shared Storage  
### 模块 2：集群和共享存储

- Architecture and components of a Proxmox VE cluster: Requirements, best practices.  
  Proxmox VE 集群的架构和组件：要求、最佳实践。

- Exploring the Proxmox Cluster File System (pmxcfs) and Corosync.  
  探索 Proxmox 群集文件系统 （pmxcfs） 和 Corosync。

- Cluster networking and redundancy, software-defined networking (SDN) and VLANs.  
  群集网络和冗余、软件定义网络 （SDN） 和 VLAN。

- Storage management with shared storage options.  
  使用共享存储选项进行存储管理。

- Deploying Ceph: Hyper-converged infrastructure (HCI), Ceph RBD for guest virtual disk storage, CephFS for clustered file storage, maintenance tasks, and best practices.  
  部署 Ceph：超融合基础设施 （HCI）、用于客户虚拟磁盘存储的 Ceph RBD、用于集群文件存储的 CephFS、维护任务和最佳实践。

- Migration of guests between nodes.  
  节点之间的 Guest 迁移。

- ZFS for asynchronous guest disk replication in a cluster.  
  ZFS 用于群集中的异步来宾磁盘复制。

- High availability (HA) for VMs and containers.  
  VM 和容器的高可用性 （HA）。

- Failure scenarios with exercises for HA and Ceph.  
  带有 HA 和 Ceph 练习的故障场景。

- Considerations for a minimal 2 node setup with an external tiebreaker (QDevice).  
  使用外部仲裁 （QDevice） 进行最少 2 节点设置的注意事项。

- Automate tasks using the Proxmox REST API or CLI tools.  
  使用 Proxmox REST API 或 CLI 工具自动执行任务。

- Troubleshooting common issues  
  排查常见问题
