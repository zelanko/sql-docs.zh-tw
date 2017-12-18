---
title: "管理和監視異動資料擷取 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: track-changes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- change data capture [SQL Server], monitoring
- change data capture [SQL Server], administering
- change data capture [SQL Server], jobs
ms.assetid: 23bda497-67b2-4e7b-8e4d-f1f9a2236685
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0528c9fb9751aadc11f7896347538d5a200b0290
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="administer-and-monitor-change-data-capture-sql-server"></a>管理和監視異動資料擷取 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] 本主題描述如何管理及監視異動資料擷取。  
  
##  <a name="Capture"></a> 擷取作業  
 擷取作業是透過執行無參數的預存程序 **sp_MScdc_capture_job**起始的。 這個預存程序一開始會從 msdb.dbo.cdc_jobs 中擷取作業之 *maxtrans*、 *maxscans*、 *continuous*和 *pollinginterval* 的設定值。 然後，這些設定值會當作參數傳遞給 **sp_cdc_scan**預存程序。 這個預存程序是用來叫用 **sp_replcmds** ，以便執行記錄檔掃描。  
  
### <a name="capture-job-parameters"></a>擷取作業參數  
 若要了解擷取作業行為，您必須了解 **sp_cdc_scan**如何使用可設定的參數。  
  
#### <a name="maxtrans-parameter"></a>maxtrans 參數  
 *maxtrans* 參數會指定可以在記錄檔之單一掃描循環中處理的最大交易數目。 在掃描期間，如果要處理的交易數目達到這個限制，目前的掃描就不會加入其他任何交易。 在掃描循環完成之後，已處理的交易數目一定會小於或等於 *maxtrans*。  
  
#### <a name="maxscans-parameter"></a>maxscans 參數  
 *maxscans* 參數會指定傳回 (continuous = 0) 或執行 Waitfor (continuous = 1) 之前嘗試清空記錄檔的最大掃描循環數目。  
  
#### <a name="continous-parameter"></a>continous 參數  
 *continuous* 參數會控制 **sp_cdc_scan** 在清空記錄檔或執行最大掃描循環數目 (一次模式) 之後讓出控制權。 它也會控制 **sp_cdc_scan** 是否繼續執行，直到明確停止為止 (連續模式)。  
  
##### <a name="one-shot-mode"></a>一次模式  
 在一次模式中，擷取作業會要求 **sp_cdc_scan** 執行最多 *maxtrans* 次掃描，以便嘗試清空記錄檔並傳回。 存在記錄檔中 *maxtrans* 以外的任何交易將在後續掃描中處理。  
  
 一次模式會用於受到控制的測試中，因為已知要處理的交易數量，而且作業完成時自動關閉具有一些優點。 不建議您在實際執行環境中使用一次模式。 這是因為它會仰賴作業排程來管理執行掃描循環的頻率。  
  
 在一次模式中執行時，您可以使用下列計算來計算擷取作業之預期輸送量的上限 (以每秒交易數表示)：  
  
 `(maxtrans * maxscans) / number of seconds between scans`  
  
 即使掃描記錄檔和擴展變更資料表所需的時間並未與 0 完全不同，此作業的平均輸送量仍無法超過將單一掃描允許的最大交易數乘以允許的最大掃描數再除以分隔記錄檔處理的秒數所取得的值。  
  
 如果您使用一次模式來管理記錄檔掃描，記錄檔處理之間的秒數就必須受到作業排程的管制。 需要這種行為時，在連續模式中執行擷取作業是管理重新排程記錄檔掃描的較佳方式。  
  
##### <a name="continuous-mode-and-the-polling-interval"></a>連續模式和輪詢間隔  
 在連續模式中，擷取作業會要求 **sp_cdc_scan** 連續執行。 這會透過提供 maxtrans 和 maxscans，以及記錄檔處理之間秒數的值 (輪詢間隔)，讓此預存程序管理自己的等候迴圈。 在這種模式中執行時，擷取作業會維持使用中，並且在記錄檔掃描之間執行 **WAITFOR** 。  
  
> [!NOTE]  
>  當輪詢間隔的值大於 0 時，重複執行一次作業之輸送量的相同上限也會套用至連續模式中的作業。 也就是說，(*maxtrans* \* *maxscans*) 除以非零的輪詢間隔會針對擷取作業可以處理的平均交易數目放置上限。  
  
