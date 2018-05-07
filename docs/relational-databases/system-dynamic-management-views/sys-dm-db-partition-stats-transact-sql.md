---
title: sys.dm_db_partition_stats (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_partition_stats
- dm_db_partition_stats_TSQL
- sys.dm_db_partition_stats_TSQL
- sys.dm_db_partition_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_partition_stats dynamic management view
ms.assetid: 9db9d184-b3a2-421e-a804-b18ebcb099b7
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1d59bf08d70a59dedae4ae940c810d70dba0f6c4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmdbpartitionstats-transact-sql"></a>sys.dm_db_partition_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對目前資料庫中的每個資料分割，各傳回其頁面和資料列計數資訊。  
  
> [!NOTE]  
>  若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_db_partition_stats**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|資料分割的識別碼。 在資料庫中，這是唯一的。 這是相同的值**sys.partitions**中**sys.partitions**目錄檢視|  
|**object_id**|**int**|資料分割所屬資料表或索引檢視的物件識別碼。|  
|**index_id**|**int**|資料分割所屬之堆積或索引的識別碼。<br /><br /> 0 = 堆積<br /><br /> 1 = 叢集索引。<br /><br /> > 1 = 非叢集索引|  
|**partition_number**|**int**|在索引或堆積內，以 1 為基底的資料分割編號。|  
|**in_row_data_page_count**|**bigint**|這個資料分割中用來儲存同資料列資料的頁數。 如果資料分割屬於堆積，這個值是堆積中的資料頁數。 如果資料分割屬於索引，這個值是分葉層級中的頁數。 (計數不包含 B 型樹狀目錄中的非分葉頁數。)以上兩種情況均不包含 IAM (索引配置對應) 頁數。 xVelocity 記憶體最佳化的資料行存放區索引之 Always 0。|  
|**in_row_used_page_count**|**bigint**|這個資料分割中用來儲存和管理同資料列資料的總頁數。 這個計數包括非分葉 B 型樹狀目錄頁數、 IAM 頁數，以及包含在所有頁面**in_row_data_page_count**資料行。 永遠是 0，表示資料行存放區索引。|  
|**in_row_reserved_page_count**|**bigint**|這個資料分割中為儲存和管理同資料列資料所保留的總頁數，不管這些頁面是否正在使用中。 永遠是 0，表示資料行存放區索引。|  
|**lob_used_page_count**|**bigint**|用來儲存和管理之資料列中的頁數**文字**， **ntext**，**映像**， **varchar （max)**， **nvarchar(max)**， **varbinary （max)**，和**xml**資料分割內的資料行。 IAM 頁數包括在內。<br /><br /> 資料分割中用來儲存和管理資料行存放區索引的 LOB 總數。|  
|**lob_reserved_page_count**|**bigint**|總頁數保留儲存和管理資料列外**文字**， **ntext**，**映像**， **varchar （max)**， **nvarchar （max)**， **varbinary （max)**，和**xml**磁碟分割，不論這些頁面是否正在使用中或不內的資料行。 IAM 頁數包括在內。<br /><br /> 保留在資料分割中儲存和管理資料行存放區索引的 LOB 總數。|  
|**row_overflow_used_page_count**|**bigint**|用來儲存和管理資料列溢位中的頁數**varchar**， **nvarchar**， **varbinary**，和**sql_variant**資料行資料分割。 IAM 頁數包括在內。<br /><br /> 永遠是 0，表示資料行存放區索引。|  
|**row_overflow_reserved_page_count**|**bigint**|總頁數保留儲存和管理資料列溢位**varchar**， **nvarchar**， **varbinary**，和**sql_variant**資料分割，不論這些頁面是否正在使用中或不內的資料行。 IAM 頁數包括在內。<br /><br /> 永遠是 0，表示資料行存放區索引。|  
|**used_page_count**|**bigint**|資料分割的總使用頁數。 計算方式為**in_row_used_page_count** + **lob_used_page_count** + **row_overflow_used_page_count**。|  
|**reserved_page_count**|**bigint**|資料分割的總保留頁數。 計算方式為**in_row_reserved_page_count** + **lob_reserved_page_count** + **row_overflow_reserved_page_count**。|  
|**row_count**|**bigint**|此資料分割中大約的資料列數目。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
|**distribution_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 與發佈相關聯的唯一數值識別碼。|  
  
## <a name="remarks"></a>備註  
 **sys.dm_db_partition_stats**顯示用來儲存和管理同資料列資料、 LOB 資料和資料列溢位資料之資料庫中的所有資料分割的空間的相關資訊。 每個資料分割顯示一個資料列。  
  
 在各個不同的系統資料表中，輸出所依據的計數快取於記憶體中或儲存在磁碟中。  
  
 同資料列資料、LOB 資料和資料列溢位資料代表組成資料分割的三個配置單位。 [Sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)可以查詢目錄檢視有關資料庫中每個配置單位的中繼資料。  
  
 如果堆積或索引不分割，則是由一個資料分割組成 (資料分割數目 = 1)；因此，只會針對該堆積或索引傳回一個資料列。 [Sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)可以查詢目錄檢視有關每個資料分割的所有資料表和資料庫中的索引的中繼資料。  
  
 個別資料表或索引的總計數可以藉由加入所有相關資料分割的計數來取得。  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW DATABASE STATE 權限來查詢**sys.dm_db_partition_stats**動態管理檢視。 如需動態管理檢視權限的相關詳細資訊，請參閱[動態管理檢視和函數&#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-all-counts-for-all-partitions-of-all-indexes-and-heaps-in-a-database"></a>A. 傳回資料庫中所有索引和堆積之所有資料分割的所有計數  
 下列範例會顯示 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中所有索引和堆積之所有資料分割的所有計數。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats;  
GO  
```  
  
### <a name="b-returning-all-counts-for-all-partitions-of-a-table-and-its-indexes"></a>B. 傳回資料表與其索引之所有資料分割的所有計數  
 下列範例會顯示 `HumanResources.Employee` 資料表與其索引之所有資料分割的所有計數。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats   
WHERE object_id = OBJECT_ID('HumanResources.Employee');  
GO  
```  
  
### <a name="c-returning-total-used-pages-and-total-number-of-rows-for-a-heap-or-clustered-index"></a>C. 傳回堆積或叢集索引的總使用頁數和資料列總數  
 下列範例會傳回 `HumanResources.Employee` 資料表之堆積或叢集索引的總使用頁數和資料列總數。 因為依預設不會分割 `Employee` 資料表，請注意總和只包括一個資料分割。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT SUM(used_page_count) AS total_number_of_used_pages,   
    SUM (row_count) AS total_number_of_rows   
FROM sys.dm_db_partition_stats  
WHERE object_id=OBJECT_ID('HumanResources.Employee')    AND (index_id=0 or index_id=1);  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  


