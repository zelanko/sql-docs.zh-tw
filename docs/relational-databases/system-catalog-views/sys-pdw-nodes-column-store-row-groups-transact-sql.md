---
title: 'pdw_nodes_column_store_row_groups (Transact-sql) '
ms.custom: seo-dt-2019
ms.date: 08/05/2020
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 17a4c925-d4b5-46ee-9cd6-044f714e6f0e
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 88dd890b9d3f691fa671916b34daf8b2258aa2bc
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823903"
---
# <a name="syspdw_nodes_column_store_row_groups-transact-sql"></a>pdw_nodes_column_store_row_groups (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  提供每個區段的叢集資料行存放區索引資訊，以協助系統管理員在中進行系統管理決策 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。 **pdw_nodes_column_store_row_groups**具有實際儲存 (（包括標示為已) 刪除的資料列總數）的資料行，以及標示為已刪除之資料列數目的資料行。 請使用**pdw_nodes_column_store_row_groups**來判斷哪些資料列群組具有較高百分比的已刪除資料列，而且應該重建。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|object_id|**int**|基礎資料表的識別碼。 這是計算節點上的實體資料表，而不是控制節點上邏輯資料表的 object_id。 例如，object_id 與 sys.databases 中的 object_id 不相符。<br /><br /> 若要與 sys.databases 聯結，請使用 sys.databases pdw_index_mappings。|  
|**index_id**|**int**|*Object_id*資料表上叢集資料行存放區索引的識別碼。|  
|**partition_number**|**int**|保留資料列群組*row_group_id*之資料表資料分割的識別碼。 您可以使用*partition_number*將此 DMV 加入至 sys.databases。|  
|**row_group_id**|**int**|此資料列群組的識別碼。 此號碼在分割區中是唯一的。|  
|**dellta_store_hobt_id**|**bigint**|差異資料列群組的 hobt_id，如果資料列群組類型不是差異，則為 NULL。 差異資料列群組是讀取/寫入資料列群組，可接受新記錄。 差異資料列群組具有 [**開啟**] 狀態。 差異資料列群組仍採用資料列存放區格式，且尚未壓縮為資料行存放區格式。|  
|**state**|**tinyint**|與 state_description 相關聯的識別碼。<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED|  
|**state_desccription**|**nvarchar(60)**|資料列群組的持續狀態描述：<br /><br /> 開啟-接受新記錄的讀取/寫入資料列群組。 開啟的資料列群組仍採用資料列存放區格式，且尚未壓縮為資料行存放區格式。<br /><br /> CLOSED-已填滿但尚未由元組移動程式壓縮的資料列群組。<br /><br /> 已壓縮-已填滿和壓縮的資料列群組。|  
|**total_rows**|**bigint**|實際儲存在資料列群組中的總列數。 有些可能已刪除，但是仍然保存。 資料列群組中資料列數目的上限為 1,048,576 (十六進位 FFFFF)。|  
|**deleted_rows**|**bigint**|實際儲存在標示為要刪除之資料列群組中的資料列數目。<br /><br /> 差異資料列群組一律為0。|  
|**size_in_bytes**|**int**|此資料列群組中所有頁面的組合大小（以位元組為單位）。 此大小不包含儲存中繼資料或共用字典所需的大小。|  
|**pdw_node_id**|**int**|節點的唯一識別碼 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。|  
|**distribution_id**|**int**|散發的唯一識別碼。|
  