### <a name="capture-job-customization"></a>擷取作業自訂  
 您可以針對擷取作業套用其他邏輯，以便決定新的掃描是否會立即開始，或者在啟動新的掃描之前是否加上休眠，而非仰賴固定的輪詢間隔。 這項選擇可能僅僅依據當天時間，或許在尖峰活動時段強制執行非常長的休眠，甚至在當天結束時移至輪詢間隔 0 (如果完成日間處理和準備夜間執行很重要的話)。 您也可以監視擷取處理序進度，以便判斷午夜之前認可之所有交易已經掃描並儲放在變更資料表中的時間。 這會讓擷取作業結束，以便依據排程的每日重新啟動時間重新啟動。 只要將呼叫 **sp_cdc_scan** 的傳遞作業步驟取代成呼叫 **sp_cdc_scan**的使用者撰寫包裝函式，您即可透過少數額外步驟來取得高度自訂的行為。  
  
##  <a name="Cleanup"></a> 清除作業  
 本節提供有關異動資料擷取清除作業如何運作的資訊。  
  
### <a name="structure-of-the-cleanup-job"></a>清除作業的結構  
 異動資料擷取會使用保留性清除策略來管理變更資料表大小。 此清除機制包含啟用第一個資料庫資料表時建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業。 單一清除作業會處理所有資料庫變更資料表的清除，並且將相同的保留值套用至所有定義的擷取執行個體。  
  
 清除作業是透過執行無參數的預存程序 **sp_MScdc_cleanup_job**起始的。 這個預存程序一開始會從 **msdb.dbo.cdc_jobs**中擷取清除作業的設定保留和臨界值。 此保留值會用來計算變更資料表的新下限標準。 從 *cdc.lsn_time_mapping* 資料表的最大 **tran_end_time** 值中減去指定的分鐘數，以便取得表示成日期時間值的新下限標準。 然後，使用 CDC.lsn_time_mapping 資料表來將這個日期時間值轉換成對應的 **lsn** 值。 如果資料表中的多個項目共用相同的認可時間，就會選擇對應至具有最小 **lsn** 之項目的 **lsn** 成為新的下限標準。 這個 **lsn** 值會傳遞給 **sp_cdc_cleanup_change_tables** ，以便從資料庫變更資料表中移除變更資料表項目。  
  
> [!NOTE]  
>  使用最近交易之認可時間當做計算新下限標準之基礎的優點在於，它會在指定的時間內讓變更保留在變更資料表中。 即使擷取處理序正在後方執行，也會發生這種情況。 具有相同認可時間當做目前下限標準的所有項目會透過選擇具有實際下限標準之共用認可時間的最小 **lsn** ，繼續在變更資料表內部表示。  
  
 執行清除時，所有擷取執行個體的下限標準一開始是在單一交易中更新。 然後，它會嘗試從變更資料表和 cdc.lsn_time_mapping 資料表中移除已過時的項目。 可設定的臨界值會限制在任何單一陳述式中刪除的項目數。 如果無法針對任何個別的資料表執行刪除，將無法防止針對其餘資料表嘗試進行此作業。  
  
### <a name="cleanup-job-customization"></a>清除作業自訂  
 對於清除作業而言，自訂的可能性在於用來決定哪些變更資料表項目要捨棄的策略。 在傳遞的清除作業中，唯一支援的策略是以時間為基礎的策略。 在該情況下，新下限標準的計算方式是從上次處理之交易的認可時間中減去允許的保留週期。 由於基礎清除程序是以 **lsn** 而非時間為基礎，所以您可以使用任何數目的策略來決定要保留在變更資料表中的最小 **lsn** 。 其中只有某些策略是嚴格地以時間為基礎。 例如，如果需要存取變更資料表的下游處理序無法執行，用戶端的相關知識就可用來提供保全。 此外，雖然預設策略會套用相同的 **lsn** 來清除所有資料庫的變更資料表，但是您也可以呼叫基礎清除程序，以便在擷取執行個體層級進行清除。  
  
##  <a name="Monitor"></a> 監視異動資料擷取程序  
 監視異動資料擷取程序可讓您判斷變更是否正確地並且以合理的延遲寫入變更資料表。 監視也可以協助您識別可能發生的任何錯誤。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含兩個動態管理檢視，可協助您監視異動資料擷取： [sys.dm_cdc_log_scan_sessions](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md) 和 [sys.dm_cdc_errors](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md)。  
  
### <a name="identify-sessions-with-empty-result-sets"></a>識別含有空白結果集的工作階段  
 sys.dm_cdc_log_scan_sessions 中的每個資料列都代表記錄檔掃描工作階段 (除了識別碼為 0 的資料列以外)。 記錄檔掃描工作階段相當於執行一次 [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md)。 在工作階段期間，掃描可能會傳回變更或傳回空的結果。 如果結果集是空的，sys.dm_cdc_log_scan_sessions 中的 empty_scan_count 資料行就會設定為 1。 如果含有連續的空結果集 (例如擷取作業連續執行)，最後一個現有資料列中的 empty_scan_count 就會遞增。 例如，如果 sys.dm_cdc_log_scan_sessions 已經針對傳回變更的掃描包含 10 個資料列，而且資料列中含有五個空的結果，表示檢視包含 11 個資料列。 在 empty_scan_count 資料行中，最後一個資料列的值為 5。 若要判斷具有空白掃描的工作階段，請執行下列查詢：  
  
 `SELECT * from sys.dm_cdc_log_scan_sessions where empty_scan_count <> 0`  
  
