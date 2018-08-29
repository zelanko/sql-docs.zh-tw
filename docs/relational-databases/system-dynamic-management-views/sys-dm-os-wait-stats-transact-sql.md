---
title: sys.dm_os_wait_stats & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 04/23/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_wait_stats_TSQL
- dm_os_wait_stats
- sys.dm_os_wait_stats
- sys.dm_os_wait_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_wait_stats dynamic management view
ms.assetid: 568d89ed-2c96-4795-8a0c-2f3e375081da
caps.latest.revision: 111
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 253f8628a461f3d2e8ff27961e7dabfafe04d2a1
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43076738"
---
# <a name="sysdmoswaitstats-transact-sql"></a>sys.dm_os_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回執行中之執行緒所遇到之所有等候的相關資訊。 您可以使用這份彙總檢視來診斷 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的效能問題，以及特定查詢和批次的效能問題。 [sys.dm_exec_session_wait_stats &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)提供類似的工作階段的資訊。  
  
> [!NOTE] 
> 若要呼叫這個屬性從**[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或是[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]** ，使用名稱**sys.dm_pdw_nodes_os_wait_stats**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|wait_type|**nvarchar(60)**|等候類型的名稱。 如需詳細資訊，請參閱 <<c0> [ 等候的類型](#WaitTypes)稍後在本主題中。|  
|waiting_tasks_count|**bigint**|這個等候類型的等候次數。 這個計數器是從每次開始等候時逐量遞增計算。|  
|wait_time_ms|**bigint**|這個等候類型的總等候時間 (以毫秒為單位)。 這個時間包括 signal_wait_time_ms 在內。|  
|max_wait_time_ms|**bigint**|這個等候類型的等候時間上限。|  
|signal_wait_time_ms|**bigint**|從等候執行緒接獲訊號到開始執行的時間。|  
|pdw_node_id|**int**|這個分佈是在節點的識別碼。 <br/> **適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] |  
  
## <a name="permissions"></a>Permissions

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   

##  <a name="WaitTypes"></a> 等候的類型  
 **資源等候**工作者要求存取無法使用，因為正由某些其他背景工作的資源，或尚無法使用的資源時，就會發生資源等候。 鎖定、閂鎖、網路和磁碟 I/O 等候，都是資源等候的範例。 鎖定和閂鎖等候是同步處理物件的等候。  
  
**佇列等候**  
 佇列等候發生在工作者因為等候指派工作而閒置時。 佇列等候大部分都是在進行系統背景工作 (例如，監視死結和刪除記錄清除工作) 時發生。 這些工作會等候工作要求被置於工作佇列。 即使沒有新的封包置於佇列中，佇列等候也可能會定期變成使用中狀態。  
  
 **外部等候**  
 外部等候是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作者正在等候外部事件 (例如，擴充預存程序呼叫或連結伺服器查詢) 完成時發生。 記住，當您診斷封鎖問題時，外部等候不會一直暗示工作者正在閒置，因為工作者可能很積極的在執行一些外部程式碼。  
  
 `sys.dm_os_wait_stats` 顯示已完成等候的時間。 此動態管理檢視不會顯示目前的等候。  
  
 在下列任何一種情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作者執行緒都不算是在等候中：  
  
-   資源可以使用。  
  
-   佇列不是空的。  
  
-   外部處理序完成。  
  
 雖然執行緒已經不在等候中，執行緒也不必立即開始執行。 因為這類執行緒會先置於可執行之工作者的佇列上，而且必須等候排程器執行某個配量才行。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]等候時間計數器**bigint**值，並因此不太一樣計數器換用為在舊版的對等計數器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 在執行查詢時，特定類型的等候時間可以指出查詢中的瓶頸或拋錨點。 同樣地，等候時間很長或伺服器等候計數很大，也代表伺服器執行個體中互動查詢互動的瓶頸或熱點。 例如，鎖定等候表示查詢在競爭資料；資料頁 IO 閂鎖等候表示 IO 回應時間很慢；資料頁閂鎖更新等候表示檔案配置不正確。  
  
 您可以執行下列命令，重設這份動態管理檢視的內容：  
  
```sql  
DBCC SQLPERF ('sys.dm_os_wait_stats', CLEAR);  
GO  
```  
  
這個命令會將所有的計數器重設為 0。  
  
> [!NOTE]
> 這些統計資料在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新啟動之後都不會保存下來，而且所有的資料都是從上次統計資料重設或伺服器啟動之後開始累加計算。  
  
 下表列出工作會遇到的等候類型。  