## <a name="remarks"></a>備註  
 針對擁有叢集或非叢集資料行存放區索引的每一個資料表的每一個資料行存放區資料列群組傳回一個資料列。  
  
 請使用**pdw_nodes_column_store_row_groups**來判斷資料列群組中包含的資料列數，以及資料列群組的大小。  
  
 當資料列群組中已刪除的資料列數增加到佔總列數的相當大比例時，資料表的效率就會降低。 重建資料行存放區索引可縮小資料表，減少讀取資料表所需的磁碟 I/O。 若要重建資料行存放區索引，請使用**ALTER index**語句的**rebuild**選項。  
  
 可更新的資料行存放區會先將新資料插入**開啟**的資料列群組（格式為 rowstore），有時也稱為差異資料表。  開啟的資料列群組填滿後，其狀態會變更為 [**已關閉**]。 已關閉的資料列群組會由元組移動器壓縮為數據行存放區格式，而狀態會變更為 [已**壓縮**  Tuple Mover 是背景處理序，會定期喚醒並檢查是否有任何準備好壓縮為資料行存放區資料列群組的關閉資料列群組。  Tuple Mover 也會取消配置其中所有資料列都已刪除的任何資料列群組。 已解除配置的資料列群組會標示為已**淘汰**。 若要立即執行元組移動器，請使用**ALTER INDEX**語句的 [重新**組織**] 選項。  
  
 當資料行存放區資料列群組已滿時，就會進行壓縮，並停止接受新的資料列。 資料列從壓縮的群組中刪除時仍會持續存在，但會標示為已刪除。 對壓縮的群組進行更新的實作方式，是從壓縮的群組中刪除，然後插入開啟的群組。  
  
## <a name="permissions"></a>權限  
 需要 **VIEW SERVER STATE** 權限。  
  
## <a name="examples-sssdw-and-sspdw"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會將**sys.databases pdw_nodes_column_store_row_groups**資料表聯結至其他系統資料表，以傳回特定資料表的相關資訊。 導出的 `PercentFull` 資料行是資料列群組的效率預估。 若要尋找單一資料表上的資訊，請移除 WHERE 子句前面的批註連字號，並提供資料表名稱。  
  
```sql
SELECT IndexMap.object_id,   
  object_name(IndexMap.object_id) AS LogicalTableName,   
  i.name AS LogicalIndexName, IndexMap.index_id, NI.type_desc,   
  IndexMap.physical_name AS PhyIndexNameFromIMap,   
  CSRowGroups.*,  
  100*(ISNULL(deleted_rows,0))/total_rows AS PercentDeletedRows   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.pdw_index_mappings AS IndexMap  
    ON i.object_id = IndexMap.object_id  
    AND i.index_id = IndexMap.index_id  
JOIN sys.pdw_nodes_indexes AS NI  
    ON IndexMap.physical_name = NI.name  
    AND IndexMap.index_id = NI.index_id  
JOIN sys.pdw_nodes_column_store_row_groups AS CSRowGroups  
    ON CSRowGroups.object_id = NI.object_id   
    AND CSRowGroups.pdw_node_id = NI.pdw_node_id  
    AND CSRowGroups.index_id = NI.index_id      
WHERE total_rows > 0
--WHERE t.name = '<table_name>'   
ORDER BY object_name(i.object_id), i.name, IndexMap.physical_name, pdw_node_id;  
```  

下列範例會計算叢集資料行存放 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 區的每個資料分割，以及開啟、關閉或壓縮資料列群組中的資料列數目：  

```sql
SELECT
    s.name AS [Schema Name]
    ,t.name AS [Table Name]
    ,rg.partition_number AS [Partition Number]
    ,SUM(rg.total_rows) AS [Total Rows]
    ,SUM(CASE WHEN rg.State = 1 THEN rg.Total_rows Else 0 END) AS [Rows in OPEN Row Groups]
    ,SUM(CASE WHEN rg.State = 2 THEN rg.Total_Rows ELSE 0 END) AS [Rows in Closed Row Groups]
    ,SUM(CASE WHEN rg.State = 3 THEN rg.Total_Rows ELSE 0 END) AS [Rows in COMPRESSED Row Groups]
FROM sys.pdw_nodes_column_store_row_groups rg
  JOIN sys.pdw_nodes_tables pt
    ON rg.object_id = pt.object_id
    AND rg.pdw_node_id = pt.pdw_node_id
    AND pt.distribution_id = rg.distribution_id
  JOIN sys.pdw_table_mappings tm
    ON pt.name = tm.physical_name
  INNER JOIN sys.tables t
    ON tm.object_id = t.object_id
  INNER JOIN sys.schemas s
    ON t.schema_id = s.schema_id
GROUP BY s.name, t.name, rg.partition_number
ORDER BY 1, 2
```
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [建立資料行存放區索引 &#40;Transact-sql&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [pdw_nodes_column_store_segments &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [pdw_nodes_column_store_dictionaries &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
  
