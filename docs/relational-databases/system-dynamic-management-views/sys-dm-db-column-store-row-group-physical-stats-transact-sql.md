---
title: sys.dm_db_column_store_row_group_physical_stats & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_column_store_row_group_physical_stats_TSQL
- sys.dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_db_column_store_row_group_physical_stats
- sys.dm_db_column_store_row_group_physical_stats dynamic management view
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: a6eaa2759ac911f748da143dbd592abc5de066b9
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39533848"
---
# <a name="sysdmdbcolumnstorerowgroupphysicalstats-transact-sql"></a>sys.dm_db_column_store_row_group_physical_stats & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  提供有關所有目前資料庫中的資料行存放區索引的目前資料列群組層級資訊。  
  
 這會擴充目錄檢視[sys.column_store_row_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|基礎資料表的識別碼。|  
|**index_id**|**int**|此資料行存放區索引的識別碼*object_id*資料表。|  
|**partition_number**|**int**|保存的資料表資料分割識別碼*row_group_id*。 您可以使用 partition_number 將此 DMV 聯結至 sys.partitions。|  
|**row_group_id**|**int**|此資料列群組的識別碼。 對於資料分割的資料表，這是資料分割內唯一的。<br /><br /> -1 代表一個記憶體中的尾端。|  
|**delta_store_hobt_id**|**bigint**|差異存放區中資料列群組的 hobt_id。<br /><br /> 如果資料列群組不在差異存放區，則為 NULL。<br /><br /> 記憶體中資料表的結尾是 NULL。|  
|**state**|**tinyint**|相關聯的識別碼編號*state_description*。<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED<br /><br /> 4 = 標記<br /><br /> 壓縮是唯一適用於記憶體中資料表的狀態。|  
|**state_desc**|**nvarchar(60)**|資料列群組狀態的描述：<br /><br /> 看不見 – 正在建置的資料列群組。 例如： <br />在 資料行存放區中的資料列群組時，看不進行壓縮的資料。 壓縮完成中繼資料參數變更資料行存放區資料列的狀態群組從看不見壓縮，並標記從 已關閉的差異存放區資料列群組的狀態。<br /><br /> 開啟 – 差異存放區資料列群組，可接受新的資料列。 開啟的資料列群組仍採用資料列存放區格式，且尚未壓縮為資料行存放區格式。<br /><br /> CLOSED – 在差異存放區，其中包含的資料列數目上限，並將其壓縮到資料行存放區 tuple mover 程序正在等候中的資料列群組。<br /><br /> COMPRESSED – 壓縮資料行存放區壓縮並儲存在資料行存放區中的資料列群組。<br /><br /> 標記 – 使用先前在差異存放區中，且不能的資料列群組。|  
|**total_rows**|**bigint**|資料列數目實體儲存在資料列群組。 壓縮的資料列群組，這包括標示為刪除的資料列。|  
|**deleted_rows**|**bigint**|實際儲存在壓縮的資料列群組資料列標示為刪除的數目。<br /><br /> 差異存放區中的資料列群組為 0。|  
|**size_in_bytes**|**bigint**|合併的大小，以位元組為單位，此資料列群組中的所有頁面。 這個大小不包括所需儲存中繼資料或共用的字典的大小。|  
|**trim_reason**|**tinyint**|觸發 COMPRESSED 資料列群組擁有的原因小於資料列數目上限。<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION<br /><br /> 1-NO_TRIM<br /><br /> 2-大量載入<br /><br /> 3 – REORG<br /><br /> 4-DICTIONARY_SIZE<br /><br /> 5 – MEMORY_LIMITATION<br /><br /> 6 – RESIDUAL_ROW_GROUP<br /><br /> 7-STATS_MISMATCH<br /><br /> 8-溢出|  
|**trim_reason_desc**|**nvarchar(60)**|Popis *trim_reason*。<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION： 從舊版升級時，發生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br /> 1-NO_TRIM： 不修剪資料列群組。 資料列群組壓縮的 1,048,476 的資料列的最大值。  如果關閉差異資料列群組後，已刪除的資料列的 subsset，資料列數目可能會小於<br /><br /> 2 – BULKLOAD： 大量載入批次大小限制資料列的數目。<br /><br /> 3 – REORG： 強制壓縮 REORG 命令的一部分。<br /><br /> 4-DICTIONARY_SIZE： 字典大小成長過大而無法壓縮所有資料列在一起。<br /><br /> 5 – MEMORY_LIMITATION： 沒有足夠的記憶體可壓縮所有資料列在一起。<br /><br /> 6 – RESIDUAL_ROW_GROUP： 關閉的最後一個資料列群組一部分的資料列 < 1 百萬個索引建立作業期間<br /><br /> STATS_MISMATCH： 僅適用於資料行存放區的記憶體中資料表上。 如果統計資料不正確地指定 > = 1 百萬個結尾中的合格資料列，但我們發現較少，壓縮的資料列群組會有 < 1 百萬個資料列<br /><br /> 溢出： 僅適用於資料行存放區的記憶體中資料表上。 如果結尾具有 > 1 百萬個合格的資料列，將最後一個批次的其餘資料列，壓縮如果計數為 1 百萬個 100 k 之間|  
|**transition_to_compressed_state**|TINYINT|示範如何這個資料列群組已移動從差異存放區中的資料行存放區的壓縮狀態。<br /><br /> 1-NOT_APPLICABLE<br /><br /> 2 – INDEX_BUILD<br /><br /> 3 – TUPLE_MOVER<br /><br /> 4-REORG_NORMAL<br /><br /> 5 – REORG_FORCED<br /><br /> 6-大量載入<br /><br /> 7-合併|  
|**transition_to_compressed_state_desc**|nvarchar(60)|NOT_APPLICABLE – 作業不適用於差異存放區。 或者，您也可以在升級至之前壓縮資料列群組[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]不在此情況下會保留歷程記錄。<br /><br /> INDEX_BUILD – 索引建立或重建索引會壓縮資料列群組。<br /><br /> TUPLE_MOVER – 在背景執行 tuple mover 壓縮資料列群組。 會發生這種情況後資料列群組從 已開啟狀態變更為 已關閉。<br /><br /> REORG_NORMAL – 重新組織作業，ALTER INDEX... REORG，從差異存放區的 CLOSED 資料列群組移到資料行存放區。 此 tuple mover 已開始移動資料列群組之前發生。<br /><br /> REORG_FORCED – 此資料列群組已在差異存放區中開啟，並已強制到資料行存放區中，它具有完整的數字的資料列之前。<br /><br /> BULKLOAD – 大量載入作業不直接使用差異存放區壓縮資料列群組。<br /><br /> 合併-合併作業會合併到此資料列群組的一或多個資料列群組，並接著執行 資料行存放區壓縮。|  
|**has_vertipaq_optimization**|bit|Vertipaq 最佳化會改善重新排列資料列群組中的資料列才能達到更高的壓縮的資料行存放區壓縮。 在大部分情況下，此最佳化會自動進行。 有兩種情況下，不使用 Vertipaq 最佳化：<br/>  A. 當差異資料列群組移到資料行存放區，並有一或多個非叢集索引的資料行存放區索引-在此情況下 Vertipaq 最佳化會略過以對應索引的變更降至最低<br/> B. 記憶體最佳化資料表上的資料行存放區索引。 <br /><br /> 0 = 否<br /><br /> 1 = 是|  
|**產生**|BIGINT|此資料列群組相關聯的資料列群組產生。|  
|**created_time**|datetime2|建立此資料列群組時的時鐘時間。<br /><br /> 「 NULL 」 – 在記憶體中的資料表資料行存放區索引。|  
|**closed_time**|datetime2|關閉這個資料列群組時的時鐘時間。<br /><br /> 「 NULL 」 – 在記憶體中的資料表資料行存放區索引。|  
  
## <a name="results"></a>結果  
 傳回目前資料庫中的每個資料列群組的一個資料列。  
  
## <a name="permissions"></a>Permissions  
 需要下列權限：  
  
-   在資料表上的 CONTROL 權限。  
  
-   資料庫的 VIEW DATABASE STATE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-calculate-fragmentaton-to-decide-when-to-reorganize-or-rebuild-a-columnstore-index"></a>A. 計算 fragmentaton 決定何時要重新組織或重建資料行存放區索引。  
 資料行存放區索引已刪除的資料列的百分比是很好的量值的資料列群組中的片段。 當片段是 20%或更多建議您移除已刪除的資料列。  如需範例，請參閱[資料行存放區索引重組](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)。  
  
 此範例會聯結**sys.dm_db_column_store_row_group_physical_stats**與其他系統資料表，然後計算`Fragmentation`作為目前資料庫中每個資料列群組的效率預估值的資料行。     若要尋找有關單一資料表移除註解連字號前面**其中**子句，並提供資料表名稱。  
  
```sql  
SELECT i.object_id,   
    object_name(i.object_id) AS TableName,   
    i.name AS IndexName,   
    i.index_id,   
    i.type_desc,   
    CSRowGroups.*,  
    100*(ISNULL(deleted_rows,0))/total_rows AS 'Fragmentation'  
FROM sys.indexes AS i  
JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id AND i.index_id = CSRowGroups.index_id   
-- WHERE object_name(i.object_id) = 'table_name'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [資料行存放區索引指南](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_dictionaries &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
