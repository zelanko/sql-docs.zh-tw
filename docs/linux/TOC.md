# [關於 Linux 上的 SQL Server](sql-server-linux-overview.md)

# 概觀
## [版本資訊](sql-server-linux-release-notes.md)
## [新功能](sql-server-linux-whats-new.md)
## [新增及更新的發行項](new-updated-linux.md)
## [版本和支援的功能](sql-server-linux-editions-and-components-2017.md)
## [常見問題集](sql-server-linux-faq.md)

# 快速入門
## [安裝與連線 - Red Hat](quickstart-install-connect-red-hat.md)
## [安裝與連線 - SUSE](quickstart-install-connect-suse.md)
## [安裝與連線 - Ubuntu](quickstart-install-connect-ubuntu.md)
## [執行與連線 - Docker](quickstart-install-connect-docker.md)
## [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
## [執行與連線 - 雲端](quickstart-install-connect-clouds.md)

# 教學課程
## [1_從 Windows 移轉](sql-server-linux-migrate-restore-database.md)
## [2_從 Oracle 移轉](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json)
## [3_移轉到 Docker](tutorial-restore-backup-in-sql-server-container.md)
## [4_建立作業](sql-server-linux-run-sql-server-agent-job.md)
## [5_設定 AD 驗證](sql-server-linux-active-directory-authentication.md)
## [6_建立容錯移轉叢集執行個體](sql-server-linux-shared-disk-cluster-configure.md)
### [iSCSI](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
### [NFS](sql-server-linux-shared-disk-cluster-configure-nfs.md)
### [SMB](sql-server-linux-shared-disk-cluster-configure-smb.md)
## [7_部署 Pacemaker 叢集](sql-server-linux-deploy-pacemaker-cluster.md)
## [8_建立及設定可用性群組](sql-server-linux-create-availability-group.md)
## [9_在 Kubernetes 中設定以達到高可用性](tutorial-sql-server-containers-kubernetes.md)

# 概念
## Install
### [安裝 SQL Server](sql-server-linux-setup.md)
### [安裝 SQL Server 工具](sql-server-linux-setup-tools.md)
### [安裝 SQL Server Agent](sql-server-linux-setup-sql-agent.md)
### [安裝 SQL Server 全文檢索搜尋](sql-server-linux-setup-full-text-search.md)
### [安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)
### [設定存放庫](sql-server-linux-change-repo.md)

## 設定
### [使用 mssql-conf 進行設定](sql-server-linux-configure-mssql-conf.md)
### [環境變數](sql-server-linux-configure-environment-variables.md)
### [設定 Docker 容器](sql-server-linux-configure-docker.md)
### [客戶回函](sql-server-linux-customer-feedback.md)

## [開發](sql-server-linux-develop-overview.md)
### [連線程式庫](sql-server-linux-develop-connectivity-libraries.md)
### [使用 Visual Studio Code](sql-server-linux-develop-use-vscode.md)
### [使用 SSMS](sql-server-linux-develop-use-ssms.md)
### [使用 SSDT](sql-server-linux-develop-use-ssdt.md)

## [管理](sql-server-linux-management-overview.md)
### [使用 SSMS 來管理](sql-server-linux-manage-ssms.md)
### [使用 PowerShell 來管理](sql-server-linux-manage-powershell.md)
### [使用記錄傳送](sql-server-linux-use-log-shipping.md)
### [使用 DB Mail 和電子郵件警示](sql-server-linux-db-mail-sql-agent.md)
### [設定可用性的多個子集](sql-server-linux-configure-multiple-subnet.md)

## [移轉](sql-server-linux-migrate-overview.md)
### [從 Windows 匯出和匯入 BACPAC](sql-server-linux-migrate-ssms.md)
### [使用 SQL Server 移轉小幫手來移轉](sql-server-linux-migrate-ssma.md)
### [使用 bcp 大量複製](sql-server-linux-migrate-bcp.md)

## [擷取、轉換、載入](sql-server-linux-migrate-ssis.md)
### [限制與已知問題](sql-server-linux-ssis-known-issues.md)
### [設定 SSIS](sql-server-linux-configure-ssis.md)
### [排程 SSIS 套件](sql-server-linux-schedule-ssis-packages.md)

## [設定商務持續性](sql-server-linux-business-continuity-dr.md)
### [可用性基礎](sql-server-linux-ha-basics.md)
### [備份與還原](sql-server-linux-backup-and-restore-database.md)
#### [虛擬裝置介面 - Linux](sql-server-linux-backup-vdi-specification.md)
### [容錯移轉叢集執行個體](sql-server-linux-shared-disk-cluster-concepts.md)
#### [Red Hat Enterprise Linux (RHEL)]()
##### [設定 (HA 附加元件)](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)
##### [操作 (HA 附加元件)](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
#### [SUSE Linux Enterprise Server (SLES)]()
##### [設定 (HA 附加元件)](sql-server-linux-shared-disk-cluster-sles-configure.md)
### [可用性群組](sql-server-linux-availability-group-overview.md)
#### [為高可用性建立](sql-server-linux-availability-group-ha.md)
##### [設定 AG](sql-server-linux-availability-group-configure-ha.md)
##### [在 RHEL 上設定](sql-server-linux-availability-group-cluster-rhel.md)
##### [在 SLES 上設定](sql-server-linux-availability-group-cluster-sles.md)
##### [在 Ubuntu 上設定](sql-server-linux-availability-group-cluster-ubuntu.md)
##### [容錯移轉](sql-server-linux-availability-group-failover-ha.md)
##### [操作](sql-server-linux-availability-group-operate-ha.md)
#### [僅供讀取級別的建立作業]()
##### [設定 AG](sql-server-linux-availability-group-configure-rs.md)
#### [設定跨平台 (Windows 與 Linux)](sql-server-linux-availability-group-cross-platform.md)

## [Security](sql-server-linux-security-overview.md)
### [開始使用安全性功能](sql-server-linux-security-get-started.md)
### [Active Directory 驗證](sql-server-linux-active-directory-auth-overview.md)
### [為連線加密](sql-server-linux-encrypted-connections.md)

## [效能]
### [最佳做法](sql-server-linux-performance-best-practices.md)
### [開始使用效能功能](sql-server-linux-performance-get-started.md)

# 範例
## 自動安裝
### [Red Hat Enterprise Linux (RHEL)](sample-unattended-install-redhat.md)
### [SUSE Linux Enterprise Server (SLES)](sample-unattended-install-suse.md)
### [Ubuntu](sample-unattended-install-ubuntu.md)

# 資源
## [疑難排解](sql-server-linux-troubleshooting-guide.md)
## [SQL Server 文件](../sql-server/sql-server-technical-documentation.md)
## 夥伴
### [監視](../sql-server/partner-monitor-sql-server.md)
### [高可用性和災害復原](../sql-server/partner-hadr-sql-server.md)
### [管理](../sql-server/partner-management-sql-server.md)
### [開發](../sql-server/partner-dev-sql-server.md)
## [DBA Stack Exchange](https://dba.stackexchange.com/questions/tagged/sql-server)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/sql-server)
## [MSDN 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
## [提交意見反應](https://feedback.azure.com/forums/908035-sql-server)
## [Reddit](https://www.reddit.com/r/SQLServer)