|型別 |描述| 
|-------------------------- |--------------------------| 
|ABR |僅供參考之用。 不支援。 我們無法保證未來的相容性。| | 
|AM_INDBUILD_ALLOCATION |TBD <br />**適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|AM_SCHEMAMGR_UNSHARED_CACHE |TBD <br />**適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ASSEMBLY_FILTER_HASHTABLE |TBD <br />**適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ASSEMBLY_LOAD |在組件載入的獨佔存取期間發生。| 
|ASYNC_DISKPOOL_LOCK |在同步處理執行建立檔案，或者檔案初始化等工作的平行執行緒時發生。| 
|ASYNC_IO_COMPLETION |在工作等候 I/O 完成時發生。| 
|ASYNC_NETWORK_IO |當工作被封鎖在網路後面時，進行網路寫入就會發生這種情形。 請確認用戶端正在處理來自伺服器的資料。| 
|ASYNC_OP_COMPLETION |TBD <br />**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ASYNC_OP_CONTEXT_READ |TBD <br />**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ASYNC_OP_CONTEXT_WRITE |TBD <br />**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ASYNC_SOCKETDUP_IO |TBD <br />**適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|AUDIT_GROUPCACHE_LOCK |當控制特殊快取之存取權的鎖定上存在等候時發生。 此快取包含哪些稽核要用來稽核每個稽核動作群組的相關資訊。| 
|AUDIT_LOGINCACHE_LOCK |當控制特殊快取之存取權的鎖定上存在等候時發生。 此快取包含哪些稽核要用來稽核登入稽核動作群組的相關資訊。| 
|AUDIT_ON_DEMAND_TARGET_LOCK |當用來確保稽核相關「擴充事件」目標之單一初始化的鎖定上存在等候時發生。| 
|AUDIT_XE_SESSION_MGR |當用來同步處理稽核相關「擴充事件」工作階段之啟動和停止的鎖定上存在等候時發生。| 
|BACKUP |當工作被當做備份處理的一部分而加以封鎖時發生。| 
|BACKUP_OPERATOR |在工作等候磁帶掛載時發生。 若要檢視磁帶狀態，請查詢 sys.dm_io_backup_tapes。 如果掛載作業沒有暫止，這個等候類型可能就表示磁帶機發生硬體問題。| 
|BACKUPBUFFER |當備份工作正在等候資料，或者等候儲存資料的緩衝區時發生。 除非當工作正在等候磁帶掛載，否則這個類型並非標準類型。| 
|BACKUPIO |當備份工作正在等候資料，或者等候儲存資料的緩衝區時發生。 除非當工作正在等候磁帶掛載，否則這個類型並非標準類型。| 
|BACKUPTHREAD |在工作等候備份工作完成時發生。 等候時間可能會很長，從幾分鐘到數小時都可能。 如果等候的工作是在 I/O 處理序中，這個類型就不表示發生問題。| 
|BAD_PAGE_PROCESS |當背景可疑頁面記錄器想要避免執行間隔超過每 5 秒一次時發生。 可疑頁面過多將導致記錄器經常執行。| 
|BLOB_METADATA |TBD <br />**適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BMPALLOCATION |TBD <br />**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BMPBUILD |TBD <br />**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BMPREPARTITION |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BMPREPLICATION |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BPSORT |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_CONNECTION_RECEIVE_TASK |在連接端點上等候接收訊息的存取權時發生。 端點的接收存取是序列化的。| 
|BROKER_DISPATCHER |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_ENDPOINT_STATE_MUTEX |若要存取的狀態，Service Broker 連接端點發生爭用時，就會發生。 存取變更的狀態是序列化的。| 
|BROKER_EVENTHANDLER |當工作在等候中的 Service broker 的主要事件處理常式時，就會發生。 發生的時間相當短暫。| 
|BROKER_FORWARDER |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_INIT |初始化每個作用中的資料庫中的 Service Broker 時，就會發生。 這種情況不常發生。| 
|BROKER_MASTERSTART |當工作在等候啟動 Service Broker 的主要事件處理常式，就會發生。 發生的時間相當短暫。| 
|BROKER_RECEIVE_WAITFOR |當 RECEIVE WAITFOR 在等候時發生。 這可能表示，任何訊息已準備好要在佇列中接收或鎖定爭用的情況會使其無法接收來自佇列的訊息。| 
|BROKER_REGISTERALLENDPOINTS |在 Service Broker 連接端點初始化時發生。 發生的時間相當短暫。| 
|BROKER_SERVICE |更新或重新設定優先權與目標服務相關聯的 Service Broker 目的地清單時，就會發生。| 
|BROKER_SHUTDOWN |Service Broker 的計劃的關機時，就會發生。 即使發生，時間也相當短暫。| 
|BROKER_START |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_TASK_SHUTDOWN |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_TASK_STOP |當 Service Broker 佇列工作處理常式嘗試關閉工作時，就會發生。 狀態檢查會序化列，而且必須事先處於執行中狀態。| 
|BROKER_TASK_SUBMIT |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_TO_FLUSH |Service Broker 延遲清除器清除記憶體中傳輸物件工作資料表時，就會發生。| 
|BROKER_TRANSMISSION_OBJECT |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_TRANSMISSION_TABLE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_TRANSMISSION_WORK |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|BROKER_TRANSMITTER |當 Service Broker 傳輸器正在等候工作時，就會發生。| 
|BUILTIN_HASHKEY_MUTEX |可能在啟動執行個體之後，而內部資料結構正在初始化時發生。 資料結構初始化之後就不會再次發生。| 
|CHANGE_TRACKING_WAITFORCHANGES |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CHECK_PRINT_RECORD |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|CHECK_SCANNER_MUTEX |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CHECK_TABLES_INITIALIZATION |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CHECK_TABLES_SINGLE_SCAN |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CHECK_TABLES_THREAD_BARRIER |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CHECKPOINT_QUEUE |當檢查點工作在等候下一個檢查點要求時發生。| 
|CHKPT |在伺服器啟動時發生，目的在告知檢查點執行緒，它可以啟動了。| 
|CLEAR_DB |在變更資料庫狀態的作業期間發生，例如開啟或關閉資料庫。| 
|CLR_AUTO_EVENT |當工作目前在執行 Common Language Runtime (CLR) 執行，以及在等候特定自動事件起始時發生。 等候時間長是正常情況，並不表示發生任何問題。| 
|CLR_CRST |當工作目前正在執行 CLR 執行，以及正在等候進入目前正被另一個工作使用中之工作的重要區段時發生。| 
|CLR_JOIN |當工作目前正在執行 CLR 執行，以及正在等候另一個工作結束時發生。 這個等候狀態是在工作之間有聯結時發生。| 
|CLR_MANUAL_EVENT |當工作目前正在執行 CLR 執行，以及正在等候特定的手動事件起始時發生。| 
|CLR_MEMORY_SPY |在用來記錄來自 CLR 之所有虛擬記憶體配置的資料結構等候取得鎖定期間發生。 如果存在平行存取，資料結構就會鎖定，以便維持其完整性。| 
|CLR_MONITOR |當工作目前正在執行 CLR 執行，以及正在等候取得監視器鎖定時發生。| 
|CLR_RWLOCK_READER |當工作目前正在執行 CLR 執行，以及正在等候讀取器鎖定時發生。| 
|CLR_RWLOCK_WRITER |當工作目前正在執行 CLR 執行，以及正在等候寫入器鎖定時發生。| 
|CLR_SEMAPHORE |當工作目前正在執行 CLR 執行，以及正在等候信號時發生。| 
|CLR_TASK_START |在等候 CLR 工作完成啟動時發生。| 
|CLRHOST_STATE_ACCESS |在等候取得 CLR 主控資料結構之獨佔存取權的情況下發生。 這種等候類型會在設定或終止 CLR 執行階段時發生。| 
|CMEMPARTITIONED |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CMEMTHREAD |當工作在安全執行緒記憶體物件待命時發生。 如果有多個工作嘗試從同一個記憶體物件配置記憶體而導致競爭情形時，等候時間可能會增加。| 
|COLUMNSTORE_BUILD_THROTTLE |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|COLUMNSTORE_COLUMNDATASET_SESSION_LIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|COMMIT_TABLE |TBD| 
|CONNECTION_ENDPOINT_LOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|COUNTRECOVERYMGR |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CREATE_DATINISERVICE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|CXCONSUMER |當取用者執行緒等候要傳送的資料列產生者執行緒會發生平行查詢計畫。 這是正常的平行查詢執行。 <br /> **適用於**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開頭[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] cu3 開始)， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|
|CXPACKET  |當同步處理查詢處理器交換重複，並產生和取用資料列時，會發生與平行查詢計畫。 如果等候時間過長，而且無法透過微調查詢 (例如加入索引) 來縮短，請考慮調整平行處理原則的成本臨界值，或降低平行處理原則的程度。<br /> **注意：** 開頭[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3，和[!INCLUDE[ssSDS](../../includes/sssds-md.md)]，同步處理查詢處理器交換重複，並產生取用者執行緒的資料列，只是指 CXPACKET。 取用者執行緒會分開追蹤在 CXCONSUMER 等候類型。| 
|CXROWSET_SYNC |在平行範圍掃描期間發生。| 
|DAC_INIT |當專用管理員連接正在初始化時發生。| 
|DBCC_SCALE_OUT_EXPR_CACHE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DBMIRROR_DBM_EVENT |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|DBMIRROR_DBM_MUTEX |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|DBMIRROR_EVENTS_QUEUE |當資料庫鏡像在等候處理事件時發生。| 
|DBMIRROR_SEND  |當工作在網路層等候通訊積存清除，以傳送訊息時發生。 它指出通訊層已經開始多載，並影響到資料庫鏡像資料輸送量。| 
|DBMIRROR_WORKER_QUEUE |指出資料庫鏡像工作者工作正在等候其他工作。| 
|DBMIRRORING_CMD  |當工作在等候記錄排清到磁碟時發生。 這個等候狀態預期會保留一段很長的時間。| 
|DBSEEDING_FLOWCONTROL |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DBSEEDING_OPERATION |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DEADLOCK_ENUM_MUTEX  |當死結監視器和 sys.dm_os_waiting_tasks 嘗試確定到 SQL Server 沒有在執行多個死結搜尋一次。| 
|DEADLOCK_TASK_SEARCH  |在此資源上的等候時間如果很長，表示伺服器正在 sys.dm_os_waiting_tasks 之上執行查詢，而這些查詢則造成死結監視器無法執行死結搜尋。 只有死結監視器才會使用這種等候類型。 在 sys.dm_os_waiting_tasks 之上的查詢會使用 DEADLOCK_ENUM_MUTEX。| 
|DEBUG |TRANSACT-SQL 和 CLR 偵錯執行內部同步處理期間發生。| 
|DIRECTLOGCONSUMER_LIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DIRTY_PAGE_POLL |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DIRTY_PAGE_SYNC |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DIRTY_PAGE_TABLE_LOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DISABLE_VERSIONING |當 SQL Server 輪詢版本交易管理員，以查看最早的使用中交易的時間戳記是否晚於狀態開啟改變的時間戳記時，就會發生。 如果是這樣，則表示所有在 ALTER DATABASE 陳述式執行之前所啟動的快照集交易，已經全部完成了。 SQL Server 停用版本控制使用 ALTER DATABASE 陳述式時，會使用這個等候狀態。| 
|DISKIO_SUSPEND |當外部備份在使用中時，工作正在等候存取檔案時發生。 這是針對每個等候中的使用者處理序所報告。 如果超過每個使用者處理序五次時，可能表示外部備份花了太多時間才完成。| 
|DISPATCHER_PRIORITY_QUEUE_SEMAPHORE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DISPATCHER_QUEUE_SEMAPHORE |當發送器集區的執行緒正在等候處理其他工作時發生。 這種等候類型的等候時間應該會在發送器閒置時增加。| 
|DLL_LOADING_MUTEX |在等候 XML 剖析器 DLL 載入時發生一次。| 
|DPT_ENTRY_LOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DROP_DATABASE_TIMER_TASK |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DROPTEMP |卸除暫存物件時，如果前一次的嘗試失敗，就會在兩次嘗試之間發生這種等候類型。 等候持續時間將以指數方式，隨著每一次的卸除嘗試失敗而增加。| 
|DTC |當工作在服務管理狀態轉移所用的事件時發生。 此狀態可控制當 SQL Server 接收 MS DTC 服務已變成無法使用的通知之後，就會發生的 Microsoft Distributed Transaction Coordinator (MS DTC) 交易復原。| 
|DTC_ABORT_REQUEST  |當工作階段在等候接收 MS DTC 交易的擁有權時，在 MS DTC 工作者工作階段發生。 MS DTC 擁有交易之後，工作階段就可以回復該交易。 通常，工作階段會等候另一個使用該交易的工作階段。| 
|DTC_RESOLVE  |當復原工作在等候跨資料庫交易中的 master 資料庫，讓工作得以查詢交易結果時發生。| 
|DTC_STATE  |當工作在保護您對內部 MS DTC 全域狀態物件所做變更的事件待命時發生。 這個狀態的保留時間很短。| 
|DTC_TMDOWN_REQUEST |在 SQL Server 時接收通知，MS DTC 服務不提供 MS DTC 工作者工作階段，就會發生。 首先，工作者會等候 MS DTC 復原處理序啟動。 接著，工作者會等候取得他所處理的分散式交易結果。 除非與 MS DTC 服務的連接已經重新建立，否則這項作業會繼續進行。| 
|DTC_WAITFOR_OUTCOME  |當復原工作在等候 MS DTC 開始解析準備交易時發生。| 
|DTCNEW_ENLIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DTCNEW_PREPARE |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DTCNEW_RECOVERY |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DTCNEW_TM |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DTCNEW_TRANSACTION_ENLISTMENT |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DTCPNTSYNC |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|DUMP_LOG_COORDINATOR  |當主要工作正在等候子工作產生資料時發生。 這個狀態通常不會發生。 如果等候時間很長，就表示發生了非預期的封鎖。 您最好調查一下子工作。| 
|DUMP_LOG_COORDINATOR_QUEUE |TBD| 
|DUMPTRIGGER |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|EC |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|EE_PMOLOCK |在陳述式執行期間同步處理某些類型的記憶體配置時發生。| 
|EE_SPECPROC_MAP_INIT |在同步處理內部程序雜湊表的建立時發生。 期間初次存取雜湊資料表的 SQL Server 執行個體啟動之後，才會發生這種等候。| 
|ENABLE_EMPTY_VERSIONING |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ENABLE_VERSIONING |SQL Server 等候此完成後，宣告資料庫可以轉移到允許狀態的快照集隔離的資料庫中的所有更新交易時發生。 SQL Server 使用 ALTER DATABASE 陳述式啟用快照集隔離時，會使用此狀態。| 
|ERROR_REPORTING_MANAGER |在同步處理多個並行錯誤記錄檔的初始化時發生。| 
|EXCHANGE  |在平行查詢期間同步處理查詢處理器交換重複時發生。| 
|EXECSYNC  |平行查詢期間在與交換重複無關之區域的查詢處理器中進行同步處理時發生。 這類區域的範例包括點陣圖、大型二進位物件 (LOB) 和多工緩衝處理重複。 LOB 可能會經常使用這個等候狀態。| 
|EXECUTION_PIPE_EVENT_INTERNAL |在透過連接內容傳送的批次執行產生者與取用者部分之間同步處理期間發生。| 
|EXTERNAL_RG_UPDATE |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|EXTERNAL_SCRIPT_NETWORK_IO |TBD <br /> **適用於**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]到目前。| 
|EXTERNAL_SCRIPT_PREPARE_SERVICE |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|EXTERNAL_SCRIPT_SHUTDOWN |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|EXTERNAL_WAIT_ON_LAUNCHER， |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FABRIC_HADR_TRANSPORT_CONNECTION |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FABRIC_REPLICA_CONTROLLER_LIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FABRIC_REPLICA_CONTROLLER_STATE_AND_CONFIG |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FABRIC_REPLICA_PUBLISHER_EVENT_PUBLISH |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FABRIC_REPLICA_PUBLISHER_SUBSCRIBER_LIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FABRIC_WAIT_FOR_BUILD_REPLICA_EVENT_PROCESSING |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FAILPOINT |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|FCB_REPLICA_READ  |在同步處理快照集 (或 DBCC 所建立的暫時快照集) 疏鬆檔案的讀取作業時發生。| 
|FCB_REPLICA_WRITE  |在同步處理將資料頁發送或提取到快照集 (或 DBCC 所建立的暫時快照集) 疏鬆檔案時發生。| 
|FEATURE_SWITCHES_UPDATE |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_DB_KILL_FLAG |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_DB_LIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_FCB |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_FCB_FIND |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_FCB_PARENT |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_FCB_RELEASE_CACHED_ENTRIES |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_FCB_STATE |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_FILEOBJECT |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NSO_TABLE_LIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_NTFS_STORE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_RECOVERY |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_RSFX_COMM |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_RSFX_WAIT_FOR_MEMORY |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_STARTUP_SHUTDOWN |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_STORE_DB |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_STORE_ROWSET_LIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FFT_STORE_TABLE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILE_VALIDATION_THREADS |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILESTREAM_CACHE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILESTREAM_CHUNKER |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILESTREAM_CHUNKER_INIT |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILESTREAM_FCB |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILESTREAM_FILE_OBJECT |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILESTREAM_WORKITEM_QUEUE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FILETABLE_SHUTDOWN |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FOREIGN_REDO |TBD <br /> **適用於**:[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]到目前。| 
|FORWARDER_TRANSITION |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FS_FC_RWLOCK |當 FILESTREAM 記憶體回收行程等候進行下列其中一項作業時發生：| 
|FS_GARBAGE_COLLECTOR_SHUTDOWN |當 FILESTREAM 記憶體回收行程正在等候清除工作完成時發生。| 
|FS_HEADER_RWLOCK |當系統等候取得 FILESTREAM 資料容器之 FILESTREAM 標頭的存取權來讀取或更新 FILESTREAM 標頭檔 (Filestream.hdr) 內容時發生。| 
|FS_LOGTRUNC_RWLOCK |當系統等候取得 FILESTREAM 記錄截斷的存取權來進行下列其中一項作業時發生：| 
|FSA_FORCE_OWN_XACT |當 FILESTREAM 檔案 I/O 作業需要繫結至相關聯的交易，但是此交易目前由其他工作階段所擁有時發生。| 
|FSAGENT |當 FILESTREAM 檔案 I/O 作業正在等候其他檔案 I/O 作業所使用的 FILESTREAM 代理程式資源時發生。| 
|FSTR_CONFIG_MUTEX |當系統等候其他 FILESTREAM 功能重新設定完成時發生。| 
|FSTR_CONFIG_RWLOCK |當系統等候序列化 FILESTREAM 組態參數的存取權時發生。| 
|FT_COMPROWSET_RWLOCK |全文檢索正在等候片段中繼資料作業。 記載僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|FT_IFTS_RWLOCK |全文檢索正在等候內部的同步處理。 記載僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|FT_IFTS_SCHEDULER_IDLE_WAIT |全文檢索排程器睡眠等候類型。 排程器閒置中。| 
|FT_IFTSHC_MUTEX |全文檢索正在等候 fdhost 控制項作業。 記載僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|FT_IFTSISM_MUTEX |全文檢索正在等候通訊作業。 記載僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|FT_MASTER_MERGE |全文檢索正在等候主要合併作業。 記載僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|FT_MASTER_MERGE_COORDINATOR |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FT_METADATA_MUTEX |記載僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|FT_PROPERTYLIST_CACHE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|FT_RESTART_CRAWL |在全文檢索搜耙必須從最後一個已知的恰當起點重新啟動以便從暫時性失敗中復原時發生。 等候可讓目前正在處理該母體擴展的工作者工作得以完成或結束目前的步驟。| 
|FULLTEXT GATHERER |在同步處理全文檢索作業時發生。| 
|GDMA_GET_RESOURCE_OWNER |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GHOSTCLEANUP_UPDATE_STATS |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GHOSTCLEANUPSYNCMGR |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GLOBAL_QUERY_CANCEL |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GLOBAL_QUERY_CLOSE |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GLOBAL_QUERY_CONSUMER |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GLOBAL_QUERY_PRODUCER |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GLOBAL_TRAN_CREATE |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GLOBAL_TRAN_UCS_SESSION |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|GUARDIAN |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|HADR_AG_MUTEX |當 Always On DDL 陳述式或 Windows Server 容錯移轉叢集命令等候可用性群組組態的獨佔讀取/寫入存取，就會發生。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_AR_CRITICAL_SECTION_ENTRY |當 Always On DDL 陳述式或 Windows Server 容錯移轉叢集命令等候相關聯的可用性群組的本機複本的執行階段狀態的獨佔讀取/寫入存取，就會發生。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_AR_MANAGER_MUTEX |在可用性複本關閉等候啟動完成或者可用性複本啟動等候關閉完成時發生。 僅供內部使用。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_AR_UNLOAD_COMPLETED |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_ARCONTROLLER_NOTIFICATIONS_SUBSCRIBER_LIST |可用性複本事件 (例如狀態變更或組態變更) 的發行者正在等候事件訂閱者清單的獨佔讀取/寫入存取權。 僅供內部使用。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_BACKUP_BULK_LOCK |Alwayson 主要資料庫收到次要資料庫的備份要求而且正在等候背景執行緒完成處理上取得或釋放 BulkOp 鎖定要求。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_BACKUP_QUEUE |Alwayson 主要資料庫的備份背景執行緒正在等候來自次要資料庫的新工作要求。 （一般而言，這會發生當主要資料庫保存 BulkOp 記錄而且正在等候次要資料庫，以指出主要資料庫可以釋放鎖定時）。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_CLUSAPI_CALL |SQL Server 執行緒正在等待從非先佔式模式 （SQL server 排程） 切換到先佔式模式 （由作業系統排程） 才能叫用 Windows Server 容錯移轉叢集 Api。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_COMPRESSED_CACHE_SYNC |等候用來避免重複壓縮傳送至多個次要資料庫的記錄檔區塊的壓縮記錄檔區塊快取的存取。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_CONNECTIVITY_INFO |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DATABASE_FLOW_CONTROL |在已達佇列訊息的數目上限時，等候要傳送至夥伴的訊息。 表示記錄掃描的執行速度比網路傳送的速度要快。 這是個問題，只有當網路傳送會比預期還要慢。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DATABASE_VERSIONING_STATE |在 Alwayson 次要資料庫的版本控制狀態變更時，就會發生。 這項等候是針對內部資料結構，通常是非常短暫，不會直接影響的資料存取。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DATABASE_WAIT_FOR_RECOVERY |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DATABASE_WAIT_FOR_RESTART |等候 Always On 可用性群組控制下重新啟動資料庫。 在正常情況下，這並非客戶問題因為等候此處預期會發生。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING |Always on 可用性群組等候執行中之次要複本啟用讀取工作負載時的所有交易的認可或回復時，會封鎖資料列版本設定的可讀取次要資料庫中的物件查詢。 這種等候類型會保證資料列版本可供查詢，以在快照隔離下執行之前。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DB_COMMAND |等候交談的訊息 （而非採用的另一端，使用 Alwayson 交談訊息基礎結構的明確回應） 的回應。 有多種不同的訊息類型會使用這種等候類型。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DB_OP_COMPLETION_SYNC |等候交談的訊息 （而非採用的另一端，使用 Alwayson 交談訊息基礎結構的明確回應） 的回應。 有多種不同的訊息類型會使用這種等候類型。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DB_OP_START_SYNC |Always On DDL 陳述式或 Windows Server 容錯移轉叢集命令正在等候可用性資料庫，其執行階段狀態的序列化存取。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DBR_SUBSCRIBER |可用性複本事件 (例如狀態變更或組態變更) 的發行者正在等候對應至可用性資料庫之事件訂閱者執行階段狀態的獨佔讀取/寫入存取權。 僅供內部使用。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DBR_SUBSCRIBER_FILTER_LIST |可用性複本事件 (例如狀態變更或組態變更) 的發行者正在等候對應至可用性資料庫之事件訂閱者清單的獨佔讀取/寫入存取權。 僅供內部使用。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DBSEEDING |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DBSEEDING_LIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_DBSTATECHANGE_SYNC |更新資料庫複本的內部狀態的並行控制等候。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FABRIC_CALLBACK |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_BLOCK_FLUSH |FILESTREAM Alwayson 傳輸管理員正在等候，直到處理記錄檔區塊的完成。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_FILE_CLOSE |FILESTREAM Alwayson 傳輸管理員正在等候，直到下一個 FILESTREAM 檔案處理完成，而且其控制代碼已關閉。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_FILE_REQUEST |Always On 次要複本正在等候主要複本將傳送所有要求的 FILESTREAM 檔案期間復原。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_IOMGR |FILESTREAM Alwayson 傳輸管理員正在等候 R/W 鎖定，以便啟動或關機期間保護 FILESTREAM Alwayson 上 I/O 管理員。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_IOMGR_IOCOMPLETION |FILESTREAM Alwayson 上 I/O 管理員正在等候 I/O 完成。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_MANAGER |FILESTREAM Alwayson 傳輸管理員正在等候 R/W 鎖定，啟動或關機期間保護 FILESTREAM Alwayson 傳輸管理員。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_FILESTREAM_PREPROC |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_GROUP_COMMIT |交易認可處理正在等候允許群組認可，以便將多個認可記錄檔記錄放入單一記錄檔區塊中。 這項等候是最佳化記錄 I/O 的預期的狀況、 擷取並傳送作業。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_LOGCAPTURE_SYNC |有關建立或終結掃描時記錄擷取或套用物件的並行控制。 當夥伴變更狀態 」 或 「 連接 」 狀態時，這會是預期的等候。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_LOGCAPTURE_WAIT |等候記錄檔記錄變成可用。 如果讀取不在快取中的記錄，等候連接產生新的記錄檔記錄或 I/O 完成時就可能會發生這種狀況。 這是預期的等候，如果記錄檔掃描已趕上記錄結尾，或正在從磁碟讀取。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_LOGPROGRESS_SYNC |更新資料庫複本的記錄進度狀態時，並行控制等候。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_NOTIFICATION_DEQUEUE |處理 Windows Server 容錯移轉叢集通知的背景工作正在等候下一個通知。 僅供內部使用。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_NOTIFICATION_WORKER_EXCLUSIVE_ACCESS |Always On 可用性複本管理員正在等候處理 Windows Server 容錯移轉叢集通知的背景工作的執行階段狀態的序列化存取。 僅供內部使用。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_NOTIFICATION_WORKER_STARTUP_SYNC |背景工作正在等候處理 Windows Server 容錯移轉叢集通知的背景工作啟動完成。 僅供內部使用。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_NOTIFICATION_WORKER_TERMINATION_SYNC |背景工作正在等候處理 Windows Server 容錯移轉叢集通知的背景工作終止。 僅供內部使用。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_PARTNER_SYNC |協力廠商清單上的並行控制等候。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_READ_ALL_NETWORKS |等候取得 WSFC 網路清單的讀取或寫入存取權。 僅供內部使用。 請注意： 引擎會保留一份 WSFC 網路使用動態管理檢視 （例如 sys.dm_hadr_cluster_networks) 中，或驗證一律在 TRANSACT-SQL 陳述式參考 WSFC 網路資訊。 這份清單會更新在引擎啟動時，WSFC 相關通知，以及內部 Alwayson 重新啟動 （例如遺失及以重新取得 WSFC 仲裁）。 當該清單的更新正在進行時，通常會封鎖工作。 、 <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_RECOVERY_WAIT_FOR_CONNECTION |等候次要資料庫在執行復原之前連接到主要資料庫。 這是預期的等候，可能會延長慢而無法建立連線到主要複本是否。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_RECOVERY_WAIT_FOR_UNDO |資料庫復原正在等候次要資料庫完成還原和初始化階段，以便讓它返回與主要資料庫相同的記錄點。 在容錯移轉之後，這可以是預期的等候。復原可以透過 Windows 系統監視器 (perfmon.exe) 和動態管理檢視中追蹤進度。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_REPLICAINFO_SYNC |若要更新目前複本狀態的並行控制等候。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SEEDING_CANCELLATION |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SEEDING_FILE_LIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SEEDING_LIMIT_BACKUPS |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SEEDING_SYNC_COMPLETION |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SEEDING_TIMEOUT_TASK |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SEEDING_WAIT_FOR_COMPLETION |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SYNC_COMMIT |等候已同步處理之次要資料庫的交易認可處理強行寫入記錄。 Transaction Delay 效能計數器也會反映這項等候。 這種等候類型應該同步處理可用性群組，並指出傳送、 寫入及認可到次要資料庫的記錄檔的時間。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_SYNCHRONIZING_THROTTLE |等候交易認可處理允許同步處理中的次要資料庫趕上主要記錄結尾，以便轉換成已同步處理的狀態。 這是預期的等候次要資料庫正在趕上時。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_TDS_LISTENER_SYNC |內部 Alwayson 系統或 WSFC 叢集將會在接聽程式會啟動或停止要求。 這項要求的處理方式一律為非同步，而且具有移除重複要求的機制。 此外，這個處理序有時候會由於組態變更而暫停。 與此接聽程式同步處理機制相關的所有等候都會使用此等候類型。 僅供內部使用。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_TDS_LISTENER_SYNC_PROCESSING |使用此選項，需要啟動及/或停止 anavailability 群組接聽程式的一律在 TRANSACT-SQL 陳述式的結尾。 啟動/停止作業會以非同步方式完成，因為使用者執行緒會封鎖直到稱為接聽程式的情況下，使用這種等候類型。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_THROTTLE_LOG_RATE_GOVERNOR |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_THROTTLE_LOG_RATE_LOG_SIZE |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_THROTTLE_LOG_RATE_SEEDING |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_THROTTLE_LOG_RATE_SEND_RECV_QUEUE_SIZE |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_TIMER_TASK |等候取得計時器工作物件的鎖定，而且也會用於工作執行間隔的實際等候。 比方說，工作執行之後執行一次，每隔 10 秒時，Alwayson 可用性群組會等候大約 10 秒重新排定工作，並等候此列出是為了。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_TRANSPORT_DBRLIST |等候傳輸層之資料庫複本清單的存取權。 用於授與其存取權的執行緒同步鎖定。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_TRANSPORT_FLOW_CONTROL |等候時未完成未認可 Alwayson 訊息數目超過輸出流程控制臨界值。 這是根據可用性複本-複本 （不在資料庫為基礎）。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_TRANSPORT_SESSION |Always On 可用性群組正在等候變更或存取基礎傳輸狀態。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_WORK_POOL |Always On 可用性群組背景工作的工作物件上的並行控制等候。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_WORK_QUEUE |Always On 可用性群組背景工作者執行緒正在等候指派新的工作。 這是預期的等候時準備就緒的工作者等候新工作，也就是正常的狀態。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HADR_XRF_STACK_ACCESS |存取 （查閱、 加入和刪除） Alwayson 可用性資料庫的擴充的復原分岔堆疊。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HCCO_CACHE |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HK_RESTORE_FILEMAP |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HKCS_PARALLEL_MIGRATION |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HKCS_PARALLEL_RECOVERY |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HTBUILD |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HTDELETE |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HTMEMO |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HTREINIT |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HTREPARTITION |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|HTTP_ENUMERATION  |在啟動以列舉 HTTP 端點來啟動 HTTP 時發生。| 
|HTTP_START |在連接等候 HTTP 完成初始化時發生。| 
|HTTP_STORAGE_CONNECTION |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|IMPPROV_IOWAIT |SQL Server 等候大量載入 I/O 完成時發生。| 
|INSTANCE_LOG_RATE_GOVERNOR |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|INTERNAL_TESTING |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|IO_AUDIT_MUTEX  |在同步處理追蹤事件緩衝區時發生。| 
|IO_COMPLETION |在等候 I/O 作業完成時發生。 這種等候類型通常代表非資料頁面 I/O。 資料頁面 I/O 完成等候會顯示為 PAGEIOLATCH\_ \*等候。| 
|IO_QUEUE_LIMIT |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|IO_RETRY |當讀取或寫入磁碟等 I/O 作業由於資源不足而失敗，然後重試時發生。| 
|IOAFF_RANGE_QUEUE |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|KSOURCE_WAKEUP |供服務控制工作在等候來自服務控制管理員的要求時使用。 等候時間長是正常情況，並不表示發生任何問題。| 
|KTM_ENLISTMENT |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|KTM_RECOVERY_MANAGER |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|KTM_RECOVERY_RESOLUTION |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|LATCH_DT  |在等候 DT (終結) 閂鎖時發生。 其中不包括緩衝區閂鎖或交易標示閂鎖。 閂鎖的清單\_\*等候是 sys.dm_os_latch_stats 中。 請注意，sys.dm_os_latch_stats 會將 LATCH_NL、LATCH_SH、LATCH_UP、LATCH_EX 和 LATCH_DT 等候分組在一起。| 
|LATCH_EX  |在等候 EX (獨佔) 閂鎖時發生。 其中不包括緩衝區閂鎖或交易標示閂鎖。 閂鎖的清單\_\*等候是 sys.dm_os_latch_stats 中。 請注意，sys.dm_os_latch_stats 會將 LATCH_NL、LATCH_SH、LATCH_UP、LATCH_EX 和 LATCH_DT 等候分組在一起。| 
|LATCH_KP  |在等候 KP (保留) 閂鎖時發生。 其中不包括緩衝區閂鎖或交易標示閂鎖。 閂鎖的清單\_\*等候是 sys.dm_os_latch_stats 中。 請注意，sys.dm_os_latch_stats 會將 LATCH_NL、LATCH_SH、LATCH_UP、LATCH_EX 和 LATCH_DT 等候分組在一起。| 
|LATCH_NL  |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|LATCH_SH  |在等候 SH (共用) 閂鎖時發生。 其中不包括緩衝區閂鎖或交易標示閂鎖。 閂鎖的清單\_\*等候是 sys.dm_os_latch_stats 中。 請注意，sys.dm_os_latch_stats 會將 LATCH_NL、LATCH_SH、LATCH_UP、LATCH_EX 和 LATCH_DT 等候分組在一起。| 
|LATCH_UP  |在等候 UP (更新) 閂鎖時發生。 其中不包括緩衝區閂鎖或交易標示閂鎖。 閂鎖的清單\_\*等候是 sys.dm_os_latch_stats 中。 請注意，sys.dm_os_latch_stats 會將 LATCH_NL、LATCH_SH、LATCH_UP、LATCH_EX 和 LATCH_DT 等候分組在一起。| 
|LAZYWRITER_SLEEP  |在延遲寫入器工作暫止時發生。 這是等候中的背景工作所花的時間。 如果您要尋找使用者拋錨點，就不要考慮這個狀態。| 
|LCK_M_BU  |當工作在等候取得大量更新 (BU) 鎖定時發生。| 
|LCK_M_BU_ABORT_BLOCKERS |當工作在等候取得具有中止封鎖器的大量更新 (BU) 鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_BU_LOW_PRIORITY |當工作在等候取得低優先順序的大量更新 (BU) 鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_IS |當工作在等候取得意圖共用 (IS) 鎖定時發生。| 
|LCK_M_IS_ABORT_BLOCKERS |當工作在等候取得具有中止封鎖器的意圖共用 (IS) 鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_IS_LOW_PRIORITY |當工作在等候取得低優先順序的意圖共用 (IS) 鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_IU |當工作在等候取得意圖更新 (IU) 鎖定時發生。| 
|LCK_M_IU_ABORT_BLOCKERS |當工作在等候取得具有中止封鎖器的意圖更新 (IU) 鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_IU_LOW_PRIORITY |當工作在等候取得低優先順序的意圖更新 (IU) 鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_IX  |當工作在等候取得意圖獨佔 (IX) 鎖定時發生。| 
|LCK_M_IX_ABORT_BLOCKERS |當工作在等候取得具有中止封鎖器的意圖獨佔 (IX) 鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_IX_LOW_PRIORITY |當工作在等候取得低優先順序的意圖獨佔 (IX) 鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_NL  |當工作在等候取得目前索引鍵值的 NULL 鎖定，以及目前索引鍵和前一個索引鍵之間的插入範圍鎖定時發生。 索引鍵的 NULL 鎖定是一個立即釋放鎖定。| 
|LCK_M_RIn_NL_ABORT_BLOCKERS |當工作在等候取得目前索引鍵值的具有中止封鎖器的 NULL 鎖定，以及目前索引鍵和前一個索引鍵之間具有中止封鎖器的插入範圍鎖定時發生。 索引鍵的 NULL 鎖定是一個立即釋放鎖定。 （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_NL_LOW_PRIORITY |當工作在等候取得目前索引鍵值的低優先順序的 NULL 鎖定，以及目前索引鍵和前一個索引鍵之間低優先順序的插入範圍鎖定時發生。 索引鍵的 NULL 鎖定是一個立即釋放鎖定。 （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_S  |當工作在等候取得目前索引鍵值的共用鎖定，以及目前索引鍵和前一個索引鍵之間的插入範圍鎖定時發生。| 
|LCK_M_RIn_S_ABORT_BLOCKERS |當工作在等候取得目前索引鍵值的具有中止封鎖器的共用鎖定，以及目前索引鍵和前一個索引鍵之間具有中止封鎖器的插入範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_S_LOW_PRIORITY |當工作在等候取得目前索引鍵值的低優先順序的共用鎖定，以及目前索引鍵和前一個索引鍵之間低優先順序的插入範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_U  |工作在等候取得目前索引鍵值的更新鎖定，以及目前索引鍵和前一個索引鍵之間的插入範圍鎖定。| 
|LCK_M_RIn_U_ABORT_BLOCKERS |工作在等候取得目前索引鍵值的具有中止封鎖器的更新鎖定，以及目前索引鍵和前一個索引鍵之間具有中止封鎖器的插入範圍鎖定  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_U_LOW_PRIORITY |工作在等候取得目前索引鍵值的低優先順序的更新鎖定，以及目前索引鍵和前一個索引鍵之間低優先順序的插入範圍鎖定  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_X  |當工作在等候取得目前索引鍵值的獨佔鎖定，以及目前索引鍵和前一個索引鍵之間的插入範圍鎖定時發生。| 
|LCK_M_RIn_X_ABORT_BLOCKERS |當工作在等候取得目前索引鍵值的具有中止封鎖器的獨佔鎖定，以及目前索引鍵和前一個索引鍵之間具有中止封鎖器的插入範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RIn_X_LOW_PRIORITY |當工作在等候取得目前索引鍵值的低優先順序的獨佔鎖定，以及目前索引鍵和前一個索引鍵之間低優先順序的插入範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RS_S  |當工作在等候取得目前索引鍵值的共用鎖定，以及目前索引鍵和前一個索引鍵之間的共用範圍鎖定時發生。| 
|LCK_M_RS_S_ABORT_BLOCKERS |當工作在等候取得目前索引鍵值的具有中止封鎖器的共用鎖定，以及目前索引鍵和前一個索引鍵之間具有中止封鎖器的共用範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RS_S_LOW_PRIORITY |當工作在等候取得目前索引鍵值的低優先順序的共用鎖定，以及目前索引鍵和前一個索引鍵之間低優先順序的共用範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RS_U  |當工作在等候取得目前索引鍵值的更新鎖定，以及目前索引鍵和前一個索引鍵之間的更新範圍鎖定時發生。| 
|LCK_M_RS_U_ABORT_BLOCKERS |當工作在等候取得目前索引鍵值的具有中止封鎖器的更新鎖定，以及目前索引鍵和前一個索引鍵之間具有中止封鎖器的更新範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RS_U_LOW_PRIORITY |當工作在等候取得目前索引鍵值的低優先順序的更新鎖定，以及目前索引鍵和前一個索引鍵之間低優先順序的更新範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RX_S  |當工作在等候取得目前索引鍵值的共用鎖定，以及目前索引鍵和前一個索引鍵之間的獨佔範圍鎖定時發生。| 
|LCK_M_RX_S_ABORT_BLOCKERS |當工作在等候取得目前索引鍵值的具有中止封鎖器的共用鎖定，以及目前索引鍵和前一個索引鍵之間具有中止封鎖器的獨佔範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RX_S_LOW_PRIORITY |當工作在等候取得目前索引鍵值的低優先順序的共用鎖定，以及目前索引鍵和前一個索引鍵之間低優先順序的獨佔範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RX_U  |當工作在等候取得目前索引鍵值的更新鎖定，以及目前索引鍵和前一個索引鍵之間的獨佔範圍鎖定時發生。| 
|LCK_M_RX_U_ABORT_BLOCKERS |當工作在等候取得目前索引鍵值的具有中止封鎖器的更新鎖定，以及目前索引鍵和前一個索引鍵之間具有中止封鎖器的獨佔範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RX_U_LOW_PRIORITY |當工作在等候取得目前索引鍵值的低優先順序的更新鎖定，以及目前索引鍵和前一個索引鍵之間低優先順序的獨佔範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RX_X  |當工作在等候取得目前索引鍵值的獨佔鎖定，以及目前索引鍵和前一個索引鍵之間的獨佔範圍鎖定時發生。| 
|LCK_M_RX_X_ABORT_BLOCKERS |當工作在等候取得目前索引鍵值的具有中止封鎖器的獨佔鎖定，以及目前索引鍵和前一個索引鍵之間具有中止封鎖器的獨佔範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_RX_X_LOW_PRIORITY |當工作在等候取得目前索引鍵值的低優先順序的獨佔鎖定，以及目前索引鍵和前一個索引鍵之間低優先順序的獨佔範圍鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_S  |當工作在等候取得共用鎖定時發生。| 
|LCK_M_S_ABORT_BLOCKERS |當工作在等候取得具有中止封鎖器的共用鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_S_LOW_PRIORITY |當工作在等候取得低優先順序的共用鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SCH_M  |當工作在等候取得結構描述修改鎖定時發生。| 
|LCK_M_SCH_M_ABORT_BLOCKERS |當工作在等候取得具有中止封鎖器的結構描述修改鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SCH_M_LOW_PRIORITY |當工作在等候取得低優先順序的結構描述修改鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SCH_S  |當工作在等候取得結構描述共用鎖定時發生。| 
|LCK_M_SCH_S_ABORT_BLOCKERS |當工作在等候取得具有中止封鎖器的結構描述共用鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SCH_S_LOW_PRIORITY |當工作在等候取得低優先順序的結構描述共用鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SIU  |當工作在等候取得共用意圖更新鎖定時發生。| 
|LCK_M_SIU_ABORT_BLOCKERS |當工作在等候取得具有中止封鎖器的共用意圖更新鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SIU_LOW_PRIORITY |當工作在等候取得低優先順序的共用意圖更新鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SIX  |當工作在等候取得共用意圖獨佔鎖定時發生。| 
|LCK_M_SIX_ABORT_BLOCKERS |當工作在等候取得具有中止封鎖器的共用意圖獨佔鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_SIX_LOW_PRIORITY |當工作在等候取得低優先順序的共用意圖獨佔鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_U  |當工作在等候取得更新鎖定時發生。| 
|LCK_M_U_ABORT_BLOCKERS |當工作在等候取得具有中止封鎖器的更新鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_U_LOW_PRIORITY |當工作在等候取得低優先順序的更新鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_UIX  |當工作在等候取得更新意圖獨佔鎖定時發生。| 
|LCK_M_UIX_ABORT_BLOCKERS |當工作在等候取得具有中止封鎖器的更新意圖獨佔鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_UIX_LOW_PRIORITY |當工作在等候取得低優先順序的更新意圖獨佔鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_X  |當工作在等候取得獨佔鎖定時發生。| 
|LCK_M_X_ABORT_BLOCKERS |當工作在等候取得具有中止封鎖器的獨佔鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LCK_M_X_LOW_PRIORITY |當工作在等候取得低優先順序的獨佔鎖定時發生  （與 ALTER TABLE 和 ALTER INDEX 的低優先順序等候選項。）， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOG_POOL_SCAN |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOG_RATE_GOVERNOR |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGBUFFER  |當工作在等候記錄緩衝區的空間來儲存記錄時發生。 如果這個值一直居高不下，可能表示記錄裝置趕不上伺服器產生的記錄量。| 
|LOGCAPTURE_LOGPOOLTRUNCPOINT |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGGENERATION |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|LOGMGR  |當工作在關閉資料庫時，於關閉記錄之前等候任何未完成的記錄 I/O 完成時發生。| 
|LOGMGR_FLUSH  |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|LOGMGR_PMM_LOG |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGMGR_QUEUE |在記錄寫入器工作等候工作要求時發生。| 
|LOGMGR_RESERVE_APPEND  |當工作在等候記錄截斷清出記錄空間，讓工作寫入新記錄時發生。 請考慮增加受影響之資料庫的記錄檔案大小，以縮短這個等候時間。| 
|LOGPOOL_CACHESIZE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGPOOL_CONSUMER |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGPOOL_CONSUMERSET |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGPOOL_FREEPOOLS |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGPOOL_MGRSET |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGPOOL_REPLACEMENTSET |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOGPOOLREFCOUNTEDOBJECT_REFDONE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|LOWFAIL_MEMMGR_QUEUE  |在等候記憶體變成可供使用的狀態時發生。| 
|MD_AGENT_YIELD |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|MD_LAZYCACHE_RWLOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|MEMORY_ALLOCATION_EXT |配置的記憶體內部的 SQL Server 記憶體集區或作業系統時，就會發生。， <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|MEMORY_GRANT_UPDATE |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|METADATA_LAZYCACHE_RWLOCK |TBD <br /> **適用於**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]只。 |  
|MIGRATIONBUFFER |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|MISCELLANEOUS |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|MISCELLANEOUS |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|MSQL_DQ  |在工作等候分散式查詢作業完成時發生。 這種等候類型可用來偵測潛在的 Multiple Active Result Set (MARS) 應用程式死結。 等候會隨著分散式查詢呼叫的完成而結束。| 
|MSQL_XACT_MGR_MUTEX  |當工作在等候取得工作階段交易管理員的擁有權，以執行工作階段層級交易作業時發生。| 
|MSQL_XACT_MUTEX |在同步處理交易使用量時發生。 要求必須先取得 Mutex，才能使用交易。| 
|MSQL_XP  |當工作在等候擴充預存程序結束時發生。 SQL Server 會使用這個等候狀態來偵測可能發生的 MARS 應用程式死結。 這個等候會隨著擴充預存程序呼叫的結束而停止。| 
|MSSEARCH |在使用全文檢索搜尋呼叫時發生。 這個等候會隨著全文檢索作業的完成而結束。 這並不表示發生競爭情況，而是指出全文檢索作業的持續時間。| 
|NET_WAITFOR_PACKET |當連接在網路讀取期間等候網路封包時發生。| 
|NETWORKSXMLMGRLOAD |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|NODE_CACHE_MUTEX |TBD| 
|OLEDB |在 SQL Server 呼叫 SQL Server Native Client OLE DB 提供者時發生。 這個等候類型不用於同步處理， 而會指出呼叫 OLE DB 提供者的持續時間。| 
|ONDEMAND_TASK_QUEUE |在背景工作等候高優先權的系統工作要求時發生。 如果等候時間很長，表示沒有高優先權的要求需要處理，而且應該不會造成任何問題。| 
|PAGEIOLATCH_DT  |當工作在位於 I/O 要求中的緩衝區閂鎖待命時發生。 閂鎖要求是終結模式。 如果等候時間很長，表示磁碟子系統有問題。| 
|PAGEIOLATCH_EX  |當工作在位於 I/O 要求中的緩衝區閂鎖待命時發生。 閂鎖要求是獨佔模式。 如果等候時間很長，表示磁碟子系統有問題。| 
|PAGEIOLATCH_KP  |當工作在位於 I/O 要求中的緩衝區閂鎖待命時發生。 閂鎖要求是保留模式。 如果等候時間很長，表示磁碟子系統有問題。| 
|PAGEIOLATCH_NL  |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|PAGEIOLATCH_SH  |當工作在位於 I/O 要求中的緩衝區閂鎖待命時發生。 閂鎖要求是共用模式。 如果等候時間很長，表示磁碟子系統有問題。| 
|PAGEIOLATCH_UP  |當工作在位於 I/O 要求中的緩衝區閂鎖待命時發生。 閂鎖要求是更新模式。 如果等候時間很長，表示磁碟子系統有問題。| 
|PAGELATCH_DT  |當工作不是在 I/O 要求中的緩衝區閂鎖待命時發生。 閂鎖要求是終結模式。| 
|PAGELATCH_EX  |當工作不是在 I/O 要求中的緩衝區閂鎖待命時發生。 閂鎖要求是獨佔模式。| 
|PAGELATCH_KP  |當工作不是在 I/O 要求中的緩衝區閂鎖待命時發生。 閂鎖要求是保留模式。| 
|PAGELATCH_NL  |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|PAGELATCH_SH  |當工作不是在 I/O 要求中的緩衝區閂鎖待命時發生。 閂鎖要求是共用模式。| 
|PAGELATCH_UP  |當工作不是在 I/O 要求中的緩衝區閂鎖待命時發生。 閂鎖要求是更新模式。| 
|PARALLEL_BACKUP_QUEUE |在序列化 RESTORE HEADERONLY、RESTORE FILELISTONLY 或 RESTORE LABELONLY 所產生的輸出時發生。| 
|PARALLEL_REDO_DRAIN_WORKER |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PARALLEL_REDO_FLOW_CONTROL |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PARALLEL_REDO_LOG_CACHE |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PARALLEL_REDO_TRAN_LIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PARALLEL_REDO_TRAN_TURN |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PARALLEL_REDO_WORKER_SYNC |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PARALLEL_REDO_WORKER_WAIT_WORK |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PERFORMANCE_COUNTERS_RWLOCK |TBD| 
|PHYSICAL_SEEDING_DMV |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|POOL_LOG_RATE_GOVERNOR |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_ABR |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|PREEMPTIVE_AUDIT_ACCESS_EVENTLOG |在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 作業系統 (SQLOS) 排程器切換到先佔式模式，以便將稽核事件寫入 Windows 事件記錄檔時發生。 <br /> **適用於**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]只。 |  
|PREEMPTIVE_AUDIT_ACCESS_SECLOG |當 SQLOS 排程器切換到先佔式模式，以便將稽核事件寫入 Windows 安全性記錄檔時發生。 <br /> **適用於**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]只。 |  
|PREEMPTIVE_CLOSEBACKUPMEDIA |當 SQLOS 排程器切換到先佔式模式，以便關閉備份媒體時發生。| 
|PREEMPTIVE_CLOSEBACKUPTAPE |當 SQLOS 排程器切換到先佔式模式，以便關閉磁帶備份裝置時發生。| 
|PREEMPTIVE_CLOSEBACKUPVDIDEVICE |當 SQLOS 排程器切換到先佔式模式，以便關閉虛擬備份裝置時發生。| 
|PREEMPTIVE_CLUSAPI_CLUSTERRESOURCECONTROL |當 SQLOS 排程器切換到先佔式模式，以便執行 Windows 容錯移轉叢集作業時發生。| 
|PREEMPTIVE_COM_COCREATEINSTANCE |當 SQLOS 排程器切換到先佔式模式，以便建立 COM 物件時發生。| 
|PREEMPTIVE_COM_COGETCLASSOBJECT |TBD| 
|PREEMPTIVE_COM_CREATEACCESSOR |TBD| 
|PREEMPTIVE_COM_DELETEROWS |TBD| 
|PREEMPTIVE_COM_GETCOMMANDTEXT |TBD| 
|PREEMPTIVE_COM_GETDATA |TBD| 
|PREEMPTIVE_COM_GETNEXTROWS |TBD| 
|PREEMPTIVE_COM_GETRESULT |TBD| 
|PREEMPTIVE_COM_GETROWSBYBOOKMARK |TBD| 
|PREEMPTIVE_COM_LBFLUSH |TBD| 
|PREEMPTIVE_COM_LBLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBREADAT |TBD| 
|PREEMPTIVE_COM_LBSETSIZE |TBD| 
|PREEMPTIVE_COM_LBSTAT |TBD| 
|PREEMPTIVE_COM_LBUNLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBWRITEAT |TBD| 
|PREEMPTIVE_COM_QUERYINTERFACE |TBD| 
|PREEMPTIVE_COM_RELEASE |TBD| 
|PREEMPTIVE_COM_RELEASEACCESSOR |TBD| 
|PREEMPTIVE_COM_RELEASEROWS |TBD| 
|PREEMPTIVE_COM_RELEASESESSION |TBD| 
|PREEMPTIVE_COM_RESTARTPOSITION |TBD| 
|PREEMPTIVE_COM_SEQSTRMREAD |TBD| 
|PREEMPTIVE_COM_SEQSTRMREADANDWRITE |TBD| 
|PREEMPTIVE_COM_SETDATAFAILURE |TBD| 
|PREEMPTIVE_COM_SETPARAMETERINFO |TBD| 
|PREEMPTIVE_COM_SETPARAMETERPROPERTIES |TBD| 
|PREEMPTIVE_COM_STRMLOCKREGION |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDREAD |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDWRITE |TBD| 
|PREEMPTIVE_COM_STRMSETSIZE |TBD| 
|PREEMPTIVE_COM_STRMSTAT |TBD| 
|PREEMPTIVE_COM_STRMUNLOCKREGION |TBD| 
|PREEMPTIVE_CONSOLEWRITE |TBD| 
|PREEMPTIVE_CREATEPARAM |TBD| 
|PREEMPTIVE_DEBUG |TBD| 
|PREEMPTIVE_DFSADDLINK |TBD| 
|PREEMPTIVE_DFSLINKEXISTCHECK |TBD| 
|PREEMPTIVE_DFSLINKHEALTHCHECK |TBD| 
|PREEMPTIVE_DFSREMOVELINK |TBD| 
|PREEMPTIVE_DFSREMOVEROOT |TBD| 
|PREEMPTIVE_DFSROOTFOLDERCHECK |TBD| 
|PREEMPTIVE_DFSROOTINIT |TBD| 
|PREEMPTIVE_DFSROOTSHARECHECK |TBD| 
|PREEMPTIVE_DTC_ABORT |TBD| 
|PREEMPTIVE_DTC_ABORTREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_BEGINTRANSACTION |TBD| 
|PREEMPTIVE_DTC_COMMITREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_ENLIST |TBD| 
|PREEMPTIVE_DTC_PREPAREREQUESTDONE |TBD| 
|PREEMPTIVE_FILESIZEGET |TBD| 
|PREEMPTIVE_FSAOLEDB_ABORTTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_COMMITTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_STARTTRANSACTION |TBD| 
|PREEMPTIVE_FSRECOVER_UNCONDITIONALUNDO |TBD| 
|PREEMPTIVE_GETRMINFO |TBD| 
|PREEMPTIVE_HADR_LEASE_MECHANISM |Always On 可用性群組租用管理員排程 CSS 診斷。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_HTTP_EVENT_WAIT |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_HTTP_REQUEST |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_LOCKMONITOR |TBD| 
|PREEMPTIVE_MSS_RELEASE |TBD| 
|PREEMPTIVE_ODBCOPS |TBD| 
|PREEMPTIVE_OLE_UNINIT |TBD| 
|PREEMPTIVE_OLEDB_ABORTORCOMMITTRAN |TBD| 
|PREEMPTIVE_OLEDB_ABORTTRAN |TBD| 
|PREEMPTIVE_OLEDB_GETDATASOURCE |TBD| 
|PREEMPTIVE_OLEDB_GETLITERALINFO |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTYINFO |TBD| 
|PREEMPTIVE_OLEDB_GETSCHEMALOCK |TBD| 
|PREEMPTIVE_OLEDB_JOINTRANSACTION |TBD| 
|PREEMPTIVE_OLEDB_RELEASE |TBD| 
|PREEMPTIVE_OLEDB_SETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDBOPS |TBD| 
|PREEMPTIVE_OS_ACCEPTSECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_ACQUIRECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_AUTHENTICATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHORIZATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHZGETINFORMATIONFROMCONTEXT |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZECONTEXTFROMSID |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZERESOURCEMANAGER |TBD| 
|PREEMPTIVE_OS_BACKUPREAD |TBD| 
|PREEMPTIVE_OS_CLOSEHANDLE |TBD| 
|PREEMPTIVE_OS_CLUSTEROPS |TBD| 
|PREEMPTIVE_OS_COMOPS |TBD| 
|PREEMPTIVE_OS_COMPLETEAUTHTOKEN |TBD| 
|PREEMPTIVE_OS_COPYFILE |TBD| 
|PREEMPTIVE_OS_CREATEDIRECTORY |TBD| 
|PREEMPTIVE_OS_CREATEFILE |TBD| 
|PREEMPTIVE_OS_CRYPTACQUIRECONTEXT |TBD| 
|PREEMPTIVE_OS_CRYPTIMPORTKEY |TBD| 
|PREEMPTIVE_OS_CRYPTOPS |TBD| 
|PREEMPTIVE_OS_DECRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_DELETEFILE |TBD| 
|PREEMPTIVE_OS_DELETESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_DEVICEIOCONTROL |TBD| 
|PREEMPTIVE_OS_DEVICEOPS |TBD| 
|PREEMPTIVE_OS_DIRSVC_NETWORKOPS |TBD| 
|PREEMPTIVE_OS_DISCONNECTNAMEDPIPE |TBD| 
|PREEMPTIVE_OS_DOMAINSERVICESOPS |TBD| 
|PREEMPTIVE_OS_DSGETDCNAME |TBD| 
|PREEMPTIVE_OS_DTCOPS |TBD| 
|PREEMPTIVE_OS_ENCRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_FILEOPS |TBD| 
|PREEMPTIVE_OS_FINDFILE |TBD| 
|PREEMPTIVE_OS_FLUSHFILEBUFFERS |TBD| 
|PREEMPTIVE_OS_FORMATMESSAGE |TBD| 
|PREEMPTIVE_OS_FREECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_FREELIBRARY |TBD| 
|PREEMPTIVE_OS_GENERICOPS |TBD| 
|PREEMPTIVE_OS_GETADDRINFO |TBD| 
|PREEMPTIVE_OS_GETCOMPRESSEDFILESIZE |TBD| 
|PREEMPTIVE_OS_GETDISKFREESPACE |TBD| 
|PREEMPTIVE_OS_GETFILEATTRIBUTES |TBD| 
|PREEMPTIVE_OS_GETFILESIZE |TBD| 
|PREEMPTIVE_OS_GETFINALFILEPATHBYHANDLE |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_OS_GETLONGPATHNAME |TBD| 
|PREEMPTIVE_OS_GETPROCADDRESS |TBD| 
|PREEMPTIVE_OS_GETVOLUMENAMEFORVOLUMEMOUNTPOINT |TBD| 
|PREEMPTIVE_OS_GETVOLUMEPATHNAME |TBD| 
|PREEMPTIVE_OS_INITIALIZESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_LIBRARYOPS |TBD| 
|PREEMPTIVE_OS_LOADLIBRARY |TBD| 
|PREEMPTIVE_OS_LOGONUSER |TBD| 
|PREEMPTIVE_OS_LOOKUPACCOUNTSID |TBD| 
|PREEMPTIVE_OS_MESSAGEQUEUEOPS |TBD| 
|PREEMPTIVE_OS_MOVEFILE |TBD| 
|PREEMPTIVE_OS_NETGROUPGETUSERS |TBD| 
|PREEMPTIVE_OS_NETLOCALGROUPGETMEMBERS |TBD| 
|PREEMPTIVE_OS_NETUSERGETGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERGETLOCALGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERMODALSGET |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICY |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICYFREE |TBD| 
|PREEMPTIVE_OS_OPENDIRECTORY |TBD| 
|PREEMPTIVE_OS_PDH_WMI_INIT |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_OS_PIPEOPS |TBD| 
|PREEMPTIVE_OS_PROCESSOPS |TBD| 
|PREEMPTIVE_OS_QUERYCONTEXTATTRIBUTES |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_OS_QUERYREGISTRY |TBD| 
|PREEMPTIVE_OS_QUERYSECURITYCONTEXTTOKEN |TBD| 
|PREEMPTIVE_OS_REMOVEDIRECTORY |TBD| 
|PREEMPTIVE_OS_REPORTEVENT |TBD| 
|PREEMPTIVE_OS_REVERTTOSELF |TBD| 
|PREEMPTIVE_OS_RSFXDEVICEOPS |TBD| 
|PREEMPTIVE_OS_SECURITYOPS |TBD| 
|PREEMPTIVE_OS_SERVICEOPS |TBD| 
|PREEMPTIVE_OS_SETENDOFFILE |TBD| 
|PREEMPTIVE_OS_SETFILEPOINTER |TBD| 
|PREEMPTIVE_OS_SETFILEVALIDDATA |TBD| 
|PREEMPTIVE_OS_SETNAMEDSECURITYINFO |TBD| 
|PREEMPTIVE_OS_SQLCLROPS |TBD| 
|PREEMPTIVE_OS_SQMLAUNCH |TBD <br /> **適用於**： [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] 至 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]。 |  
|PREEMPTIVE_OS_VERIFYSIGNATURE |TBD| 
|PREEMPTIVE_OS_VERIFYTRUST |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_OS_VSSOPS |TBD| 
|PREEMPTIVE_OS_WAITFORSINGLEOBJECT |TBD| 
|PREEMPTIVE_OS_WINSOCKOPS |TBD| 
|PREEMPTIVE_OS_WRITEFILE |TBD| 
|PREEMPTIVE_OS_WRITEFILEGATHER |TBD| 
|PREEMPTIVE_OS_WSASETLASTERROR |TBD| 
|PREEMPTIVE_REENLIST |TBD| 
|PREEMPTIVE_RESIZELOG |TBD| 
|PREEMPTIVE_ROLLFORWARDREDO |TBD| 
|PREEMPTIVE_ROLLFORWARDUNDO |TBD| 
|PREEMPTIVE_SB_STOPENDPOINT |TBD| 
|PREEMPTIVE_SERVER_STARTUP |TBD| 
|PREEMPTIVE_SETRMINFO |TBD| 
|PREEMPTIVE_SHAREDMEM_GETDATA |TBD| 
|PREEMPTIVE_SNIOPEN |TBD| 
|PREEMPTIVE_SOSHOST |TBD| 
|PREEMPTIVE_SOSTESTING |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|PREEMPTIVE_SP_SERVER_DIAGNOSTICS |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_STARTRM |TBD| 
|PREEMPTIVE_STREAMFCB_CHECKPOINT |TBD| 
|PREEMPTIVE_STREAMFCB_RECOVER |TBD| 
|PREEMPTIVE_STRESSDRIVER |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|PREEMPTIVE_TESTING |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|PREEMPTIVE_TRANSIMPORT |TBD| 
|PREEMPTIVE_UNMARSHALPROPAGATIONTOKEN |TBD| 
|PREEMPTIVE_VSS_CREATESNAPSHOT |TBD| 
|PREEMPTIVE_VSS_CREATEVOLUMESNAPSHOT |TBD| 
|PREEMPTIVE_XE_CALLBACKEXECUTE |TBD| 
|PREEMPTIVE_XE_CX_FILE_OPEN |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_XE_CX_HTTP_CALL |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PREEMPTIVE_XE_DISPATCHER |TBD| 
|PREEMPTIVE_XE_ENGINEINIT |TBD| 
|PREEMPTIVE_XE_GETTARGETSTATE |TBD| 
|PREEMPTIVE_XE_SESSIONCOMMIT |TBD| 
|PREEMPTIVE_XE_TARGETFINALIZE |TBD| 
|PREEMPTIVE_XE_TARGETINIT |TBD| 
|PREEMPTIVE_XE_TIMERRUN |TBD| 
|PREEMPTIVE_XETESTING |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|PRINT_ROLLBACK_PROGRESS |用於使用者處理序在已經使用 ALTER DATABASE 終止子句加以轉換的資料庫中結束時等候。 如需詳細資訊，請參閱 ALTER DATABASE & Amp;#40;transact-SQL&AMP;#41;。| 
|PRU_ROLLBACK_DEFERRED |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_ALL_COMPONENTS_INITIALIZED |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_COOP_SCAN |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_DIRECTLOGCONSUMER_GETNEXT |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_EVENT_SESSION_INIT_MUTEX |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_FABRIC_REPLICA_CONTROLLER_DATA_LOSS |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_ACTION_COMPLETED |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_CHANGE_NOTIFIER_TERMINATION_SYNC |當背景工作正在等候接收 （經由輪詢） 的背景工作終止時，就會發生 Windows Server 容錯移轉叢集通知。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_CLUSTER_INTEGRATION |附加、 取代和/或移除作業正在等候擷取 Alwayson 內部清單 （例如網路、 網路位址或可用性群組接聽程式的清單） 的寫入鎖定。 僅限內部使用 <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_FAILOVER_COMPLETED |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_JOIN |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_OFFLINE_COMPLETED |Alwayson 卸除可用性群組作業正在等候目標可用性群組離線，然後再終結 Windows Server 容錯移轉叢集的物件。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_ONLINE_COMPLETED |Alwayson 建立或容錯移轉可用性群組作業正在等候目標可用性群組上線。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_POST_ONLINE_COMPLETED |Alwayson 卸除可用性群組作業正在等候先前命令中排程任何背景工作終止。 例如，可能會存在將可用性資料庫轉換成主要角色的背景工作。 DROP AVAILABILITY GROUP DDL 必須等候此背景工作終止，才能避免競爭情形。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_SERVER_READY_CONNECTIONS |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADR_WORKITEM_COMPLETED |等候非同步工作完成之執行緒的內部等候。 這是預期的等候，而且使用 CSS。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_HADRSIM |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_LOG_CONSOLIDATION_IO |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_LOG_CONSOLIDATION_POLL |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_MD_LOGIN_STATS |在 登入統計資料的中繼資料中執行內部同步處理期間發生。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_MD_RELATION_CACHE |在資料表或索引中繼資料中執行內部同步處理期間發生。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_MD_SERVER_CACHE |連結伺服器上的中繼資料中執行內部同步處理期間發生。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_MD_UPGRADE_CONFIG |在升級伺服器範圍組態的內部同步處理期間發生。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_PREEMPTIVE_APP_USAGE_TIMER |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_PREEMPTIVE_AUDIT_ACCESS_WINDOWSLOG |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_QRY_BPMEMORY |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_REPLICA_ONLINE_INIT_MUTEX |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_SBS_FILE_OPERATION |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_XTP_FSSTORAGE_MAINTENANCE |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|PWAIT_XTP_HOST_STORAGE_WAIT |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_ASYNC_CHECK_CONSISTENCY_TASK |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_ASYNC_PERSIST_TASK |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_ASYNC_PERSIST_TASK_START |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_ASYNC_QUEUE |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_BCKG_TASK |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_BLOOM_FILTER |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_CLEANUP_STALE_QUERIES_TASK_MAIN_LOOP_SLEEP |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_CTXS |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_DB_DISK |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_DYN_VECTOR |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_EXCLUSIVE_ACCESS |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_HOST_INIT |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_LOADDB |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_PERSIST_TASK_MAIN_LOOP_SLEEP |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_QDS_CAPTURE_INIT |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_SHUTDOWN_QUEUE |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_STMT |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_STMT_DISK |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_TASK_SHUTDOWN |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QDS_TASK_START |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QE_WARN_LIST_SYNC |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QPJOB_KILL |指出非同步自動統計資料更新開始執行時，已被 KILL 的呼叫所取消。 終止執行緒已經暫停，正在等候它開始接聽 KILL 命令。 其值最好少於一秒。| 
|QPJOB_WAITFOR_ABORT |指出非同步自動統計資料更新在執行時，已被 KILL 的呼叫所取消。 雖然這項更新已經完成了，但卻被暫停到終止執行緒訊息協調完成為止。 這種狀態雖然很平常，卻很少見，而且為時甚短。 其值最好少於一秒。| 
|QRY_MEM_GRANT_INFO_MUTEX  |當查詢執行記憶體管理試圖控制靜態授與資訊清單的存取時發生。 這個狀態會列出目前已授與和等候中之記憶體要求的相關資訊。 這個狀態是一種簡單的存取控制狀態。 這個狀態應該不會有長時間的等候。 如果沒有釋出這個 Mutex，所有新的記憶體使用查詢都會停止回應。| 
|QRY_PARALLEL_THREAD_MUTEX |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QRY_PROFILE_LIST_MUTEX |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QUERY_ERRHDL_SERVICE_DONE |僅供參考之用。 不支援。 <br /> **適用於**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]只。 |  
|QUERY_WAIT_ERRHDL_SERVICE |僅供參考之用。  不支援。 <br /> **適用於**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]只。  |  
|QUERY_EXECUTION_INDEX_SORT_EVENT_OPEN |在離線建立索引建置平行執行時，以及排序中的不同工作者執行緒同步處理排序檔存取作業時的某些情況中發生。| 
|QUERY_NOTIFICATION_MGR_MUTEX  |在同步處理查詢通知管理員中的記憶體回收佇列時發生。| 
|QUERY_NOTIFICATION_SUBSCRIPTION_MUTEX  |在同步處理查詢通知中交易的狀態時發生。| 
|QUERY_NOTIFICATION_TABLE_MGR_MUTEX  |在查詢通知管理員內執行內部同步處理時發生。| 
|QUERY_NOTIFICATION_UNITTEST_MUTEX  |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|QUERY_OPTIMIZER_PRINT_MUTEX |在同步處理查詢最佳化工具診斷輸出生產作業時發生。 如果已啟用診斷設定下的 Microsoft 產品支援的方向，才會發生這種等候類型。| 
|QUERY_TASK_ENQUEUE_MUTEX |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|QUERY_TRACEOUT |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|RBIO_WAIT_VLF |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|RECOVER_CHANGEDB |在同步處理暖待命資料庫中的資料庫狀態時發生。| 
|RECOVERY_MGR_LOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REDO_THREAD_PENDING_WORK |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REDO_THREAD_SYNC |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REMOTE_BLOCK_IO |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REMOTE_DATA_ARCHIVE_MIGRATION_DMV |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REMOTE_DATA_ARCHIVE_SCHEMA_DMV |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REMOTE_DATA_ARCHIVE_SCHEMA_TASK_QUEUE |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REPL_CACHE_ACCESS |在複寫發行項快取上進行同步處理時發生。 在這些等候期間，複寫記錄讀取器將會暫停，而已發行資料表上的資料定義語言 (DDL) 陳述式也會遭到封鎖。| 
|REPL_HISTORYCACHE_ACCESS |TBD| 
|REPL_SCHEMA_ACCESS |在同步處理複寫結構描述版本資訊時發生。 在已複寫物件上執行 DDL 陳述式時，以及當記錄讀取器依據 DDL 出現位置來建立或取用版本化結構描述時，都會出現這種狀態。 如果您使用異動複寫的單一 「 發行者 」 上有多個已發行的資料庫，而且已發行的資料庫非常活躍這種等候類型可能會發生競爭情況。| 
|REPL_TRANFSINFO_ACCESS |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REPL_TRANHASHTABLE_ACCESS |TBD| 
|REPL_TRANTEXTINFO_ACCESS |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|REPLICA_WRITES |在工作等候頁面寫入資料庫快照集或 DBCC 複本完成時發生。| 
|REQUEST_DISPENSER_PAUSE |當工作在等候所有未處理 I/O 完成，使其可凍結檔案 I/O 以供快照集備份時發生。| 
|REQUEST_FOR_DEADLOCK_SEARCH |在死結監視器等候開始下個死結搜尋時發生。 這個等候應該在兩次死結偵測之間發生，在此資源上的等候時間如果很長，並不表示發生任何問題。| 
|RESERVED_MEMORY_ALLOCATION_EXT |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|RESMGR_THROTTLED |當新的要求送入，然後根據 GROUP_MAX_REQUESTS 設定降低速度。| 
|RESOURCE_GOVERNOR_IDLE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|RESOURCE_QUEUE |在同步處理各種內部資源佇列時發生。| 
|RESOURCE_SEMAPHORE |在其他並行查詢導致查詢記憶體要求無法立即取得授權時發生。 如果等候頻率很高且等候時間很長，可能表示並行查詢數目過多、重複編譯，或是記憶體要求量過大。| 
|RESOURCE_SEMAPHORE_MUTEX |在查詢等候系統滿足其執行緒保留要求時發生。 同步處理查詢編譯與記憶體授權要求時也會發生這種等候類型。| 
|RESOURCE_SEMAPHORE_QUERY_COMPILE |當並行查詢編譯數目達到調整流速上限時發生。 如果等候頻率很高且等候時間很長，可能表示編譯數目過多，或是計畫無法快取。| 
|RESOURCE_SEMAPHORE_SMALL_QUERY |在其他並行查詢導致小型查詢之記憶體要求無法立即取得授權時發生。 等候時間應該不會超過幾秒鐘，因為如果伺服器無法在幾秒鐘內授權使用要求的記憶體，它就會將要求傳送到主要查詢記憶體集區。 如果等候頻率很高，可能表示並行的小型查詢數目過多，而主要記憶體集區則受到等候中的查詢所封鎖。 <br /> **適用於**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]只。 |  
|RESTORE_FILEHANDLECACHE_ENTRYLOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|RESTORE_FILEHANDLECACHE_LOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|RG_RECONFIG |TBD| 
|ROWGROUP_OP_STATS |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|ROWGROUP_VERSION |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|RTDATA_LIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SATELLITE_CARGO |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SATELLITE_SERVICE_SETUP |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SATELLITE_TASK |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SBS_DISPATCH |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SBS_RECEIVE_TRANSPORT |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SBS_TRANSPORT |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SCAN_CHAR_HASH_ARRAY_INITIALIZATION |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SEC_DROP_TEMP_KEY |在嘗試卸除暫時安全性金鑰失敗之後，再次重試之前發生。| 
|SECURITY_CNG_PROVIDER_MUTEX |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SECURITY_CRYPTO_CONTEXT_MUTEX |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SECURITY_DBE_STATE_MUTEX |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SECURITY_KEYRING_RWLOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SECURITY_MUTEX |當系統等候控制可延伸金鑰管理 (EKM) 密碼編譯提供者之全域清單和 EKM 工作階段之工作階段範圍清單存取權的 Mutex 時發生。| 
|SECURITY_RULETABLE_MUTEX |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SEMPLAT_DSI_BUILD |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SEQUENCE_GENERATION |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SEQUENTIAL_GUID |正在取得新的循序 GUID 時發生。| 
|SERVER_IDLE_CHECK |資源監視器已嘗試宣告為閒置的 SQL Server 執行個體，或嘗試喚醒時，SQL Server 執行個體閒置狀態的同步處理期間發生。| 
|SERVER_RECONFIGURE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SESSION_WAIT_STATS_CHILDREN |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SHARED_DELTASTORE_CREATION |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SHUTDOWN |在關機陳述式等候使用中的連接結束時發生。| 
|SLEEP_BPOOL_FLUSH |在檢查點調整流速發出新 I/O 之流速以避免磁碟子系統爆滿時發生。| 
|SLEEP_BUFFERPOOL_HELPLW |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLEEP_DBSTARTUP |在啟動資料庫期間等候所有資料庫復原時發生。| 
|SLEEP_DCOMSTARTUP |等候 DCOM 初始化完成的 SQL Server 執行個體啟動期間的大部分時發生一次。| 
|SLEEP_MASTERDBREADY |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLEEP_MASTERMDREADY |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLEEP_MASTERUPGRADED |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLEEP_MEMORYPOOL_ALLOCATEPAGES |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLEEP_MSDBSTARTUP |在 SQL 追蹤等候 msdb 資料庫啟動完成時發生。| 
|SLEEP_RETRY_VIRTUALALLOC |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLEEP_SYSTEMTASK |在啟動背景工作期間等候 tempdb 啟動完成時發生。| 
|SLEEP_TASK |當工作在等候一般事件發生期間進入休眠時發生。| 
|SLEEP_TEMPDBSTARTUP |在工作等候 tempdb 完成啟動時發生。| 
|SLEEP_WORKSPACE_ALLOCATEPAGE |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SLO_UPDATE |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SMSYNC |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SNI_CONN_DUP |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SNI_CRITICAL_SECTION |在 SQL Server 網路元件中的內部同步處理期間發生。| 
|SNI_HTTP_WAITFOR_0_DISCON |在 SQL Server 關機等候未處理的 HTTP 連接結束時發生。| 
|SNI_LISTENER_ACCESS |等候非統一記憶體存取 (NUMA) 節點更新狀態變更時發生。 狀態變更的存取權是序列化的。| 
|SNI_TASK_COMPLETION |當系統在 NUMA 節點狀態變更期間等候所有工作完成時發生。| 
|SNI_WRITE_ASYNC |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SOAP_READ |在等候 HTTP 網路讀取動作完成時發生。| 
|SOAP_WRITE |在等候 HTTP 網路寫入動作完成時發生。| 
|SOCKETDUPLICATEQUEUE_CLEANUP |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SOS_CALLBACK_REMOVAL |在回撥清單上執行同步處理以移除回撥時發生。 在伺服器初始化完成之後，此計數器不應該變更。| 
|SOS_DISPATCHER_MUTEX |在發送器集區的內部同步處理期間發生。 這包括正在調整集區時。| 
|SOS_LOCALALLOCATORLIST |在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 記憶體管理員中執行內部同步處理時發生。 <br /> **適用於**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]只。 |  
|SOS_MEMORY_TOPLEVELBLOCKALLOCATOR |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SOS_MEMORY_USAGE_ADJUSTMENT |調整集區之間的記憶體使用量時發生。| 
|SOS_OBJECT_STORE_DESTROY_MUTEX |在記憶體集區中執行內部同步處理期間從集區終結物件時發生。| 
|SOS_PHYS_PAGE_CACHE |表示執行緒等候取得 Mutex 的時間，執行緒必須取得 Mutex，才能配置實體頁面，或將這些頁面傳回作業系統。 只有 SQL Server 執行個體使用 AWE 記憶體，才會出現在這種類型的等候。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SOS_PROCESS_AFFINITY_MUTEX |在同步處理程序相似性設定的存取作業時發生。| 
|SOS_RESERVEDMEMBLOCKLIST |SQL Server 記憶體管理員中執行內部同步處理期間發生。 <br /> **適用於**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]只。 |  
|SOS_SCHEDULER_YIELD |在工作主動產生排程器以供其他工作執行時發生。 在這段等候期間，該工作將等候系統更新其配量。| 
|SOS_SMALL_PAGE_ALLOC |在配置和釋放某些記憶體物件所管理的記憶體期間發生。| 
|SOS_STACKSTORE_INIT_MUTEX |在同步處理內部存放區初始化時發生。| 
|SOS_SYNC_TASK_ENQUEUE_EVENT |在以同步的方式啟動工作時發生。 SQL Server 中的大部分工作會以非同步方式，在其中控制回到起始工作要求已置於工作佇列後立即啟動。| 
|SOS_VIRTUALMEMORY_LOW |在記憶體配置等候資源管理員釋放虛擬記憶體時發生。| 
|SOSHOST_EVENT |主控的元件，例如 CLR，等候 SQL Server 事件同步處理物件時發生。| 
|SOSHOST_INTERNAL |在同步處理主控元件 (例如 CLR) 使用的記憶體管理員回撥時發生。| 
|SOSHOST_MUTEX |主控的元件，例如 CLR，等候 SQL Server mutex 同步處理物件時發生。| 
|SOSHOST_RWLOCK |主控的元件，例如 CLR，等候 SQL Server 讀取器-寫入器同步處理物件時發生。| 
|SOSHOST_SEMAPHORE |主控的元件，例如 CLR，等候 SQL Server 信號同步處理物件時發生。| 
|SOSHOST_SLEEP |當主控的工作在等候一般事件發生期間進入休眠時發生。 主控的工作是供主控的元件 (例如 CLR) 使用。| 
|SOSHOST_TRACELOCK |在同步處理追蹤資料流的存取作業時發生。| 
|SOSHOST_WAITFORDONE |在主控的元件 (例如 CLR) 等候工作完成時發生。| 
|SP_PREEMPTIVE_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SP_SERVER_DIAGNOSTICS_BUFFER_ACCESS |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SP_SERVER_DIAGNOSTICS_INIT_MUTEX |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SP_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SQLCLR_APPDOMAIN |在 CLR 等候應用程式網域完成啟動時發生。| 
|SQLCLR_ASSEMBLY |在等候存取 appdomain 中已載入的組件清單時發生。| 
|SQLCLR_DEADLOCK_DETECTION |在 CLR 等候死結偵測完成時發生。| 
|SQLCLR_QUANTUM_PUNISHMENT |在 CLR 工作由於本身已超過其執行配量而進行調整流速時發生。 執行這項調整流速的目的是為了降低這個大量使用資源的工作對其他工作所造成的影響。| 
|SQLSORT_NORMMUTEX |在內部同步處理期間初始化內部排序結構時發生。| 
|SQLSORT_SORTMUTEX |在內部同步處理期間初始化內部排序結構時發生。| 
|SQLTRACE_BUFFER_FLUSH |當工作在等候背景工作每四秒將追蹤緩衝區排清到磁碟時發生。 <br /> **適用於**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]只。 |  
|SQLTRACE_FILE_BUFFER |在檔案追蹤的同步處理追蹤緩衝區時發生。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SQLTRACE_FILE_READ_IO_COMPLETION |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SQLTRACE_FILE_WRITE_IO_COMPLETION |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SQLTRACE_INCREMENTAL_FLUSH_SLEEP |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SQLTRACE_LOCK |TBD <br /> **適用對象**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]只。 |  
|SQLTRACE_PENDING_BUFFER_WRITERS |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|SQLTRACE_SHUTDOWN |在追蹤關機等候未處理的追蹤事件完成時發生。| 
|SQLTRACE_WAIT_ENTRIES |在 SQL 追蹤事件佇列等候封包到達佇列時發生。| 
|SRVPROC_SHUTDOWN |在關機處理序等候內部資源釋出以完整關機時發生。| 
|STARTUP_DEPENDENCY_MANAGER |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|TDS_BANDWIDTH_STATE |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|TDS_INIT |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|TDS_PROXY_CONTAINER |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|TEMPOBJ |在已同步處理暫存物件卸除時發生。 這種等候很罕見，只有在工作已要求 temp 資料表卸除的獨佔存取權時才會發生。| 
|TEMPORAL_BACKGROUND_PROCEED_CLEANUP |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|TERMINATE_LISTENER |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|THREADPOOL |當工作在等候工作者以供其執行時發生。 這可能表示工作者設定上限太低，或者批次執行花費的時間超乎尋常地多，因而減少了可以滿足其他批次的可用工作者數目。| 
|TIMEPRIV_TIMEPERIOD |在「擴充事件」計時器的內部同步處理期間發生。| 
|TRACE_EVTNOTIF |TBD| 
|TRACEWRITE |在 SQL 追蹤資料列集追蹤提供者等候可用緩衝區或具有待處理事件之緩衝區時發生。| 
|TRAN_MARKLATCH_DT |在交易標示閂鎖上等候終結模式閂鎖時發生。 交易標示閂鎖可用來同步處理認可與已標示交易。| 
|TRAN_MARKLATCH_EX |在已標示交易上等候獨佔模式閂鎖時發生。 交易標示閂鎖可用來同步處理認可與已標示交易。| 
|TRAN_MARKLATCH_KP |在已標示交易上等候保留模式閂鎖時發生。 交易標示閂鎖可用來同步處理認可與已標示交易。| 
|TRAN_MARKLATCH_NL |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|TRAN_MARKLATCH_SH |在已標示交易上等候共用模式閂鎖時發生。 交易標示閂鎖可用來同步處理認可與已標示交易。| 
|TRAN_MARKLATCH_UP |在已標示交易上等候更新模式閂鎖時發生。 交易標示閂鎖可用來同步處理認可與已標示交易。| 
|TRANSACTION_MUTEX |在同步處理多個批次對交易的存取作業時發生。| 
|UCS_ENDPOINT_CHANGE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|UCS_MANAGER |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|UCS_MEMORY_NOTIFICATION |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|UCS_SESSION_REGISTRATION |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|UCS_TRANSPORT |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|UCS_TRANSPORT_STREAM_CHANGE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|UTIL_PAGE_ALLOC |在交易記錄掃描在記憶體壓力下等候記憶體變成可供使用的狀態時發生。| 
|VDI_CLIENT_COMPLETECOMMAND |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|VDI_CLIENT_GETCOMMAND |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|VDI_CLIENT_OPERATION |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|VDI_CLIENT_OTHER |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|VERSIONING_COMMITTING |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|VIA_ACCEPT |當虛擬介面卡 (VIA) 提供者連接在啟動期間完成時發生。| 
|VIEW_DEFINITION_MUTEX |在同步處理快取檢視定義的存取作業時發生。| 
|WAIT_FOR_RESULTS |在等候查詢通知被觸發時發生。| 
|WAIT_SCRIPTDEPLOYMENT_REQUEST |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_SCRIPTDEPLOYMENT_WORKER |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XLOGREAD_SIGNAL |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_ASYNC_TX_COMPLETION |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_CKPT_AGENT_WAKEUP |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_CKPT_CLOSE |當等候檢查點作業完成時發生。， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_CKPT_ENABLED |啟用的已停用，並等待檢查點檢查點時，就會發生。， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_CKPT_STATE_LOCK |同步處理查看檢查點狀態時，就會發生。， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_COMPILE_WAIT |TBD <br /> **適用對象**：[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_GUEST |資料庫的記憶體配置器需要停止接收記憶體不足通知時發生。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_HOST_WAIT |Database engine 所觸發且由主機實作等候時，就會發生。， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_OFFLINE_CKPT_BEFORE_REDO |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_OFFLINE_CKPT_LOG_IO |離線檢查點正在等候記錄檔讀取 IO 完成時發生。， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_OFFLINE_CKPT_NEW_LOG |離線檢查點等候掃描新的記錄檔記錄時發生。， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_PROCEDURE_ENTRY |當卸除程序正在等候完成該程序的所有目前的執行，就會發生。， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_RECOVERY |發生於資料庫復原正在等候的記憶體最佳化的物件，以完成復原。， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_SERIAL_RECOVERY |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_SWITCH_TO_INACTIVE |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_TASK_SHUTDOWN |等候 In-memory OLTP 執行緒完成時發生。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAIT_XTP_TRAN_DEPENDENCY |等候交易相依性時，就會發生。， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAITFOR |WAITFOR TRANSACT-SQL 陳述式後，就會發生。 等候的持續時間由陳述式的參數決定。 這是使用者起始的等候。| 
|WAITFOR_PER_QUEUE |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WAITFOR_TASKSHUTDOWN |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|WAITSTAT_MUTEX |在同步處理用來擴展 sys.dm_os_wait_stats 之統計資料集合的存取作業時發生。| 
|WCC |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|WINDOW_AGGREGATES_MULTIPASS |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WINFAB_API_CALL |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WINFAB_REPLICA_BUILD_OPERATION |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WINFAB_REPORT_FAULT |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|WORKTBL_DROP |在工作資料表卸除失敗之後，於重試之前暫停時發生。| 
|WRITE_COMPLETION |當寫入作業正在進行時發生。| 
|WRITELOG |在等候記錄排清完成時發生。 造成記錄排清的一般作業包括檢查點和交易認可。| 
|XACT_OWN_TRANSACTION |在等候取得交易的擁有權時發生。| 
|XACT_RECLAIM_SESSION |在等候工作階段目前的擁有者釋出工作階段擁有權時發生。| 
|XACTLOCKINFO |在同步處理交易鎖定清單的存取作業時發生。 除了交易本身之外，諸如死結偵測和鎖定移轉等作業也會在頁面分割時存取鎖定清單。| 
|XACTWORKSPACE_MUTEX |在同步處理從交易脫離的作業，以及交易之編列成員之間的資料庫鎖定數目時發生。| 
|XDB_CONN_DUP_HASH |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XDES_HISTORY |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XDES_OUT_OF_ORDER_LIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XDES_SNAPSHOT |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XDESTSVERMGR |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XE_BUFFERMGR_ALLPROCESSED_EVENT |當擴充的事件工作階段緩衝區排清至目標時發生。 這項等候發生在背景執行緒中。| 
|XE_BUFFERMGR_FREEBUF_EVENT |當下列其中一個條件成立時發生：| 
|XE_CALLBACK_LIST |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XE_CX_FILE_READ |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XE_DISPATCHER_CONFIG_SESSION_LIST |當使用非同步目標的擴充的事件工作階段啟動或停止時發生。 這個等候表示下列其中一個狀況：| 
|XE_DISPATCHER_JOIN |當用於擴充的事件工作階段的背景執行緒結束時發生。| 
|XE_DISPATCHER_WAIT |當用於擴充的事件工作階段的背景執行緒正在等候事件緩衝區處理時發生。| 
|XE_FILE_TARGET_TVF |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XE_LIVE_TARGET_TVF |TBD <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XE_MODULEMGR_SYNC |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|XE_OLS_LOCK |僅供參考之用。 不支援。 我們無法保證未來的相容性。| 
|XE_PACKAGE_LOCK_BACKOFF |僅供參考之用。 不支援。 <br /> **適用於**:[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]只。 |  
|XE_SERVICES_EVENTMANUAL |TBD| 
|XE_SERVICES_MUTEX |TBD| 
|XE_SERVICES_RWLOCK |TBD| 
|XE_SESSION_CREATE_SYNC |TBD| 
|XE_SESSION_FLUSH |TBD| 
|XE_SESSION_SYNC |TBD| 
|XE_STM_CREATE |TBD| 
|XE_TIMER_EVENT |TBD| 
|XE_TIMER_MUTEX |TBD| 
|XE_TIMER_TASK_DONE |TBD| 
|XIO_CREDENTIAL_MGR_RWLOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XIO_CREDENTIAL_RWLOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XIO_EDS_MGR_RWLOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XIO_EDS_RWLOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XIO_IOSTATS_BLOBLIST_RWLOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XIO_IOSTATS_FCBLIST_RWLOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XIO_LEASE_RENEW_MGR_RWLOCK |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTP_HOST_DB_COLLECTION |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTP_HOST_LOG_ACTIVITY |TBD <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTP_HOST_PARALLEL_RECOVERY |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTP_PREEMPTIVE_TASK |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTP_TRUNCATION_LSN |TBD <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTPPROC_CACHE_ACCESS |存取所有的原生編譯的預存程序快取物件，就會發生。， <br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
|XTPPROC_PARTITIONED_STACK_CREATE |配置每個 NUMA 節點的原生編譯預存程序快取結構 （必須以單一執行緒） 特定程序時，就會發生。， <br /> **適用於**： [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|

  
 下列 Xevent 與資料分割相關**交換器**和線上索引重建。 如需語法的詳細資訊，請參閱 < [ALTER TABLE &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-table-transact-sql.md)和[ALTER INDEX &#40;-&#41;](../../t-sql/statements/alter-index-transact-sql.md)。  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 如需鎖定相容性矩陣，請參閱[sys.dm_tran_locks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
    
 [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_session_wait_stats &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)   
 [sys.dm_db_wait_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-wait-stats-azure-sql-database.md)  
  
  


