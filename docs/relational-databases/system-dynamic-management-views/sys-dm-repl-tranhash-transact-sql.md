---
title: "sys.dm_repl_tranhash (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_tranhash
- sys.dm_repl_tranhash_TSQL
- dm_repl_tranhash_TSQL
- dm_repl_tranhash
dev_langs: TSQL
helpviewer_keywords: sys.dm_repl_tranhash dynamic management view
ms.assetid: 0cc52338-e805-4ed4-9835-b19bbf72448e
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 40d5bdff43e1022e62f20092b8b3d8dff1928231
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmrepltranhash-transact-sql"></a>sys.dm_repl_tranhash (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關在交易式發行集中複寫之交易的資訊。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
|column_name|data_type|description|  
|------------------|----------------|-----------------|  
|**值區**|**bigint**|雜湊資料表中的值區數。|  
|**hashed_trans**|**bigint**|在目前批次中複寫的認可交易數。|  
|**completed_trans**|**bigint**|到目前為止完成的交易數。|  
|**compensated_trans**|**bigint**|包含部分回復的交易數。|  
|**first_begin_lsn**|**nvarchar （64)**|目前批次中的最早開始記錄序號 (LSN)。|  
|**last_commit_lsn**|**nvarchar （64)**|目前批次中的最後認可 LSN。|  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW DATABASE STATE 權限在發行集資料庫上的呼叫**dm_repl_tranhash**。  
  
## <a name="remarks"></a>備註  
 只對目前載入複寫發行項快取中的複寫資料庫物件傳回這項資訊。  
  
## <a name="see-also"></a>請參閱＜  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [複寫相關的動態管理檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  
