---
title: sys.databases dm_column_store_object_pool （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a8a58ca7-0a7d-4786-bfd9-e8894bd345dd
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83369736ee18c36b3967bbbd129e0fd64574a2ed
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68265992"
---
# <a name="sysdm_column_store_object_pool-transact-sql"></a>sys.databases dm_column_store_object_pool （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 針對資料行存放區索引物件，傳回不同類型的物件記憶體集區使用計數。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|資料庫的識別碼。 這在 SQL Server 資料庫或 Azure SQL database 伺服器的實例內是唯一的。 |  
|`object_id`|`int`|物件的識別碼。 物件是其中一個 object_types。 | 
|`index_id`|`int`|資料行存放區索引的識別碼。|  
|`partition_number`|`bigint`|在索引或堆積內，以 1 為基底的資料分割編號。 每個資料表或視圖都至少有一個資料分割。| 
|`column_id`|`int`|資料行存放區資料行的識別碼。 對於 DELETE_BITMAP，這會是 Null。| 
|`row_group_id`|`int`|資料列群組的識別碼。|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|COLUMN_SEGMENT-資料行區段。 `object_id`這是區段識別碼。 區段會將一個資料行的所有值儲存在一個資料列群組中。 例如，如果資料表有10個數據行，每個資料列群組會有10個數據行區段。 <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY-包含資料表中所有資料行區段之查閱資訊的全域字典。<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY-與一個資料行相關聯的本機字典。<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY-全域字典的另一個標記法。 這會提供從值到 dictionary_id 的反向查詢。 用來建立壓縮區段做為 Tuple Mover 或大量載入的一部分。<br /><br /> COLUMN_SEGMENT_DELETE_BITMAP-追蹤區段刪除的點陣圖。 每個分割區都有一個刪除點陣圖。|  
|`access_count`|`int`|此物件的讀取或寫入存取次數。|  
|`memory_used_in_bytes`|`bigint`|物件集區中此物件所使用的記憶體。|  
|`object_load_time`|`datetime`|將 object_id 帶入物件集區時的時鐘時間。|  
  
## <a name="permissions"></a>權限  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要許可權。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高階層級上， `VIEW DATABASE STATE`需要資料庫的許可權。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] [標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   
 
## <a name="see-also"></a>另請參閱  
  
 [索引相關的動態管理檢視和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [dm_db_index_operational_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  
