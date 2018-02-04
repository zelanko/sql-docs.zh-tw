---
title: "sys.dm_fts_index_population (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_population
- dm_fts_index_population
- sys.dm_fts_index_population_TSQL
- dm_fts_index_population_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_population dynamic management view
ms.assetid: 82d1c102-efcc-4b60-9a5e-3eee299bcb2b
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f118b1be30119e7328ee20477a0c18808fbdc3e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmftsindexpopulation-transact-sql"></a>sys.dm_fts_index_population (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中目前進行中之全文檢索索引和語意關鍵片語擴展的資訊。  
 
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|包含要擴展之全文檢索索引的資料庫識別碼。|  
|**catalog_id**|**int**|包含這個全文檢索索引之全文檢索目錄的識別碼。|  
|**table_id**|**int**|要擴展全文檢索索引的資料表識別碼。|  
|**memory_address**|**varbinary(8)**|用來表示使用中母體擴展之內部資料結構的記憶體位址。|  
|**population_type**|**int**|母體擴展的類型。 它有下列幾種：<br /><br /> 1 = 完整母體擴展。<br /><br /> 2 = 累加、以時間戳記為基礎的母體擴展<br /><br /> 3 = 追蹤變更的手動更新。<br /><br /> 4 = 追蹤變更的背景更新。|  
|**population_type_description**|**nvarchar(120)**|母體擴展類型的描述。|  
|**is_clustered_index_scan**|**bit**|指出母體擴展是否涉及叢集索引上的掃描。|  
|**range_count**|**int**|這個母體擴展平行處理的子範圍數目。|  
|**completed_range_count**|**int**|完成處理的範圍數目。|  
|**outstanding_batch_count**|**int**|目前此母體擴展未處理的批次數目。 如需詳細資訊，請參閱[sys.dm_fts_outstanding_batches &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md).|  
|**status**|**int**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 這個母體擴展的狀態。 注意：有些狀態是暫時性。 它有下列幾種：<br /><br /> 3 = 啟動中<br /><br /> 5 = 正常處理<br /><br /> 7 = 已停止處理<br /><br /> 例如，當自動合併正在進行時，就會發生這個狀態。<br /><br /> 11 = 母體擴展中止<br /><br /> 12 = 正在處理語意相似度擷取|  
|**status_description**|**nvarchar(120)**|母體擴展狀態的描述。|  
|**completion_type**|**int**|這個母體擴展如何完成的狀態。|  
|**completion_type_description**|**nvarchar(120)**|完成類型的描述。|  
|**worker_count**|**int**|這個值一定是 0。|  
|**queued_population_type**|**int**|母體擴展的類型，以追蹤變更為基礎，將遵照目前的母體擴展 (如果有的話)。|  
|**queued_population_type_description**|**nvarchar(120)**|要遵照之母體擴展的描述 (如果有的話)。 例如，當 CHANGE TRACKING = AUTO 而且初始完整母體擴展正在進行時，這個資料行就會顯示「自動母體擴展」。|  
|**start_time**|**datetime**|啟動母體擴展的時間。|  
|**incremental_timestamp**|**timestamp**|代表完整母體擴展的起始時間戳記。 如果是其他所有母體擴展類型，這個值是最後一個認可的檢查點，代表母體擴展的進度。|  
  
## <a name="remarks"></a>備註  
 如果除了全文檢索索引之外還啟用了統計語意索引，則關鍵片語的語意擷取和擴展以及擷取文件相似度資料會與全文檢索索引同步執行。 擴展文件相似度索引會在稍後的第二個階段執行。 如需詳細資訊，請參閱[管理及監視語意搜尋](../../relational-databases/search/manage-and-monitor-semantic-search.md)。  
  
## <a name="permissions"></a>Permissions  
在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 層需要`VIEW DATABASE STATE`資料庫的權限。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]標準和基本層，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。  
 
## <a name="physical-joins"></a>實體聯結  
 ![這個動態管理檢視的重要聯結](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-index-population-1.gif "此動態管理檢視的重要聯結")  
  
## <a name="relationship-cardinalities"></a>關聯性基數  
  
|來源|若要|關聯性|  
|----------|--------|------------------|  
|dm_fts_active_catalogs.database_id|dm_fts_index_population.database_id|一對一|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|一對一|  
|dm_fts_population_ranges.parent_memory_address|dm_fts_index_population.memory_address|多對一|  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [全文檢索搜尋及語意搜尋動態管理檢視與函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

