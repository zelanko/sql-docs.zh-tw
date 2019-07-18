---
title: 什麼&#39;s 新 (Database Engine) |Microsoft Docs
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- what's new [SQL Server Database Engine]
- Database Engine [SQL Server], what's new
ms.assetid: 8f625d5a-763c-4440-97b8-4b823a6e2439
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0650d15ece36593139ae804f6535315eacbf9294
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62843438"
---
# <a name="what39s-new-database-engine"></a>什麼&#39;s 新 (Database Engine)
  這個最新版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 導入了一些新功能和增強功能，可提升設計、開發和維護資料儲存系統之架構設計師、開發人員和管理員的能力和生產力。 以下是 [!INCLUDE[ssDE](../includes/ssde-md.md)] 已增強的範圍。  
  
##  <a name="Feature"></a> Database Engine 功能增強  
  
###  <a name="MemoryOpt"></a> 記憶體最佳化資料表  
 記憶體中 OLTP 是已整合至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 引擎的記憶體最佳化資料庫引擎。 記憶體中 OLTP 已針對 OLTP 最佳化。 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
 
  
###  <a name="DataFiles"></a> 在 Windows Azure 中的 SQL Server 資料檔案  
 [在 Windows Azure 中的 SQL Server 資料檔案](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)提供原生支援[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]資料庫檔案儲存為 Windows Azure Blob。 這項功能可讓您在內部部署執行或 Windows Azure 虛擬機器上執行的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中建立資料庫，以將您的 Windows Azure Blob 儲存體資料儲存在專用儲存位置。  
  
  
###  <a name="AzureVM"></a> 裝載 SQL Server 資料庫中的 Windows Azure 虛擬機器  
 使用[SQL Server Database 部署到 Windows Azure 虛擬機器](https://msdn.microsoft.com/library/dn195938\(v=sql.120\).aspx)精靈來裝載資料庫的執行個體從[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Windows Azure 虛擬機器。  
  
  
###  <a name="Backup"></a> 備份與還原增強功能  
 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 包含 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份與還原的下列增強功能：  
  
-   **SQL Server 備份至 URL**  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份至 URL 原本是在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP1 CU2 中導入，而且只有 [!INCLUDE[tsql](../includes/tsql-md.md)]、PowerShell 和 SMO 提供支援。 在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中，您可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 來備份至 Windows Azure Blob 儲存體服務，或從中還原。 備份工作和維護計畫皆可使用這個新選項。 如需詳細資訊，請參閱 <<c0> [ 使用 SQL Server Management Studio 中的備份工作](../relational-databases/backup-restore/sql-server-backup-to-url.md#BackupTaskSSMS)， [SQL Server 備份至 URL Using Maintenance Plan Wizard](../relational-databases/backup-restore/sql-server-backup-to-url.md#MaintenanceWiz)，和[從 Windows Azure 儲存體還原使用 SQLServer Management Studio](../relational-databases/backup-restore/sql-server-backup-to-url.md#RestoreSSMS)。  
  
-   **SQL Server Managed Backup 到 Windows Azure**  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]建立在 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 備份至 URL 上，它是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供的服務，可用來管理及排程資料庫和記錄備份。 在這個版本中，僅支援備份至 Windows Azure 儲存庫。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]可以同時設定在資料庫和執行個體層級，這樣既可在資料庫層級更精確地控制，還可在執行個體層級自動化。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]可以設定在內部部署執行的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體上，以及在 Windows Azure 虛擬機器執行的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體上。 建議用於在 Windows Azure 虛擬機器上執行的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體。 如需詳細資訊，請參閱 < [SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)。  
  
-   **備份的加密**  
  
     您現在可以選擇在備份作業期間加密備份檔案。  它支援數種加密演算法，包括 AES 128、AES 192、AES 256 和 Triple DES。 在備份期間，您必須使用憑證或非對稱金鑰進行加密。 如需詳細資訊，請參閱＜ [備份加密](../relational-databases/backup-restore/backup-encryption.md)＞。  
  
  
