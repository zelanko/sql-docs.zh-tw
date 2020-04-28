---
title: sys.databases dm_fts_population_ranges （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_population_ranges
- sys.dm_fts_population_ranges_TSQL
- dm_fts_population_ranges_TSQL
- dm_fts_population_ranges
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_population_ranges dynamic management view
ms.assetid: 58d8564b-9c43-4965-a31c-2893890334ef
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f00de77ef3435bf998f9019fc8b60458594fb0f2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68265898"
---
# <a name="sysdm_fts_population_ranges-transact-sql"></a>sys.dm_fts_population_ranges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回與目前正在進行的全文檢索索引擴展相關之特定範圍的資訊。  
   
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**memory_address**|**varbinary(8)**|針對與這個全文檢索索引母體擴展子範圍有關之活動所配置的記憶體緩衝區位址。|  
|**parent_memory_address**|**varbinary(8)**|代表與全文檢索索引相關之母體擴展所有範圍的父物件記憶體緩衝區位址。|  
|**is_retry**|**bit**|如果其值為 1，這個子範圍就負責重試發生錯誤的資料列。|  
|**session_id**|**smallint**|目前正在處理這項工作的工作階段識別碼。|  
|**processed_row_count**|**int**|這個範圍已處理的資料列數。 向前進度會進行保存，而且每 5 分鐘計算一次，而不是每批次認可計算一次。|  
|**error_count**|**int**|這個範圍已發生錯誤的資料列數。 向前進度會進行保存，而且每 5 分鐘計算一次，而不是每批次認可計算一次。|  
  
## <a name="permissions"></a>權限  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要許可權。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高階層級上， `VIEW DATABASE STATE`需要資料庫的許可權。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] [標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   
 
## <a name="physical-joins"></a>實體聯結  
 ![這個動態管理檢視的重要聯結](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-population-ranges-1.gif "這個動態管理檢視的重要聯結")  
  
## <a name="relationship-cardinalities"></a>關聯性基數  
  
|從|至|關聯性|  
|----------|--------|------------------|  
|dm_fts_population_ranges.parent_memory_address|dm_fts_index_population.memory_address|多對一|  
  
## <a name="see-also"></a>另請參閱  
  [全文檢索搜尋和語義搜尋動態管理檢視和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

