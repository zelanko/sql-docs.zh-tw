---
title: sys.dm_repl_tranhash (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_tranhash
- sys.dm_repl_tranhash_TSQL
- dm_repl_tranhash_TSQL
- dm_repl_tranhash
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_tranhash dynamic management view
ms.assetid: 0cc52338-e805-4ed4-9835-b19bbf72448e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0c44c5c08dc46da5a0f2f3dfd2c53ab6cb20f27d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067868"
---
# <a name="sysdmrepltranhash-transact-sql"></a>sys.dm_repl_tranhash (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關在交易式發行集中複寫之交易的資訊。  
  
|column_name|data_type|description|  
|------------------|----------------|-----------------|  
|**貯體**|**bigint**|雜湊資料表中的值區數。|  
|**hashed_trans**|**bigint**|在目前批次中複寫的認可交易數。|  
|**completed_trans**|**bigint**|到目前為止完成的交易數。|  
|**compensated_trans**|**bigint**|包含部分回復的交易數。|  
|**first_begin_lsn**|**nvarchar(64)**|目前批次中的最早開始記錄序號 (LSN)。|  
|**last_commit_lsn**|**nvarchar(64)**|目前批次中的最後認可 LSN。|  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW DATABASE STATE 權限在發行集資料庫上的呼叫**dm_repl_tranhash**。  
  
## <a name="remarks"></a>備註  
 只對目前載入複寫發行項快取中的複寫資料庫物件傳回這項資訊。  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [複寫相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  