###  <a name="CE"></a> 基數估計的新設計  
 基數估計邏輯 (稱為基數估計工具) 在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中經過重新設計，可改善查詢計劃的品質，從而提升查詢效能。 新的基數估計工具併入了可搭配新型 OLTP 和資料倉儲工作負載完善運作的假設和演算法。 這項發展乃是憑藉著我們針對新型工作負載進行深入的基數估計研究，以及過去 15 年來改進 SQL Server 基數估計工具的經驗。 由客戶的意見反應得知，儘管無論變更與否都能讓大多數的查詢獲益，但與舊版基數估計工具相比，少數的查詢可能會顯現效能退化。 如需效能微調與測試的建議，請參閱[基數估計&#40;SQL Server&#41;](../relational-databases/performance/cardinality-estimation-sql-server.md)。  
   
  
###  <a name="Durability"></a> 延遲的持久性  
 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 導入了將部分或所有交易指定為延遲的持久，藉以降低延遲的能力。 延遲的持久交易會在交易記錄檔記錄寫入磁碟之後，將控制權傳回給用戶端。 您可以在資料庫層級、COMMIT 層級或 ATOMIC 區塊層級控制持久性。  
  
 如需詳細資訊，請參閱主題[控制交易持久性](../relational-databases/logs/control-transaction-durability.md)。  
  
  
###  <a name="AlwaysOn"></a> AlwaysOn 增強功能  
 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 包含 AlwaysOn 容錯移轉叢集執行個體和 AlwaysOn 可用性群組的下列增強功能：  
  
-   加入 Azure 複本精靈可簡化為 AlwaysOn 可用性群組建立混合式方案的作業。 如需詳細資訊，請參閱 <<c0> [ 使用 [加入 Azure 複本精靈] &#40;SQL Server&#41;](availability-groups/windows/use-the-add-azure-replica-wizard-sql-server.md)。</c0>  
  
-   次要複本的最大數目已經從 4 增加為 8。  
  
-   從主要複本中斷連接或是在叢集仲裁遺失期間，可讀取的次要複本現在依然可供讀取工作負載使用。  
  
-   容錯移轉叢集執行個體 (FCI) 現在可使用叢集共用磁碟區 (CSV) 當做叢集共用磁碟。 如需詳細資訊，請參閱 < [Alwayson 容錯移轉叢集執行個體](../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)。  
  
-   新的系統函數[sys.fn_hadr_is_primary_replica](/sql/relational-databases/system-functions/sys-fn-hadr-is-primary-replica-transact-sql)，和新的 DMV [sys.dm_io_cluster_valid_path_names](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql)，可用。  
  
-   下列 Dmv 已增強，現在會傳回 FCI 資訊： [sys.dm_hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql)， [sys.dm_hadr_cluster_members](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)，並[sys.dm_hadr_cluster_networks](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql)。  
  
  
###  <a name="OIR"></a> 切換資料分割和編製索引  
 現在已可重建分割區資料表的個別分割區。 如需詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)。  
   
  
###  <a name="Lock"></a> 管理線上作業的鎖定優先權  
 `ONLINE = ON` 選項現在包含 `WAIT_AT_LOW_PRIORITY` 選項，該選項允許您指定重建程序應該等候必要鎖定多長的時間。 `WAIT_AT_LOW_PRIORITY` 選項也允許您設定與該重建陳述式相關之封鎖處理序的終止。 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql) 和 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)。 中有提供疑難排解的鎖定狀態的新類型的相關資訊[sys.dm_tran_locks &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)並[sys.dm_os_wait_stats &#40;-&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql)。  
 
  
###  <a name="CCI"></a> 資料行存放區索引  
 這些新功能僅適用於資料行存放區索引：  
  
-   **叢集資料行存放區索引**  
  
     使用叢集資料行存放區索引，可提高主要執行大量載入和唯讀查詢的資料倉儲工作負載的資料壓縮和查詢效能。 因為叢集資料行存放區索引可更新，工作負載可以執行許多插入、更新和刪除作業。 如需詳細資訊，請參閱 < [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md)並[Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md)。  
  
-   **SHOWPLAN**  
  
     SHOWPLAN 會顯示有關資料行存放區索引的資訊。 **EstimatedExecutionMode**並**ActualExecutionMode**屬性有兩個可能的值：**批次**或是**資料列**。  **儲存體**屬性有兩個可能的值：**資料列存放區**並**資料行存放區**。  
  
-   **封存資料壓縮**  
  
     ALTER INDEX ...REBUILD 擁有新的 COLUMNSTORE_ARCHIVE 資料壓縮選項可進一步壓縮資料行存放區索引之指定分割區。 使用此選項進行封存，或是在其他需要較小資料儲存大小且允許較長儲存和擷取時間的情況下使用。 如需詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)。  
   
  
