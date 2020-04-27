---
title: 支援的 SQL Server 功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 660515f10797e1f11fac22c1baf4ed74e9f67c0c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63157240"
---
# <a name="supported-sql-server-features"></a>支援的 SQL Server 功能
  本主題會討論在使用記憶體最佳化的物件時，所支援或不支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。  
  
## <a name="ssnoversion-features-supported-for-in-memory-oltp"></a>記憶體中 OLTP 支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能  
 擁有記憶體最佳化之物件的資料庫可以支援下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能，包括記憶體最佳化的檔案群組在內。  
  
 如需有關支援之資料類型的資訊，請參閱＜ [Supported Data Types](supported-data-types-for-in-memory-oltp.md)＞。  
  
-   記憶體最佳化之資料表支援的選項和作業。 如需詳細資訊，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)。  
  
-   原生編譯的預存程序上支援的選項和作業。 如需詳細資訊，請參閱 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)。  
  
-   能夠使用解譯的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 存取記憶體最佳化的資料表。 解譯的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 會提供相當於存取不是記憶體最佳化的資料表的介面區，其方式是使用非原生編譯的預存程序和使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)]。 如需詳細資訊，請參閱[使用解譯的 Transact-SQL 存取記憶體最佳化的資料表](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)。  
  
-   多重版本設定和開放式並行存取控制。 如需詳細資訊，請參閱 [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md)。  
  
-   備份和還原包含記憶體最佳化之資料檔案群組的資料庫。 如需詳細資訊，請參閱 [SQL Server 資料庫的備份與還原](../backup-restore/back-up-and-restore-of-sql-server-databases.md)。  
  
