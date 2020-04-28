---
title: sys.databases dm_fts_memory_pools （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_memory_pools_TSQL
- sys.dm_fts_memory_pools_TSQL
- sys.dm_fts_memory_pools
- dm_fts_memory_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_memory_pools dynamic management view
ms.assetid: 24747239-cd78-4d55-a00a-19233a457f42
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d45436070618e446921c610a9e82b0cc35271c8d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68265910"
---
# <a name="sysdm_fts_memory_pools-transact-sql"></a>sys.dm_fts_memory_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對全文檢索搜耙或全文檢索搜耙範圍，傳回可供「全文檢索收集程式」元件使用之共用記憶體集區的相關資訊。  
   
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|配置的記憶體集區識別碼。<br /><br /> 0 = 小緩衝區<br /><br /> 1 = 大緩衝區|  
|**buffer_size**|**int**|記憶體集區中每一個配置的緩衝區大小。|  
|**min_buffer_limit**|**int**|記憶體集區所接受的緩衝區最小數目。|  
|**max_buffer_limit**|**int**|記憶體集區所接受的緩衝區最大數目。|  
|**buffer_count**|**int**|目前記憶體集區中共用記憶體緩衝區的數目。|  
  
## <a name="permissions"></a>權限  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要許可權。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高階層級上， `VIEW DATABASE STATE`需要資料庫的許可權。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] [標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   
 
## <a name="physical-joins"></a>實體聯結  
 ![這個動態管理檢視的重要聯結](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-memory-pools-1.gif "這個動態管理檢視的重要聯結")  
  
## <a name="relationship-cardinalities"></a>關聯性基數  
  
|從|至|關聯性|  
|----------|--------|------------------|  
|dm_fts_memory_buffers.pool_id|dm_fts_memory_pools.pool_id|多對一|  
  
## <a name="examples"></a>範例  
 下列範例會傳回 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 處理序的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]「全文檢索收集程式」元件擁有的共用記憶體總計。  
  
```  
SELECT SUM(buffer_size * buffer_count) AS "total memory"   
    FROM sys.dm_fts_memory_pools;  
```  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋和語義搜尋動態管理檢視和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