###  <a name="Buffer"></a> 緩衝集區延伸模組  
 [緩衝集區延伸模組](configure-windows/buffer-pool-extension.md)提供固態硬碟 (SSD) 無縫整合的非動態隨機存取記憶體 (NvRAM) 延伸模組，以當做[!INCLUDE[ssDE](../includes/ssde-md.md)]緩衝集區，以大幅提升 I/O 輸送量。  
   
  
###  <a name="Stats"></a> 累加統計資料  
 CREATE STATISTICS 和相關統計陳述式現在可以使用累加選項，建立每個分割區的統計資料。 相關陳述式允許或回報累加統計資料。 受影響的語法包括 UPDATE STATISTICS、 sp_createstats、 CREATE INDEX、 ALTER INDEX、 ALTER DATABASE SET 選項、 DATABASEPROPERTYEX、 sys.databases 和 sys.stats。如需詳細資訊，請參閱 [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)。  
  
  
###  <a name="RG"></a> 實體 IO 控制的資源管理員增強功能  
 資源管理員可讓您針對內送應用程式要求可在資源集區使用的 CPU、實體 IO 和記憶體數量指定限制。 在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中，您可以使用新的 MIN_IOPS_PER_VOLUME 和 MAX_IOPS_PER_VOLUME 設定，以針對指定資源集區，控制為使用者執行緒發出的實體 IO 數。 如需詳細資訊，請參閱[Resource Governor Resource Pool](../relational-databases/resource-governor/resource-governor-resource-pool.md)並[CREATE RESOURCE POOL &#40;-&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql)。  
  
 ALTER RESOURCE GOVENOR 的 MAX_OUTSTANDING_IO_PER_VOLUME 設定可設定每個磁碟區的未完成 I/O 作業數上限。 您可以使用此設定來將 IO 資源管理調整為磁碟區的 IO 特性，以及在 SQL Server 執行個體界限用來限制發出的 IO 數目。 如需詳細資訊，請參閱 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)。  
  
  
###  <a name="OnlineEvent"></a> 線上索引作業事件類別  
 線上索引作業事件類別的進度報表現在有兩個新的資料行：**PartitionId**並**PartitionNumber**。 如需詳細資訊，請參閱[進度報表：線上索引作業事件類別](../relational-databases/event-classes/progress-report-online-index-operation-event-class.md)。  
  
  
