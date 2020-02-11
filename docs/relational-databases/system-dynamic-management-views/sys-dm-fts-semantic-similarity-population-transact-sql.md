---
title: sys.databases dm_fts_semantic_similarity_population （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_semantic_similarity_population_TSQL
- sys.dm_fts_semantic_similarity_population
- dm_fts_semantic_similarity_population
- sys.dm_fts_semantic_similarity_population_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_semantic_similarity_population dynamic management view
ms.assetid: 33666f28-c370-47e2-a932-190316ed5f69
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 280ab197ef9347c6a209be7ef05e8f1ce2dfd23e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67900877"
---
# <a name="sysdm_fts_semantic_similarity_population-transact-sql"></a>sys.dm_fts_semantic_similarity_population (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回一個資料列，其中包含每個有相關語意索引的資料表中每個相似度索引之文件相似度索引母體擴展的狀態資訊。  
  
 母體擴展步驟在擷取步驟之後執行。 如需相似性解壓縮步驟的狀態資訊，請參閱[dm_fts_index_population &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)。  
    
||||  
|-|-|-|  
|**資料行名稱**|**型別**|**說明**|  
|**database_id**|**int**|包含要擴展之全文檢索索引的資料庫識別碼。|  
|**catalog_id**|**int**|包含這個全文檢索索引之全文檢索目錄的識別碼。|  
|**table_id**|**int**|要擴展全文檢索索引的資料表識別碼。|  
|**document_count**|**int**|母體擴展中的總文件數|  
|**document_processed_count**|**int**|此母體擴展循環啟動之後所處理的文件數|  
|**completion_type**|**int**|這個母體擴展如何完成的狀態。|  
|**completion_type_description**|**Nvarchar （120）**|完成類型的描述。|  
|**worker_count**|**int**|與相似度擷取相關聯的背景工作執行緒數目|  
|**狀態**|**int**|這個母體擴展的狀態。 注意：有些狀態是暫時性。 下列其中之一：<br /><br /> 3 = 啟動中<br /><br /> 5 = 正常處理<br /><br /> 7 = 已停止處理<br /><br /> 11 = 母體擴展中止|  
|**status_description**|**Nvarchar （120）**|母體擴展狀態的描述。|  
|**start_time**|**datetime**|啟動母體擴展的時間。|  
|**incremental_timestamp**|**timestamp**|代表完整母體擴展的起始時間戳記。 如果是其他所有母體擴展類型，這個值是最後一個認可的檢查點，代表母體擴展的進度。|  
  
## <a name="general-remarks"></a>一般備註  
 如需詳細資訊，請參閱[管理和監視語義搜尋](../../relational-databases/search/manage-and-monitor-semantic-search.md)。  
  
## <a name="metadata"></a>中繼資料  
 如需有關語義索引狀態的詳細資訊，請查詢[sys.databases dm_fts_index_population &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
 下列範例示範如何針對有相關語意索引的所有資料表，查詢文件相似度索引母體擴展的狀態：  
  
```  
SELECT * FROM sys.dm_fts_semantic_similarity_population;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [管理及監視語意搜尋](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
