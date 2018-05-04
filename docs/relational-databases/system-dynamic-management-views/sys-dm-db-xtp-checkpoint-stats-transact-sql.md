---
title: sys.dm_db_xtp_checkpoint_stats (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_stats
- dm_db_xtp_checkpoint_stats_TSQL
- sys.dm_db_xtp_checkpoint_stats
- sys.dm_db_xtp_checkpoint_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_stats dynamic management view
ms.assetid: 8d0b18ca-db4d-4376-9905-3e4457727c46
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 76173cf1247f13d7f900b0a98bb19cc79c40cb9c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmdbxtpcheckpointstats-transact-sql"></a>sys.dm_db_xtp_checkpoint_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  傳回有關目前資料庫的記憶體中 OLTP 檢查點作業的統計資料。 如果資料庫沒有記憶體中 OLTP 物件，則傳回空的結果集。  
  
 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
```  
SELECT * FROM db.sys.dm_db_xtp_checkpoint_stats;  
```  
  
**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 本質上與較新的版本不同，會在主題中的較低討論[SQL Server 2014](#bkmk_2014)。**
  
## <a name="includesssql15includessssql15-mdmd-and-later"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及更新版本  
 下表描述的資料行`sys.dm_db_xtp_checkpoint_stats`開始**[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]**。  
  
|資料行名稱|類型|Description|  
|-----------------|----------|-----------------|  
|last_lsn_processed|**bigint**|控制器所看到的最後一個 LSN。|  
|end_of_log_lsn|**numeric(38)**|記錄檔結束 LSN。|  
|bytes_to_end_of_log|**bigint**|記錄未處理的控制站，對應至不同的位元組的位元組`last_lsn_processed`和`end_of_log_lsn`。|  
|log_consumption_rate|**bigint**|交易記錄檔的耗用量 （以 KB/秒） 控制站的速率。|  
|active_scan_time_in_ms|**bigint**|正在掃描交易記錄檔中的控制站所花費的時間。|  
|total_wait_time_in_ms|**bigint**|控制器的累計等候時間時不會掃描記錄檔。|  
|waits_for_io|**bigint**|等候記錄 IO 控制器執行緒所造成的數目。|  
|io_wait_time_in_ms|**bigint**|等候記錄 IO 控制器執行緒所花費的累計時間。|  
|waits_for_new_log_count|**bigint**|要產生新的記錄檔的控制器執行緒所造成的等候次數。|  
|new_log_wait_time_in_ms|**bigint**|控制器執行緒等候新記錄檔所花費的累計時間。|  
|idle_attempts_count|**bigint**|控制器已轉換為閒置狀態的次數。|  
|tx_segments_dispatched|**bigint**|看到控制器，並分派至序列化程式的區段數目。 區段是連續記錄的部分構成序列化的單位。 它目前的大小調整成 1 MB，但可以在未來變更。|  
|segment_bytes_dispatched|**bigint**|資料庫重新啟動之後，由序列化程式，以控制站分派位元組的總位元組計數。|  
|bytes_serialized|**bigint**|序列化，因為資料庫重新啟動的位元組總數。|  
|serializer_user_time_in_ms|**bigint**|在使用者模式中的序列化程式所花費的時間。|  
|serializer_kernel_time_in_ms|**bigint**|在核心模式中的序列化程式所花費的時間。|  
|xtp_log_bytes_consumed|**bigint**|從資料庫重新啟動以來耗用的記錄檔位元組總數。|  
|checkpoints_closed|**bigint**|資料庫重新啟動之後，已關閉的檢查點計數。|  
|last_closed_checkpoint_ts|**bigint**|最近已關閉的檢查點的時間戳記。|  
|hardened_recovery_lsn|**numeric(38)**|復原會從這個 LSN 開始。|  
|hardened_root_file_guid|**uniqueidentifier**|因為最後一個已完成檢查點強行寫入的根檔案的 GUID。|  
|hardened_root_file_watermark|**bigint**|**內部只**。 正值是有效的最多讀取根檔案 （這是內部相關只對型別 – 呼叫 BSN）。|  
|hardened_truncation_lsn|**numeric(38)**|截斷點的 LSN。|  
|log_bytes_since_last_close|**bigint**|從最後一個位元組會關閉目前的記錄結尾。|  
|time_since_last_close_in_ms|**bigint**|自上次關閉的檢查點的時間。|  
|current_checkpoint_id|**bigint**|目前新的區段會被指派給這個檢查點。 檢查點系統是管線。 目前的檢查點是要指派給記錄檔中的區段。 一旦它已達到限制，檢查點會依控制站和一個新建立為目前釋出。|  
|current_checkpoint_segment_count|**bigint**|區段中目前的檢查點的計數。|  
|recovery_lsn_candidate|**bigint**|**只有在內部**。 要挑選為 recoverylsn current_checkpoint_id 關閉時的候選。|  
|outstanding_checkpoint_count|**bigint**|在等候關閉管線中的檢查點的數目。|  
|closing_checkpoint_id|**bigint**|關閉檢查點的識別碼。<br /><br /> 序列化程式會使用以平行方式，因此一旦完成後檢查點是由關閉執行緒即將關閉的候選項目。 但是關閉執行緒可以只關閉一次，而且它必須按照順序，因此關閉檢查點是關閉的執行緒目前正在處理的一個。|  
|recovery_checkpoint_id|**bigint**|若要復原中使用檢查點的識別碼。|  
|recovery_checkpoint_ts|**bigint**|復原檢查點的時間戳記。|  
|bootstrap_recovery_lsn|**numeric(38)**|啟動安裝程式復原 LSN。|  
|bootstrap_root_file_guid|**uniqueidentifier**|啟動安裝程式的根檔案的 GUID。|  
|internal_error_code|**bigint**|所有控制器、 關閉、 序列化和 merge 執行緒所都看到的錯誤。|
|bytes_of_large_data_serialized|**bigint**|已序列化的資料量。 |  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 下表描述的資料行`sys.dm_db_xtp_checkpoint_stats`，如**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**。  
  
|資料行名稱|類型|Description|  
|-----------------|----------|-----------------|  
|log_to_process_in_bytes|**bigint**|執行緒目前的記錄序號 (LSN) 和記錄檔結束之間的記錄位元組數目。|  
|total_log_blocks_processed|**bigint**|伺服器啟動後處理的記錄區塊總數。|  
|total_log_records_processed|**bigint**|伺服器啟動後處理的記錄檔記錄總數。|  
|xtp_log_records_processed|**bigint**|伺服器啟動後已處理的記憶體中 OLTP 記錄檔記錄的總數。|  
|total_wait_time_in_ms|**bigint**|累計等候時間 (毫秒)。|  
|waits_for_io|**bigint**|記錄 IO 等候的數目。|  
|io_wait_time_in_ms|**bigint**|花在等候記錄 IO 的累計時間。|  
|waits_for_new_log|**bigint**|等候新記錄產生的數目。|  
|new_log_wait_time_in_ms|**bigint**|花在等候新記錄的累計時間。|  
|log_generated_since_last_checkpoint_in_bytes|**bigint**|自從上次記憶體中 OLTP 檢查點之後產生的記錄檔數量。|  
|ms_since_last_checkpoint|**bigint**|自從上次記憶體中 OLTP 檢查點之後的時間量 (以毫秒為單位)。|  
|checkpoint_lsn|**numeric (38)**|與最後完成的記憶體中 OLTP 檢查點相關聯的復原記錄序號 (LSN)。|  
|current_lsn|**numeric (38)**|目前正在處理的記錄檔記錄 LSN。|  
|end_of_log_lsn|**numeric (38)**|記錄檔結束的 LSN。|  
|task_address|**varbinary(8)**|SOS_Task 的位址。 聯結 sys.dm_os_tasks 以尋找其他資訊。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 `VIEW DATABASE STATE` 權限。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化的資料表動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
