---
title: "sys.column_store_row_groups (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.column_store_row_groups_TSQL
- column_store_row_groups
- sys.column_store_row_groups
- column_store_row_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_row_groups catalog view
ms.assetid: 76e7fef2-d1a4-4272-a2bb-5f5dcd84aedc
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1ea17802f24a60df24fdc4107f52a5170ca4f0ea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="syscolumnstorerowgroups-transact-sql"></a>sys.column_store_row_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  提供以每個區段為基礎的叢集資料行存放區索引資訊，協助系統管理員做出系統管理決策。 **sys.column_store_row_groups**具有資料列的實際儲存 （包括標示為已刪除） 總數的資料行和資料行標示為已刪除的資料列數目。 使用**sys.column_store_row_groups**來判斷哪一個資料列群組已刪除的資料列的百分比很高，應該重建。  
   
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|定義此索引所在資料表的識別碼。|  
|**index_id**|**int**|內含此資料行存放區索引之資料表的索引識別碼。|  
|**r**|**int**|保存資料列群組 row_group_id 之資料表分割區的識別碼。 您可以使用 partition_number 將此 DMV 聯結至 sys.partitions。|  
|**row_group_id**|**int**|與此資料列群組相關聯的資料列群組號碼。 此號碼在分割區中是唯一的。<br /><br /> -1 = 記憶體中資料表的結尾。|  
|**delta_store_hobt_id**|**bigint**|差異存放區中開啟的資料列群組的 hobt_id。<br /><br /> 如果資料列群組不是差異存放區，則為 NULL。<br /><br /> 記憶體中資料表的結尾為 NULL。|  
|**狀態**|**tinyint**|與 state_description 相關聯的識別碼。<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED <br /><br /> 4 = 標記|  
|**state_description**|**nvarchar （60)**|資料列群組的持續狀態描述：<br /><br /> INVISIBLE - 正在從差異存放區中的資料建立隱藏的壓縮區段。 讀取動作將會使用差異存放區，直到不可見的壓縮區段完成為止。 然後新的區段會變成可見，並移除來源差異存放區。<br /><br /> OPEN – 讀取/寫入資料列群組，可接受新記錄。 開啟的資料列群組仍採用資料列存放區格式，且尚未壓縮為資料行存放區格式。<br /><br /> CLOSED – 已填滿但尚未壓縮 Tuple Mover 程序壓縮的資料列群組。<br /><br /> COMPRESSED – 已填滿且壓縮的資料列群組。|  
|**total_rows**|**bigint**|實際儲存在資料列群組中的總列數。 有些可能已刪除，但是仍然保存。 資料列群組中資料列數目的上限為 1,048,576 (十六進位 FFFFF)。|  
|**deleted_rows**|**bigint**|資料列群組中標示為已刪除的總列數。 DELTA 資料列群組的此值永遠為 0。|  
|**size_in_bytes**|**bigint**|DELTA 和 COLUMNSTORE 資料列群組的此資料列群組中所有資料的大小 (以位元組為單位，但不包括中繼資料或共用字典)。|  
  
## <a name="remarks"></a>備註  
 針對擁有叢集或非叢集資料行存放區索引的每一個資料表的每一個資料行存放區資料列群組傳回一個資料列。  
  
 使用**sys.column_store_row_groups**來判斷資料列群組和大小的資料列群組中包含的資料列數目。  
  
 當資料列群組中已刪除的資料列數增加到佔總列數的相當大比例時，資料表的效率就會降低。 重建資料行存放區索引可縮小資料表，減少讀取資料表所需的磁碟 I/O。 若要重建資料行存放區索引使用**重建**選項**ALTER INDEX**陳述式。  
  
 可更新的資料行存放區會先將新資料插入**開啟**資料列群組，這是資料列存放區格式，而且有時也稱為差異資料表。  一旦開啟的資料列群組已滿，其狀態會變更為**CLOSED**。 Closed 資料列群組由 tuple mover 壓縮成資料行存放區格式，並在狀態變更為**壓縮**。  Tuple Mover 是背景處理序，會定期喚醒並檢查是否有任何準備好壓縮為資料行存放區資料列群組的關閉資料列群組。  Tuple Mover 也會取消配置其中所有資料列都已刪除的任何資料列群組。 已取消配置資料列群組會標示為**標記**。 若要立即執行 tuple mover，使用**REORGANIZE**選項**ALTER INDEX**陳述式。  
  
 當資料行存放區資料列群組已滿時，就會進行壓縮，並停止接受新的資料列。 資料列從壓縮的群組中刪除時仍會持續存在，但會標示為已刪除。 對壓縮的群組進行更新的實作方式，是從壓縮的群組中刪除，然後插入開啟的群組。  
  
## <a name="permissions"></a>Permissions  
 傳回資料表的資訊，如果使用者具有**VIEW DEFINITION**資料表的權限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
 下列範例聯結**sys.column_store_row_groups**其他系統資料表，以傳回特定資料表的相關資訊的資料表。 導出的 `PercentFull` 資料行是資料列群組的效率預估。 若要尋找有關註解連字號前面的單一資料表移除**其中**子句，並提供資料表名稱。  
  
```  
SELECT i.object_id, object_name(i.object_id) AS TableName,   
i.name AS IndexName, i.index_id, i.type_desc,   
CSRowGroups.*,   
100*(total_rows - ISNULL(deleted_rows,0))/total_rows AS PercentFull    
FROM sys.indexes AS i  
JOIN sys.column_store_row_groups AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id  
AND i.index_id = CSRowGroups.index_id   
--WHERE object_name(i.object_id) = '<table_name>'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [物件目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [資料行存放區索引指南](~/relational-databases/indexes/columnstore-indexes-overview.md)     
 [sys.column_store_dictionaries &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
  

