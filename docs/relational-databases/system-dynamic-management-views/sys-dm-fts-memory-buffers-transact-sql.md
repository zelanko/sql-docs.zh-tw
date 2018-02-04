---
title: "sys.dm_fts_memory_buffers (TRANSACT-SQL) |Microsoft 文件"
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
- sys.dm_fts_memory_buffers
- dm_fts_memory_buffers_TSQL
- dm_fts_memory_buffers
- sys.dm_fts_memory_buffers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_memory_buffers dynamic management view
ms.assetid: 56895fe5-e8df-4d75-9adc-c1f7757cdef8
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 190d564ec27cf7921fbfbd9d6e85fc594b77c2d6
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmftsmemorybuffers-transact-sql"></a>sys.dm_fts_memory_buffers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回屬於特定記憶體集區之記憶體緩衝區的相關資訊，這些緩衝區會做為全文檢索搜耙的一部分或全文檢索搜耙範圍使用。  
  
> [!NOTE]
> 未來版本將移除下列資料行[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **row_count**。 請避免在新的開發工作中使用這個資料行，並請規劃修改目前使用這個資料行的應用程式。  

  
|資料行|資料類型|Description|  
|------------|---------------|-----------------|  
|**pool_id**|**int**|配置的記憶體集區識別碼。<br /><br /> 0 = 小緩衝區<br /><br /> 1 = 大緩衝區|  
|**memory_address**|**varbinary(8)**|配置記憶體集區的識別碼。|  
|**name**|**nvarchar(4000)**|共用記憶體緩衝區的名稱，這項配置就是針對該緩衝區而建立。|  
|**is_free**|**bit**|記憶體緩衝區的目前狀態。<br /><br /> 0 = 可用<br /><br /> 1 = 忙碌|  
|**row_count**|**int**|這個緩衝區目前正在處理的資料列數。|  
|**bytes_used**|**int**|這個緩衝區目前正在使用的記憶體量 (以位元組為單位)。|  
|**percent_used**|**int**|所用的配置記憶體百分比。|  
  
## <a name="permissions"></a>Permissions  
在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 層需要`VIEW DATABASE STATE`資料庫的權限。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]標準和基本層，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。  
 
## <a name="physical-joins"></a>實體聯結  
 ![這個動態管理檢視的重要聯結](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-memory-buffers-1.gif "此動態管理檢視的重要聯結")  
  
## <a name="relationship-cardinalities"></a>關聯性基數  
  
|來源|若要|關聯性|  
|----------|--------|------------------|  
|dm_fts_memory_buffers.pool_id|dm_fts_memory_pools.pool_id|多對一|  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [全文檢索搜尋及語意搜尋動態管理檢視與函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

