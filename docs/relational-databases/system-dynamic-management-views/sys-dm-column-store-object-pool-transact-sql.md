---
title: sys.dm_column_store_object_pool (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a8a58ca7-0a7d-4786-bfd9-e8894bd345dd
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: f77b7f9ac514de77825f3f0ce1f201e293da2698
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39551628"
---
# <a name="sysdmcolumnstoreobjectpool-transact-sql"></a>sys.dm_column_store_object_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 傳回計算不同類型的資料行存放區索引物件的物件記憶體集區使用方式。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|資料庫的識別碼。 這是唯一的 SQL Server 資料庫或 Azure SQL database 伺服器的執行個體。 |  
|`object_id`|`int`|物件的識別碼。 此物件為 object_types 的其中一個。 | 
|`index_id`|`int`|資料行存放區索引的識別碼。|  
|`partition_number`|`bigint`|在索引或堆積內，以 1 為基底的資料分割編號。 每個資料表或檢視表有至少一個資料分割。| 
|`column_id`|`int`|資料行存放區資料行的識別碼。 這是 DELETE_BITMAP 都是 NULL。| 
|`row_group_id`|`int`|資料列群組的識別碼。|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|COLUMN_SEGMENT – 資料行區段。 `object_id` 這是區段識別碼。 區段會儲存一個資料列群組內的一個資料行的值。 例如，如果資料表有 10 個資料行，是每個資料行的 10 個資料行區段。 <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY – 全域的字典，其中包含所有資料表中的資料行區段的查閱資訊。<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY-一個資料行相關聯的本機字典。<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY – 另一個全域字典表示法。 這會提供要 dictionary_id 值的反向查詢。 用於建立 Tuple Mover 或大量載入的一部分的壓縮的區段。<br /><br /> COLUMN_SEGMENT_DELETE_BITMAP – 點陣圖，以追蹤區段刪除。 沒有一個的刪除點陣圖，每個分割區。|  
|`access_count`|`int`|讀取或寫入存取此物件的數目。|  
|`memory_used_in_bytes`|`bigint`|物件集區中的這個物件所使用的記憶體。|  
|`object_load_time`|`datetime`|針對當 object_id 已帶入物件集區的時鐘時間。|  
  
## <a name="permissions"></a>Permissions  

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
 
## <a name="see-also"></a>另請參閱  
  
 [索引相關的動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  
