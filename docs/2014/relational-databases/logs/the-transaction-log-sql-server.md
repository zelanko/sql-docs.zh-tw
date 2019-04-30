---
title: 交易記錄 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], about
- databases [SQL Server], transaction logs
- logs [SQL Server], transaction logs
ms.assetid: d7be5ac5-4c8e-4d0a-b114-939eb97dac4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1b4a175ad850ccbb0711a0997c3658cf01497686
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63144614"
---
# <a name="the-transaction-log-sql-server"></a>交易記錄 (SQL Server)
  每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫都擁有交易記錄檔來記錄所有交易，以及交易在資料庫中所作的修改。 必須定期截斷交易記錄，以免被填滿。 但是，某些因素會影響記錄的截斷，所以監控記錄大小非常重要。 某些作業可使用最低限度記錄，以減少其對交易記錄大小的影響。  
  
 交易記錄是資料庫的重要元件，而且如果系統故障，就可能需要交易記錄讓資料庫返回一致的狀態。 永遠不要刪除或移動交易記錄，除非您完全了解執行這些動作的詳細情形。  
  
> [!NOTE]  
>  檢查點會在資料庫復原期間建立開始套用交易記錄的已知恰當起點。 如需詳細資訊，請參閱[資料庫檢查點 &#40;SQL Server&#41;](database-checkpoints-sql-server.md)。  
  
 **本主題內容：**  
  
-   [優點：交易記錄所支援的作業](#Benefits)  
  
-   [交易記錄截斷](#Truncation)  
  
-   [可能會延遲記錄截斷的因素](#FactorsThatDelayTruncation)  
  
-   [可以進行最低限度記錄的作業](#MinimallyLogged)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="Benefits"></a> 優點：交易記錄所支援的作業  
 交易記錄檔支援下列作業：  
  
-   復原個別的交易。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動時，復原所有未完成的交易。  
  
-   將還原的資料庫、檔案、檔案群組或頁面向前復原到失敗點。  
  
-   支援異動複寫。  
  
-   支援高可用性和災害復原解決方案： [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]、資料庫鏡像和記錄傳送。  
  
##  <a name="Truncation"></a> 交易記錄截斷  
 記錄截斷會釋出記錄檔中的空間，以供交易記錄重複使用。 為了避免記錄被填滿，必須截斷記錄。 記錄截斷會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的邏輯交易記錄中，刪除非使用中的虛擬記錄檔，釋出邏輯記錄中的空間以供實體交易記錄重複使用。 如果永遠都不截斷交易記錄，最終將會填滿配置給其實體記錄檔的所有磁碟空間。  
  
 為了避免這個問題，除非記錄截斷因為某個原因而延遲，否則將在以下事件後自動進行截斷：  
  
-   在簡單復原模式下，發生在檢查點之後。  
  
-   在完整復原模式或大量記錄復原模式下，如果上一次備份之後已產生檢查點，則截斷會發生在記錄備份之後 (除非它是只複製的記錄備份)。  
  
 如需詳細資訊，請參閱本主題稍後的＜ [可能會延遲記錄截斷的因素](#FactorsThatDelayTruncation)＞。  
  
> [!NOTE]  
>  記錄截斷並不會讓實體記錄檔變小。 若要減少實體記錄檔的實體大小，您必須壓縮記錄檔。 如需有關壓縮實體記錄檔大小的詳細資訊，請參閱＜ [管理交易記錄檔的大小](manage-the-size-of-the-transaction-log-file.md)＞。  
  
##  <a name="FactorsThatDelayTruncation"></a> 可能會延遲記錄截斷的因素  
 當記錄檔記錄有一段很長的時間維持在使用中狀態時，交易記錄截斷會延遲，而且可能會讓交易記錄填滿。  
  
> [!IMPORTANT]  
>  如需如何對應寫滿交易記錄的相關資訊，請參閱 [Troubleshoot a Full Transaction Log &#40;SQL Server Error 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)。  
  
 記錄截斷可能會因為各種因素而延遲。 若要探索是否有任何原因導致記錄截斷無法進行，請查詢 **sys.databases** 目錄檢視的 **log_reuse_wait** 和 [log_reuse_wait_desc](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 資料行。 下表描述這些資料行的值。  
  
|log_reuse_wait 值|log_reuse_wait_desc 值|描述|  
|----------------------------|----------------------------------|-----------------|  
|0|NOTHING|目前有一個或多個可重複使用的虛擬記錄檔。|  
|1|CHECKPOINT|自從上次記錄截斷後尚未出現任何檢查點，或是記錄標頭尚未移到虛擬記錄檔的範圍之外。 (所有復原模式)<br /><br /> 這是延遲記錄截斷的一般原因。 如需詳細資訊，請參閱[資料庫檢查點 &#40;SQL Server&#41;](database-checkpoints-sql-server.md)。|  
|2|LOG_BACKUP|在截斷交易記錄前，需要進行記錄備份。 (僅限完整或大量記錄復原模式)<br /><br /> 當下一個記錄備份完成後，某些記錄空間可能就可以重複使用。|  
|3|ACTIVE_BACKUP_OR_RESTORE|正在進行資料備份或還原 (所有復原模式)。<br /><br /> 如果資料備份阻礙截斷記錄，則取消備份作業可能有助於化解眼前的問題。|  
|4|ACTIVE_TRANSACTION|交易在使用中 (所有復原模式)。<br /><br /> 長時間執行的交易可能存在於記錄備份的開頭。 在此情況下，釋出空間可能需要另一個記錄備份。 請注意，長時間執行的交易就會防止記錄截斷，包括簡單復原模式，在其下會截斷交易記錄通常在每個自動檢查點的所有復原模式下。<br /><br /> 延遲交易。 *「延遲交易」* 實際上是回復遭到封鎖的使用中交易 (因為某些無法使用的資源所造成)。 如需有關延遲交易的原因以及如何將延遲交易移出延遲狀態的詳細資訊，請參閱[延遲交易 &#40;SQL Server&#41;](../backup-restore/deferred-transactions-sql-server.md)。 <br /><br />長時間執行的交易可能也會填滿 tempdb 的交易記錄。 內部物件的使用者交易會隱含地使用 tempdb，例如進行排序的工作資料表、進行雜湊處理的工作檔案、資料指標工作資料表，以及資料列版本設定。 即使使用者交易只包括讀取資料 （SELECT 查詢），可能會建立和使用在使用者交易內部物件。 因此，可能會填滿 tempdb 交易記錄。|  
|5|DATABASE_MIRRORING|資料庫鏡像已暫停，或者在高效能模式下，鏡像資料庫已大幅落後主體資料庫。 (僅限完整復原模式)<br /><br /> 如需詳細資訊，請參閱[資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。|  
|6|REPLICATION|進行異動複寫期間，與發行集相關的交易仍然未傳遞至散發資料庫。 (僅限完整復原模式)<br /><br /> 如需有關異動複寫的詳細資訊，請參閱＜ [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md)＞。|  
|7|DATABASE_SNAPSHOT_CREATION|正在建立資料庫快照集。 (所有復原模式)<br /><br /> 這是延遲記錄截斷的一般原因 (通常也是暫時的原因)。|  
|8|LOG_SCAN|正在進行記錄掃描。 (所有復原模式)<br /><br /> 這是延遲記錄截斷的一般原因 (通常也是暫時的原因)。|  
|9|AVAILABILITY_REPLICA|可用性群組的次要複本正在將這個資料庫的交易記錄檔記錄套用到對應的次要資料庫。 (完整復原模式)<br /><br /> 如需詳細資訊，請參閱 < [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)。|  
|10|-|僅供內部使用|  
|11|-|僅供內部使用|  
|12|-|僅供內部使用|  
|13|OLDEST_PAGE|如果將資料庫設定為使用間接檢查點，資料庫中最舊的頁面可能會比檢查點 LSN 更舊。 在此情況下，最舊的頁面可能會延遲記錄截斷。 (所有復原模式)<br /><br /> 如需間接檢查點的相關資訊，請參閱 [Database Checkpoints &#40;SQL Server&#41;](database-checkpoints-sql-server.md)。|  
|14|OTHER_TRANSIENT|這個值目前尚未使用。|  
|16|XTP_CHECKPOINT|當資料庫具有記憶體最佳化的檔案群組時，交易記錄檔可能會等到自動 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 檢查點觸發 (當記錄大小每成長 512 MB 時執行) 時，才會截斷記錄。<br /><br /> 注意:若要截斷交易記錄，512 MB 的大小之前，資料發出 Checkpoint 命令手動對有問題。|  
  
##  <a name="MinimallyLogged"></a> 可以進行最低限度記錄的作業  
 「最低限度記錄」 包含僅記錄復原交易所需的資訊，不支援時間點復原。 這個主題將識別在大量記錄復原模式下 (以及簡單復原模式下，但備份正在執行時除外) 會進行最低限度記錄的作業。  
  
> [!NOTE]  
>  記憶體最佳化資料表不支援最低限度記錄。  
  
> [!NOTE]  
>  在完整復原模式下，將完整記錄所有大量作業。 不過，您可以暫時針對大量作業，將資料庫切換成大量記錄復原模式，藉以將大量作業集的記錄降至最低。 最低限度記錄會比完整記錄更具效率，並降低大規模的大量作業在大量交易期間，填滿可用交易記錄空間的可能性。 然而，如果資料庫在最低限度記錄作用時損毀或遺失，您就無法將資料庫復原至失敗點。  
  
 下列作業 (在完整復原模式下會完整記錄) 在簡單和大量記錄復原模式下會進行最低限度記錄：  
  
-   大量匯入作業 ([bcp](../../tools/bcp-utility.md)、[BULK INSERT](/sql/t-sql/statements/bulk-insert-transact-sql) 及 [INSERT...SELECT](/sql/t-sql/statements/insert-transact-sql))。 如需何時大量匯入至資料表會採用最低限度記錄的詳細資訊，請參閱＜ [Prerequisites for Minimal Logging in Bulk Import](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)＞。  
  
    > [!NOTE]  
    >  啟用異動複寫時，即使在大量記錄復原模式下也會完整記錄 BULK INSERT 作業。  
  
-   SELECT [INTO](/sql/t-sql/queries/select-into-clause-transact-sql) 作業。  
  
    > [!NOTE]  
    >  啟用異動複寫時，即使在大量記錄復原模式下也會完整記錄 SELECT INTO 作業。  
  
-   插入或附加新資料時，在 [UPDATE](/sql/t-sql/queries/update-transact-sql) 陳述式中使用 .WRITE 子句，對大數值資料類型執行的部分更新。 請注意，更新現有值時不使用最低限度記錄。 如需有關大數值資料類型的詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)。  
  
-   [WRITETEXT](/sql/t-sql/queries/writetext-transact-sql)並[UPDATETEXT](/sql/t-sql/queries/updatetext-transact-sql)陳述式時插入或附加新資料插入`text`， `ntext`，和`image`資料類型資料行。 請注意，更新現有值時不使用最低限度記錄。  
  
    > [!NOTE]  
    >  WRITETEXT 與 UPDATETEXT 陳述式已被取代，所以您應該避免在新的應用程式中使用它們。  
  
-   如果資料庫設定為簡單或大量記錄復原模式，則不管作業是離線執行或線上執行，某些索引 DDL 作業都是以最低限度的方式記錄。 以最低限度方式記錄的索引作業如下：  
  
    -   [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql) 作業 (包括索引檢視表)。  
  
    -   [ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql) REBUILD 或 DBCC DBREINDEX 作業。  
  
        > [!NOTE]  
        >  DBCC DBREINDEX 陳述式已被取代，所以您應該避免在新的應用程式中使用它。  
  
    -   DROP INDEX 新堆積重建 (如果適用)。  
  
        > [!NOTE]  
        >  [DROP INDEX](/sql/t-sql/statements/drop-index-transact-sql) 作業期間的索引頁取消配置永遠都是完整記錄。  
  
##  <a name="RelatedTasks"></a> 相關工作  
 `Managing the transaction log`  
  
-   [管理交易記錄檔的大小](manage-the-size-of-the-transaction-log-file.md)  
  
-   [寫滿交易記錄疑難排解 &#40;SQL Server 錯誤 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
 **備份交易記錄 (完整復原模式)**  
  
-   [備份交易記錄 &#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **還原交易記錄 (完整復原模式)**  
  
-  [還原交易記錄備份](../backup-restore/restore-a-transaction-log-backup-sql-server.md)   
  
## <a name="see-also"></a>另請參閱  
 [控制交易持久性](control-transaction-durability.md)   
 [大量匯入採用最低限度記錄的必要條件](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
 [SQL Server 資料庫的備份與還原](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [資料庫檢查點 &#40;SQL Server&#41;](database-checkpoints-sql-server.md)   
 [檢視或變更資料庫的屬性](../databases/view-or-change-the-properties-of-a-database.md)   
 [復原模式 &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)  
  
  
