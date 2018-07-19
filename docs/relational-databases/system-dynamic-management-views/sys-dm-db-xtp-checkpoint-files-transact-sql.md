---
title: sys.dm_db_xtp_checkpoint_files (TRANSACT-SQL) |Microsoft Docs
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_files
- sys.dm_db_xtp_checkpoint_files_TSQL
- dm_db_xtp_checkpoint_files_TSQL
- sys.dm_db_xtp_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_files dynamic management view
ms.assetid: ac8e6333-7a9f-478a-b446-5602283e81c9
caps.latest.revision: 49
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c4ad13459024604d748c1dac8a6649c09a53f10f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38005740"
---
# <a name="sysdmdbxtpcheckpointfiles-transact-sql"></a>sys.dm_db_xtp_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  顯示有關檢查點檔案的資訊，包括檔案大小、實體位置及交易識別碼。  
  
> **注意︰** 未關閉，[狀態] 欄位為 s 的現行檢查點`ys.dm_db_xtp_checkpoint_files`會是 「 建構中的新檔案。 檢查點會自動關閉時沒有足夠的交易記錄成長，因為最後一個檢查點，或者如果您發出`CHECKPOINT`命令 ([檢查點&#40;TRANSACT-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md))。  
  
 記憶體最佳化檔案群組在內部會使用僅附加的檔案儲存於記憶體中資料表的插入和刪除資料列。 有兩種檔案類型： 資料檔案包含插入的資料列，而差異檔案則包含刪除的資料列的參考。 
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 本質上不同於較新版本，在主題中較低討論[SQL Server 2014](#bkmk_2014)。  
  
 如需詳細資訊，請參閱 <<c0> [ 建立及管理記憶體最佳化物件的儲存體](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)。  
  
##  <a name="bkmk_2016"></a> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 和更新版本  
 下表描述的資料行`sys.dm_db_xtp_checkpoint_files`，與開頭**[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]**。  
  
|資料行名稱|類型|描述|  
|-----------------|----------|-----------------|  
|container_id|**int**|資料或差異檔案所屬之容器的識別碼 (以 sys.database_files 中的 FILESTREAM 類型檔案來表示)。 與中的 file_id 聯結[sys.master_files &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)。|  
|container_guid|**uniqueidentifier**|容器，即根、 資料或差異檔案組件的 GUID。 與 file_guid sys.database_files 資料表中的聯結。|  
|checkpoint_file_id|**uniqueidentifier**|檢查點檔案的 GUID。|  
|relative_file_path|**nvarchar(256)**|相對於對應至容器之檔案的路徑。|  
|file_type|**smallint**|免費的-1<br /><br /> 0 表示資料檔案。<br /><br /> 1 代表差異檔案。<br /><br /> 2 代表根檔案<br /><br /> 3 個大型資料檔案|  
|file_type_desc|**nvarchar(60)**|維護為可用的免費全部檔案可供配置。 可用的檔案可以根據預期需求的大小因系統。 大小上限為 1 GB。<br /><br /> 資料-資料檔案包含已插入至記憶體最佳化資料表的資料列。<br /><br /> 差異-差異檔案會包含已刪除的資料檔案中的資料列的參考。<br /><br /> 根目錄-根檔案包含系統中繼資料的記憶體最佳化和原生編譯的物件。<br /><br /> 大型的資料-大型資料檔案包含的值插入 （varchar 和 varbinary （max） 資料行，以及屬於記憶體最佳化資料表上的資料行存放區索引的資料行區段。|  
|internal_storage_slot|**int**|內部儲存體陣列中之檔案的索引。 NULL 根或 1 以外的狀態。|  
|checkpoint_pair_file_id|**uniqueidentifier**|對應的資料或差異檔案。 根是 NULL。|  
|file_size_in_bytes|**bigint**|在磁碟上檔案的大小。|  
|file_size_used_in_bytes|**bigint**|針對仍在擴展的檢查點檔案組，這個資料行會在下一個檢查點之後更新。|  
|logical_row_count|**bigint**|針對資料，插入的資料列數目。<br /><br /> 差異，刪除的資料列數目之後卸除資料表。<br /><br /> 根目錄中，為 NULL。|  
|state|**smallint**|0 – 已預先建立<br /><br /> 1-在建構<br /><br /> 2 - 使用中<br /><br /> 3 – 合併目標<br /><br /> 8-等候記錄截斷|  
|state_desc|**nvarchar(60)**|預先建立 – 檢查點檔案數目會最小化，或減少任何等候配置新檔案，當交易正在執行預先配置。 這些預先建立的檔案大小會根據預估工作負載的需求而有所不同，但不包含任何資料。 這是在資料庫具有 MEMORY_OPTIMIZED_DATA 檔案群組中的儲存體額外負荷。<br /><br /> 在建構-這些檢查點檔案建構，這表示它們會根據資料庫中，所產生的記錄檔記錄正在填入且其尚未檢查點的一部分。<br /><br /> 使用中-包含從先前已關閉的檢查點的插入/刪除資料列。 它們包含由區域讀入記憶體之前套用在資料庫重新啟動的交易記錄的使用中部分的資料表的內容。 這些是記憶體中大小的記憶體最佳化的資料表，假設合併作業的大約 2 倍跟交易式工作負載的檢查點檔案的大小預計。<br /><br /> 合併目標 – 合併作業-這些檢查點檔案的目標儲存已識別的合併原則的來源檔案的彙總的資料列。 一旦安裝合併之後，「合併目標」就會轉換為「使用中」狀態。<br /><br /> 等候記錄截斷 – 一旦安裝合併和合併目標 CFP 為持久性檢查點，合併來源檢查點檔案轉換，到這個狀態的一部分。 此狀態中的檔案所需的記憶體最佳化資料表的資料庫作業的正確性。  例如，若要從持久性檢查點復原來回到過去。|  
|lower_bound_tsn|**bigint**|在檔案中; 交易的下限如果狀態不是位於 （1，3） 為 null。|  
|upper_bound_tsn|**bigint**|在檔案中; 交易的上限如果狀態不是位於 （1，3） 為 null。|  
|begin_checkpoint_id|**bigint**|開始檢查點的識別碼。|  
|end_checkpoint_id|**bigint**|結束檢查點的識別碼。|  
|last_updated_checkpoint_id|**bigint**|更新此檔案的最後一個檢查點的識別碼。|  
|encryption_status|**smallint**|0, 1, 2|  
|encryption_status_desc|**nvarchar(60)**|0 = &GT; UNENCRTPTED<br /><br /> 1 = &GT; 金鑰 1 加密<br /><br /> 2 = &GT; 使用金鑰 2 加密。 僅適用於使用中的檔案。|  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 下表描述的資料行`sys.dm_db_xtp_checkpoint_files`，如**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**。  
  
|資料行名稱|類型|描述|  
|-----------------|----------|-----------------|  
|container_id|**int**|資料或差異檔案所屬之容器的識別碼 (以 sys.database_files 中的 FILESTREAM 類型檔案來表示)。 與中的 file_id 聯結[sys.master_files &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)。|  
|container_guid|**uniqueidentifier**|資料或差異檔案所屬之容器的 GUID。|  
|checkpoint_file_id|**GUID**|資料或差異檔案的識別碼。|  
|relative_file_path|**nvarchar(256)**|資料或差異檔案的路徑 (相對於容器的位置)。|  
|file_type|**tinyint**|0 代表資料檔案。<br /><br /> 1 代表差異檔案。<br /><br /> 如果 state 資料行設定為 7 則為 NULL。|  
|file_type_desc|**nvarchar(60)**|檔案類型： DATA_FILE、 delta_file，如果 state 資料行設定為 7 則為 NULL。|  
|internal_storage_slot|**int**|內部儲存體陣列中之檔案的索引。 如果 state 資料行不是 2 或 3 則為 NULL。|  
|checkpoint_pair_file_id|**uniqueidentifier**|對應的資料或差異檔案。|  
|file_size_in_bytes|**bigint**|使用的檔案大小。 如果 state 資料行設定為 5、6 或 7 則為 NULL。|  
|file_size_used_in_bytes|**bigint**|所使用之檔案的使用大小。 如果 state 資料行設定為 5、6 或 7 則為 NULL。<br /><br /> 針對仍在擴展的檢查點檔案組，這個資料行會在下一個檢查點之後更新。|  
|inserted_row_count|**bigint**|資料檔案中的資料列數。|  
|deleted_row_count|**bigint**|差異檔案中已刪除的資料列數。|  
|drop_table_deleted_row_count|**bigint**|資料檔案中受到卸除資料表影響的資料列數目。 當 state 資料行等於 1 時，適用於資料檔案。<br /><br /> 顯示已卸除的資料表中刪除的資料列計數。 在完成已卸除之資料表中資料列的記憶體回收及取得檢查點之後，就會編譯 drop_table_deleted_row_count 統計資料。 如果您在卸除資料表統計資料反映於這個資料行之前重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，統計資料將會在復原期間更新。 復原程序不會從已卸除的資料表中載入資料列。 載入階段會編譯已卸除之資料表的統計資料，並在復原完成時於這個資料行中報告。|  
|state|**int**|0 – 已預先建立<br /><br /> 1 – 建構中<br /><br /> 2 - 使用中<br /><br /> 3 – 合併目標<br /><br /> 4 – 已合併來源<br /><br /> 5 – 備份/高可用性所需<br /><br /> 6 – 正在轉換為標記<br /><br /> 7 – 標記|  
|state_desc|**nvarchar(60)**|已預先建立 – 又稱為檢查點檔案組 (CFP) 的一小組資料和差異檔案組會維持預先配置狀態，如此一來，當交易正在執行時，就可移除或減少任何等候配置新檔案的情形。 其為配置全額，即資料檔案大小為 128MB 且差異檔案大小為 8 MB 但不含資料。 CFP 數目是依邏輯處理器或排程器的數目來計算 (每個核心一個，無上限)，最少為 8 個。 這是具有記憶體最佳化資料表的資料庫固定的儲存負擔。<br /><br /> 建構中 – 上一次檢查點之後用來儲存新插入而且可能已刪除之資料列的 CFP 集合。<br /><br /> 使用中 - 包含來自先前已關閉之檢查點的已插入和刪除的資料列。 這些 CFP 包含了在資料庫重新啟動時套用交易記錄的使用中部分之前所需的所有已插入和刪除的資料列。 這些 CFP 的大小大約是記憶體最佳化資料表的記憶體中大小的兩倍，前提是合併作業透過交易式工作負載維持在最新狀態。<br /><br /> 合併目標 – CFP 會儲存 CFP 中由合併原則所識別的合併資料列。 一旦安裝合併之後，「合併目標」就會轉換為「使用中」狀態。<br /><br /> 已合併來源 – 一旦安裝合併作業之後，來源 CFP 就會標示為「已合併來源」。 請注意，合併原則評估工具可識別多個合併，但是 CFP 只能參與一個合併作業。<br /><br /> 備份/高可用性所需 – 一旦安裝了合併而且合併目標 CFP 為持久性檢查點的一部分時，合併來源 CFP 就會轉換到這個狀態。 包含記憶體最佳化資料表的資料庫需要這個狀態下的 CFP 來確定其作業的正確性。  例如，若要從持久性檢查點復原來回到過去。 CFP 要等到記錄截斷點移出其交易範圍後才可標示為記憶體回收。<br /><br /> 正在轉換為標記 – 記憶體中的 OLTP 引擎不需要這些 CFP，而且可以為其進行記憶體回收。 此狀態表示這些 CFP 正在等候背景執行緒將其轉換到下一個狀態，也就是「標記」。<br /><br /> 標記 – 這些 CFP 正在等候由 FILESTREAM 記憶體回收行程進行記憶體回收。 ([sp_filestream_force_garbage_collection &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md))|  
|lower_bound_tsn|**bigint**|檔案中包含之交易的下限。 如果 state 資料行不是 2、3 或 4 則為 Null。|  
|upper_bound_tsn|**bigint**|檔案中包含之交易的上限。 如果 state 資料行不是 2、3 或 4 則為 Null。|  
|last_backup_page_count|**int**|上一次備份所決定的邏輯頁計數。 當 state 資料行設定為 2、3、4 或 5 時適用。 如果頁面計數未知則為 NULL。|  
|delta_watermark_tsn|**int**|寫入至這個差異檔案之上一次檢查點的交易。 這是差異檔案的標準。|  
|last_checkpoint_recovery_lsn|**nvarchar(23)**|仍然需要此檔案之上一次檢查點的復原記錄序號 (LSN)。|  
|tombstone_operation_lsn|**nvarchar(23)**|一旦 tombstone_operation_lsn 落後記錄截斷記錄檔序號，這個檔案就會遭到刪除。|  
|logical_deletion_log_block_id|**bigint**|僅適用於狀態 5。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 `VIEW DATABASE STATE` 權限。  
  
## <a name="use-cases"></a>使用案例  
 您可以估計，如下所示使用記憶體內部 OLTP 的儲存體：  
  
```  
-- total storage used by In-Memory OLTP  
SELECT SUM (file_size_in_bytes)/(1024*1024) as file_size_in_MB  
FROM sys.dm_db_xtp_checkpoint_files  
```  
  
  
若要執行下列查詢的狀態和檔案類型的儲存體使用率的細目，請參閱：
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(file_size_in_bytes) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  

  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化的資料表動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