###  <a name="Compat"></a> 資料庫相容性層級  
 90 相容性層級在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中無效。 如需詳細資訊，請參閱 < [ALTER DATABASE 相容性層級&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
##  <a name="TSQL"></a> Transact-SQL 增強功能  
  
### <a name="inline-specification-of-clustered-and-nonclustered"></a>CLUSTERED 和 NONCLUSTERED 的內嵌指定  
 以磁碟為基礎的資料表現在允許 `CLUSTERED` 和 `NONCLUSTERED` 索引的內嵌指定。 建立包含內嵌索引的資料表相當於發出 create table 且後面緊接著對應的 `CREATE INDEX` 陳述式。 內嵌索引不支援包含的資料行和篩選條件。  
  
### <a name="select--into"></a>選取此項目...INTO  
 `SELECT ... INTO` 陳述式已經改良，現在可以平行操作。 資料庫相容性層級必須至少為 110。  
  
### <a name="includetsqlincludestsql-mdmd-enhancements-for-in-memory-oltp"></a>記憶體中 OLTP 的 [!INCLUDE[tsql](../includes/tsql-md.md)] 增強功能  
 如需[!INCLUDE[tsql](../includes/tsql-md.md)]變更為支援記憶體內部 OLTP，請參閱[記憶體內部 OLTP 的 TRANSACT-SQL 支援](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)。  
  
  
##  <a name="SystemTable"></a> 系統檢視表增強功能  
  
### <a name="sysxmlindexes"></a>sys.xml_indexes  
 [sys.xml_indexes &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-xml-indexes-transact-sql)有 3 個新的資料行： `xml_index_type`， `xml_index_type_description`，並`path_id`。  
  
### <a name="sysdmexecqueryprofiles"></a>sys.dm_exec_query_profiles  
 [sys.dm_exec_query_profiles &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql)監視即時查詢進度，在執行查詢時。  
  
### <a name="syscolumnstorerowgroups"></a>sys.column_store_row_groups  
 [sys.column_store_row_groups &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql)提供來協助進行系統管理決策的系統管理員以每個區段為基礎的叢集資料行存放區索引資訊。  
  
### <a name="sysdatabases"></a>sys.databases  
 [sys.databases &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)有 3 個新的資料行： `is_auto_create_stats_incremental_on`， `is_query_store_on`，並`resource_pool_id`。  
  
### <a name="system-view-enhancements-for-in-memory-oltp"></a>記憶體中 OLTP 的系統檢視表增強功能  
 若要支援記憶體內部 OLTP 的系統檢視表增強功能的相關資訊，請參閱[系統檢視表、 預存程序、 Dmv 和等待類型的記憶體內部 OLTP](../../2014/database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)。  
   
  
##  <a name="Security"></a> 安全性增強功能  
  
### <a name="connect-any-database-permission"></a>CONNECT ANY DATABASE 權限  
 新的伺服器層級權限。 將 **CONNECT ANY DATABASE** 授與登入，該登入必須連線到目前存在的所有資料庫，以及可能於日後建立的任何新資料庫。 不要在任何資料庫中授與超出連接的任何權限。 結合**SELECT ALL USER SECURABLES**或是`VIEW SERVER STATE`若要讓稽核程序的執行個體上檢視所有資料或所有資料庫狀態[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
### <a name="impersonate-any-login-permission"></a>IMPERSONATE ANY LOGIN 權限  
 新的伺服器層級權限。 授與此權限時，可讓中間層程序在連接到資料庫時模擬連接的用戶端帳戶。 拒絕此權限時，高權限登入可能遭到封鎖，而無法模擬其他登入。 例如，具有 **CONTROL SERVER** 權限的登入可能遭到封鎖，而無法模擬其他登入。  
  
### <a name="select-all-user-securables-permission"></a>SELECT ALL USER SECURABLES 權限  
 新的伺服器層級權限。 授與此權限時，像是稽核者這類登入就可以檢視使用者可連接之所有資料庫中的資料。  
  
  
##  <a name="Deployment"></a> 部署增強功能  
### <a name="azure-vm"></a>Azure VM
[將 SQL Server 資料庫部署到 Microsoft Azure 虛擬機器](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md)能夠部署[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]資料庫到 Windows Azure VM。  

### <a name="refs"></a>ReFS
現在支援部署在 ReFS 上的資料庫。   
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 各版本所支援的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
   
