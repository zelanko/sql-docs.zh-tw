---
title: sys.databases （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.indexes
- indexes
- sys.indexes_TSQL
- indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes catalog view
ms.assetid: 066bd9ac-6554-4297-88fe-d740de1f94a8
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 33c98b63ead78a4928b5e8dca762dee3f1a8dbaa
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "73980222"
---
# <a name="sysindexes-transact-sql"></a>sys.indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對每個表格式物件 (如資料表、檢視或資料表值函式) 索引或堆積，各包含一個資料列。  
  
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|這個索引所屬物件的識別碼。|  
|**name**|**sysname**|索引的名稱。 **name**只有在物件內才是唯一的。<br /><br /> NULL = 堆積|  
|**index_id**|**int**|索引的識別碼。 **index_id**只有在物件內才是唯一的。<br /><br /> 0 = 堆積<br /><br /> 1 = 叢集索引<br /><br /> > 1 = 非叢集索引|  
|**型別**|**tinyint**|索引的類型：<br /><br /> 0 = 堆積<br /><br /> 1 = 叢集<br /><br /> 2 = 非叢集<br /><br /> 3 = XML<br /><br /> 4 = 空間<br /><br /> 5 = 叢集資料行存放區索引。 **適用對象**：[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 及更新版本。<br /><br /> 6 = 非叢集資料行存放區索引。 **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 7 = 非叢集雜湊索引。 **適用對象**：[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 及更新版本。|  
|**type_desc**|**nvarchar(60)**|索引類型的描述：<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> XML<br /><br /> SPATIAL<br /><br /> 叢集資料行存放區-**適用于**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和更新版本。<br /><br /> 非叢集資料行存放區-**適用于**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本。<br /><br /> 非叢集雜湊：只有記憶體優化資料表支援非叢集雜湊索引。 sys.hash_indexes 檢視表顯示目前雜湊索引和雜湊屬性。 如需詳細資訊，請參閱[sys.databases &#40;。 hash_indexes transact-sql&#41;](../../relational-databases/system-catalog-views/sys-hash-indexes-transact-sql.md)。 **適用對象**：[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 及更新版本。|  
|**is_unique**|**bit**|1 = 索引是唯一的。<br /><br /> 0 = 索引不是唯一的。<br /><br /> 永遠是 0，表示叢集資料行存放區索引。|  
|**data_space_id**|**int**|這個索引的資料空間識別碼。 資料空間是一個檔案群組或分割區結構描述。<br /><br /> 0 = **object_id**是資料表值函數或記憶體中的索引。|  
|**ignore_dup_key**|**bit**|1 = IGNORE_DUP_KEY 是 ON。<br /><br /> 0 = IGNORE_DUP_KEY 是 OFF。|  
|**is_primary_key**|**bit**|1 = 索引是 PRIMARY KEY 條件約束的一部分。<br /><br /> 永遠是 0，表示叢集資料行存放區索引。|  
|**is_unique_constraint**|**bit**|1 = 索引是 UNIQUE 條件約束的一部分。<br /><br /> 永遠是 0，表示叢集資料行存放區索引。|  
|**fill_factor**|**tinyint**|> 0 = 建立或重建索引時所使用的 FILLFACTOR 百分比。<br /><br /> 0 = 預設值<br /><br /> 永遠是 0，表示叢集資料行存放區索引。|  
|**is_padded**|**bit**|1 = PADINDEX 是 ON。<br /><br /> 0 = PADINDEX 是 OFF。<br /><br /> 永遠是 0，表示叢集資料行存放區索引。|  
|**is_disabled**|**bit**|1 = 索引已停用。<br /><br /> 0 = 索引未停用。|  
|**is_hypothetical**|**bit**|1 = 索引是假設的，無法直接當作資料存取路徑來使用。 假設的索引用來存放資料行層級的統計資料。<br /><br /> 0 = 索引不是假設的。|  
|**allow_row_locks**|**bit**|1 = 索引允許資料列鎖定。<br /><br /> 0 = 索引不允許資料列鎖定。<br /><br /> 永遠是 0，表示叢集資料行存放區索引。|  
|**allow_page_locks**|**bit**|1 = 索引允許頁面鎖定。<br /><br /> 0 = 索引不允許頁面鎖定。<br /><br /> 永遠是 0，表示叢集資料行存放區索引。|  
|**has_filter**|**bit**|1 = 索引有篩選，而且只包含滿足篩選定義的資料列。<br /><br /> 0 = 索引沒有篩選。|  
|**filter_definition**|**nvarchar(max)**|包含在已篩選之索引內的資料列子集運算式。<br /><br /> NULL 代表堆積或非篩選的索引。|  
|**auto_created**|**bit**|1 = 索引是由自動調整所建立。<br /><br />0 = 索引是由使用者所建立。
|**optimize_for_sequential_key**|**bit**|1 = 索引已啟用最後頁面插入優化。<br><br>0 = 預設值。 索引已停用最後頁面的插入優化。|

  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中 `Production.Product` 資料表的所有索引。  
  
```  
  
SELECT i.name AS index_name  
    ,i.type_desc  
    ,is_unique  
    ,ds.type_desc AS filegroup_or_partition_scheme  
    ,ds.name AS filegroup_or_partition_scheme_name  
    ,ignore_dup_key  
    ,is_primary_key  
    ,is_unique_constraint  
    ,fill_factor  
    ,is_padded  
    ,is_disabled  
    ,allow_row_locks  
    ,allow_page_locks  
FROM sys.indexes AS i  
INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
WHERE is_hypothetical = 0 AND i.index_id <> 0   
AND i.object_id = OBJECT_ID('Production.Product');  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [key_constraints &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.partition_schemes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