### <a name="determine-latency"></a>判斷延遲  
 sys.dm_cdc_log_scan_sessions 管理檢視含有記錄每個擷取工作階段之延遲的資料行。 延遲會定義成在來源資料表上認可交易與在變更資料表上認可最後一個擷取交易之間經過的時間。 系統只會針對使用中工作階段填入 latency 資料行。 若為 empty_scan_count 資料行中的值大於 0 的工作階段，latency 資料行就會設定為 0。 下列查詢會針對最近的工作階段傳回平均延遲：  
  
 `SELECT latency FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0`  
  
 您可以使用延遲資料來判斷擷取程序處理交易的速度快慢。 當擷取程序連續執行時，這項資料便最有用。 如果擷取程序正按照排程執行，延遲可能會很高，因為在來源資料表上認可交易與按照排程時間執行的擷取程序之間存在延遲。  
  
 擷取程序效率的另一個重要量值是輸送量。 這是指每個工作階段期間每秒處理的平均命令數目。 若要判斷某個工作階段的輸送量，請將 command_count 資料行中的值除以 duration 資料行中的值。 下列查詢會針對最近的工作階段傳回平均輸送量：  
  
 `SELECT command_count/duration AS [Throughput] FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0`  
  
### <a name="use-data-collector-to-collect-sampling-data"></a>使用資料收集器來收集取樣資料  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料收集器可讓您從任何資料表或動態管理檢視中收集資料的快照集，然後建立效能資料倉儲。 當資料庫啟用異動資料擷取時，以固定間隔建立 sys.dm_cdc_log_scan_sessions 檢視和 sys.dm_cdc_errors 檢視的快照集以便之後分析會很有用。 下列程序會設定從 sys.dm_cdc_log_scan_sessions 管理檢視中收集取樣資料的資料收集器。  
  
 **設定資料收集**  
  
1.  啟用資料收集器並設定管理資料倉儲。 如需詳細資訊，請參閱 [管理資料收集](../../relational-databases/data-collection/manage-data-collection.md)。  
  
2.  執行下列程式碼來建立異動資料擷取的自訂收集器。  
  
    ```tsql  
    USE msdb;  
  
    DECLARE @schedule_uid uniqueidentifier;  
  
    -- Collect and upload data every 5 minutes  
    SELECT @schedule_uid = (  
    SELECT schedule_uid from sysschedules_localserver_view   
    WHERE name = N'CollectorSchedule_Every_5min')  
  
    DECLARE @collection_set_id int;  
  
    EXEC dbo.sp_syscollector_create_collection_set  
    @name = N' CDC Performance Data Collector',  
    @schedule_uid = @schedule_uid,          
    @collection_mode = 0,                   
    @days_until_expiration = 30,                
    @description = N'This collection set collects CDC metadata',  
    @collection_set_id = @collection_set_id output;  
  
    -- Create a collection item using statistics from   
    -- the change data capture dynamic management view.  
    DECLARE @paramters xml;  
    DECLARE @collection_item_id int;  
  
    SELECT @paramters = CONVERT(xml,   
        N'<TSQLQueryCollector>  
            <Query>  
              <Value>SELECT * FROM sys.dm_cdc_log_scan_sessions</Value>  
              <OutputTable>cdc_log_scan_data</OutputTable>  
            </Query>  
          </TSQLQueryCollector>');  
  
    EXEC dbo.sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = N'302E93D1-3424-4BE7-AA8E-84813ECF2419',  
    @name = ' CDC Performance Data Collector',  
    @frequency = 5,   
    @parameters = @paramters,  
    @collection_item_id = @collection_item_id output;  
  
    GO  
    ```  
  
3.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，展開 **[管理]**，然後展開 **[資料收集]**。 以滑鼠右鍵按一下 **[CDC 效能資料收集器]**，然後按一下 **[啟動資料收集組]**。  
  
4.  在步驟 1 中設定的資料倉儲內，找出資料表 custom_snapshots.cdc_log_scan_data。 這份資料表會提供記錄檔掃描工作階段之資料的歷程記錄快照集。 這份資料表可用於分析經過一段時間的延遲、輸送量和其他效能量值。  
  
## <a name="see-also"></a>另請參閱  
 [追蹤資料變更 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [關於異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [啟用和停用異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [使用變更資料 &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
  
