---
title: 遇到了 sys.dm_fts_active_catalogs (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_active_catalogs_TSQL
- dm_fts_active_catalogs
- dm_fts_active_catalogs_TSQL
- sys.dm_fts_active_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_active_catalogs dynamic management view
ms.assetid: 40ab5453-040c-4d2e-bb49-e340cf90c3ee
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4cf1900b52953f296a931f40f850b94a1243158
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmftsactivecatalogs-transact-sql"></a>sys.dm_fts_active_catalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回全文檢索目錄的相關資訊，這些目錄正在伺服器上進行某個母體擴展活動。  
  
> [!NOTE]  
>  未來版本將移除下列資料行[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: is_paused、 previous_status、 previous_status_description、 row_count_in_thousands、 狀態、 status_description 和 worker_count。 請避免在新的開發工作中使用這些資料行，並規劃修改目前使用這些資料行的應用程式。  
  
 
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|包含使用中全文檢索目錄的資料庫識別碼。|  
|**catalog_id**|**int**|使用中全文檢索目錄的識別碼。|  
|**memory_address**|**varbinary(8)**|配置給與這個全文檢索目錄有關之母體擴展活動的記憶體緩衝區位址。|  
|**name**|**nvarchar(128)**|使用中全文檢索目錄的名稱。|  
|**is_paused**|**bit**|指出使用中全文檢索目錄的母體擴展是否已經暫停。|  
|**status**|**int**|全文檢索目錄的目前狀態。 它有下列幾種：<br /><br /> 0 = 正在初始化<br /><br /> 1 = 已就緒<br /><br /> 2 = 已暫停<br /><br /> 3 = 暫時錯誤<br /><br /> 4 = 需要重新掛載<br /><br /> 5 = 已關閉<br /><br /> 6 = 默認備份<br /><br /> 7 = 已備份整個目錄<br /><br /> 8 = 目錄已損毀|  
|**status_description**|**nvarchar(120)**|使用中全文檢索目錄目前狀態的描述。|  
|**previous_status**|**int**|全文檢索目錄的先前狀態。 它有下列幾種：<br /><br /> 0 = 正在初始化<br /><br /> 1 = 已就緒<br /><br /> 2 = 已暫停<br /><br /> 3 = 暫時錯誤<br /><br /> 4 = 需要重新掛載<br /><br /> 5 = 已關閉<br /><br /> 6 = 默認備份<br /><br /> 7 = 已備份整個目錄<br /><br /> 8 = 目錄已損毀|  
|**previous_status_description**|**nvarchar(120)**|使用中全文檢索目錄先前狀態的描述。|  
|**worker_count**|**int**|目前在使用這個全文檢索目錄的執行緒數目。|  
|**active_fts_index_count**|**int**|擴展中的全文檢索索引數目。|  
|**auto_population_count**|**int**|正為此全文檢索目錄進行自動母體擴展的資料表數目。|  
|**manual_population_count**|**int**|正為此全文檢索目錄進行手動母體擴展的資料表數目。|  
|**full_incremental_population_count**|**int**|針對這個全文檢索目錄在進行完整或累加母體擴展的資料表數目。|  
|**row_count_in_thousands**|**int**|這個全文檢索目錄中所有全文檢索索引中的預估資料列數 (以千為單位)。|  
|**is_importing**|**bit**|指出是否正在匯入全文檢索目錄：<br /><br /> 1 = 正在匯入此目錄。<br /><br /> 2 = 沒有正在匯入此目錄。|  
  
## <a name="remarks"></a>備註  
 Is_importing 資料行的新[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。  
  
## <a name="permissions"></a>Permissions  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
   
## <a name="physical-joins"></a>實體聯結  
 ![這個動態管理檢視的重要聯結](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-active-catalogs-1.gif "此動態管理檢視的重要聯結")  
  
## <a name="relationship-cardinalities"></a>關聯性基數  
  
|來源|若要|關聯性|  
|----------|--------|------------------|  
|dm_fts_active_catalogs.database_id|dm_fts_index_population.database_id|一對一|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|一對一|  
  
## <a name="examples"></a>範例  
 下列範例會傳回目前資料庫上之作用中全文檢索目錄的詳細資訊。  
  
```  
SELECT catalog.name, catalog.is_importing, catalog.auto_population_count,  
  OBJECT_NAME(population.table_id) AS table_name,  
  population.population_type_description, population.is_clustered_index_scan,  
  population.status_description, population.completion_type_description,  
  population.queued_population_type_description, population.start_time,  
  population.range_count   
FROM sys.dm_fts_active_catalogs catalog   
CROSS JOIN sys.dm_fts_index_population population   
WHERE catalog.database_id = population.database_id   
AND catalog.catalog_id = population.catalog_id   
AND catalog.database_id = (SELECT dbid FROM sys.sysdatabases WHERE name = DB_NAME());  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 
 [全文檢索搜尋和語意搜尋動態管理檢視與函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