-   為了可支援性而提供的目錄檢視、動態管理檢視和擴充的事件。 如需詳細資訊，請參閱[記憶體內部 OLTP 的系統檢視表、預存程序、DMV 和等待類型](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件。 如需詳細資訊，請參閱[記憶體內部 OLTP 的 SQL Server 管理物件支援](sql-server-management-objects-support-for-in-memory-oltp.md)。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 如需詳細資訊，請參閱[記憶體內部 OLTP 的 SQL Server Management Studio 支援](sql-server-management-studio-support-for-in-memory-oltp.md)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell。 如需詳細資訊，請參閱 ＜ [SQL Server PowerShell 概觀](https://msdn.microsoft.com/library/cc281954\(SQL.105\).aspx)＞。  
  
-   使用 bcp 公用程式匯入及匯出大量資料。 如需詳細資訊，請參閱[使用 bcp 公用程式匯入及匯出大量資料 &#40;SQL Server&#41;](../import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)。  
  
-   當機復原。  
  
-   記憶體最佳化的資料檔案群組中，有多個容器可以用於儲存記憶體中 OLTP 物件，可以縮短復原時間目標 (RTO)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交易記錄區塊會計算總和檢查碼及驗證。  
  
-   新的 SNAPSHOT 資料表提示。 如需詳細資訊，請參閱[資料表提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)。  
  
-   DB COMPAT 層級。  
  
-   部分自主資料庫。 支援自主資料庫驗證。 不過，所有記憶體中 OLTP 物件在 DMV dm_db_uncontained_entities 中都會標示為中斷內含項目 (Breaking Containment)。  
  
-   Service Broker 有限制。 無法從原生編譯的預存程序存取佇列。 也無法在存取記憶體最佳化的資料表的交易中存取遠端資料庫內的佇列。  
  
-   容錯移轉叢集： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Alwayson 容錯移轉叢集實例會利用 Windows Server 容錯移轉叢集（WSFC）功能，透過伺服器實例層級的冗余來提供本機高可用性-容錯移轉叢集實例（FCI）。 如需詳細資訊，請參閱 [AlwaysOn 容錯移轉叢集執行個體 (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)。  
  
-   與 AlwaysOn 整合： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供幾個選項用於建立伺服器或資料庫的高可用性，包括 AlwaysOn。 如需詳細資訊，請參閱 [高可用性解決方案 &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)。  
  
-   記錄傳送： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄傳送可讓您將主要伺服器執行個體上之主要資料庫中的交易記錄備份，自動傳送到個別之次要伺服器執行個體上的一或多個次要資料庫。 如需詳細資訊，請參閱[關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)。  
  
-   訂閱者端記憶體最佳化資料表的異動複寫受到支援，但是有一些限制。 如需詳細資訊，請參閱複寫[至記憶體優化資料表訂閱者](../replication/replication-to-memory-optimized-table-subscribers.md)。  
  
-   資源管理員： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源管理員功能可讓您用於管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作負載及系統資源耗用。 Resource Governor 可讓您指定內送應用程式要求所能使用的 CPU、實體 IO 和記憶體數量限制。 如需相關資訊，請參閱 [Managing Memory for In-Memory OLTP](../../database-engine/managing-memory-for-in-memory-oltp.md) 及 [Resource Governor](../resource-governor/resource-governor.md)。  
  
-   In-Memory OLTP 對於記憶體最佳化資料表中 (var)char 資料行支援的字碼頁，以及索引和原生編譯預存程序中支援的定序有其限制。 如需詳細資訊，請參閱 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)。  
  
-   BACPAC 支援。  
  
## <a name="ssnoversion-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體內部 OLTP 不支援的功能  
 擁有記憶體最佳化之物件的資料庫不支援下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能，包括記憶體最佳化的資料檔案群組在內。  
  
|不支援的功能|功能描述|  
|-------------------------|-------------------------|  
|記憶體最佳化之資料表的資料壓縮。|使用資料壓縮功能有助於將資料壓縮在資料庫內及縮小資料庫的大小。 如需詳細資訊，請參閱 [Data Compression](../data-compression/data-compression.md)。|  
|分割記憶體最佳化的資料表與雜湊索引。|資料分割資料表和索引的資料，已分成可以在資料庫中的多個檔案群組之間分佈的單位。 如需詳細資訊，請參閱＜ [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md)＞。|  
|記憶體最佳化資料庫資料檔案群組上的透明資料加密 (Transparent Data Encryption，TDE)。|透明資料加密 (TDE) 會執行資料和記錄檔的即時 I/O 加密和解密。 如需詳細資訊，請參閱[透明資料加密 &#40;TDE&#41;](../security/encryption/transparent-data-encryption.md)。<br /><br /> TDE 可在具有記憶體中 OLTP 物件的資料庫上啟用。 如果啟用 TDE，則會加密記憶體中 OLTP 記錄。 持久性資料表的檢查點檔案不會加密，即便在資料庫上啟用 TDE 也是一樣。|  
|複寫|訂閱者端記憶體最佳化資料表的異動複寫以外的複寫組態與參考記憶體最佳化資料表的資料表或檢視表不相容。 如果有記憶體優化的檔案群組，則不支援使用 sync_mode = ' 資料庫快照集 ' 的複寫。 如需詳細資訊，請參閱複寫[至記憶體優化資料表訂閱者](../replication/replication-to-memory-optimized-table-subscribers.md)。|  
|Multiple Active Result Set (MARS)|記憶體最佳化資料表不支援 Multiple Active Result Sets (MARS)。 此錯誤也可能表示使用連結的伺服器。 連結的伺服器可以使用 MARS。 記憶體最佳化資料表中不支援連結的伺服器。 請改為直接連接至裝載記憶體最佳化資料表的伺服器和資料庫。|  
|鏡像|資料庫鏡像是增加 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫可用性的解決方案。 如需詳細資訊，請參閱[資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。|  
|重建記錄檔|具有 MEMORY_OPTIMIZED_DATA 檔案群組的資料庫不支援透過附加或 ALTER DATABASE 重建記錄檔。|  
|連結的伺服器|如需詳細資訊，請參閱 [連結的伺服器 &#40;Database Engine&#41;](../linked-servers/linked-servers-database-engine.md)。|  
|大量記錄|無論資料庫使用何種復原模式，所有在持久性記憶體最佳化的資料表上的作業，一律會完整記錄。|  
|最低限度記錄|記憶體最佳化資料表不支援最低限度記錄。 如需最低限度記錄的詳細資訊，請參閱[交易記錄 &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md) 和[大量匯入採用最低限度記錄的必要條件](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)。|  
|變更追蹤|變更追蹤可在具有記憶體中 OLTP 物件的資料庫上啟用。 不過，記憶體最佳化的資料表中的變更不會受到追蹤。|  
|DDL 觸發程序|記憶體中 OLTP 資料表和原生編譯預存程序中不支援資料庫層級與伺服器層級的 DDL 觸發程序。|  
|異動資料擷取 (CDC)|CDC 不應在具有記憶體中 OLTP 物件的資料庫上啟用，因為它會阻止特定作業，例如 DROP。|  
|資料庫內含項目|具有原生編譯的預存程序和記憶體最佳化資料表的資料庫不支援資料庫內含項目。 如需相關資訊，請參閱 [Contained Databases](../databases/contained-databases.md)|  
|內容連接|不支援使用內容連接，從 CLR 預存程序內部存取記憶體最佳化的資料表。|  
|資料指標|存取記憶體最佳化資料表之查詢上的索引鍵集與動態資料指標。 這些查詢會降級為靜態，變成唯讀。|  
|TABLESTAMP|不支援 TABLESTAMP。 如需詳細資訊，請參閱 [FROM &#40;Transact-SQL&#41;](/sql/t-sql/queries/from-transact-sql)。|  
|AUTO_CLOSE|不支援 AUTO_CLOSE。 如需詳細資訊，請參閱 [Set the AUTO_CLOSE Database Option to OFF](../policy-based-management/set-the-auto-close-database-option-to-off.md)。|  
|資料庫快照集|不支援資料庫快照集。 如需詳細資訊，請參閱[資料庫快照集 &#40;SQL Server&#41;](../databases/database-snapshots-sql-server.md)。|  
|交易式 DDL|記憶體中 OLTP 不支援交易式 DDL。|  
|事件通知|不支援事件通知。 如需詳細資訊，請參閱 [Event Notifications](../service-broker/event-notifications.md)。|  
|Fiber 模式|記憶體中 OLTP 不支援 Fiber 模式。|  
|原則式管理 (PBM)。|不會阻止並只記錄 PBM 的模式。 伺服器上存在這類原則時，可能會使記憶體中 OLTP DDL 無法成功執行。 支援視需要和依排程模式。|  
|DACFX 部署/擷取|記憶體中 OLTP 不支援 DAC Framework 部署/擷取。|  
  
 有一些例外狀況，不支援跨資料庫的交易。 下表描述支援的案例和對應的限制。 (另請參閱 [跨資料庫查詢](cross-database-queries.md))。  
  
|資料庫|允許|描述|  
|---------------|-------------|-----------------|  
|使用者資料庫、模型和 msdb|否|不支援跨資料庫的查詢和交易。<br /><br /> 存取記憶體最佳化的資料表或原生編譯的預存程序的查詢和交易都無法存取其他資料庫，但是系統資料庫 master (用於唯讀存取) 和 tempdb 例外。|  
|資源資料庫和 tempdb|是|跨資料庫交易並沒有限制，除了單一使用者資料庫以外，只能使用資源資料庫和 tempdb。|  
|master|唯讀|如果包含任何寫入 master 資料庫的作業，則接觸記憶體中 OLTP 和 master 資料庫的跨資料庫交易認可會失敗。 只允許從 master 讀取及使用一個使用者資料庫的跨資料庫交易。|  
  
## <a name="see-also"></a>另請參閱  
 [記憶體中 OLTP 的 SQL Server 支援](sql-server-support-for-in-memory-oltp.md)  
  
  
