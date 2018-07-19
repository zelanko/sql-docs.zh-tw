---
title: sp_query_store_flush_db (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_query_store_flush_db_TSQL
- sys.sp_query_store_flush_db_TSQL
- sp_query_store_flush_db
- sys.sp_query_store_flush_db
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_query_store_flush_db
- sp_query_store_flush_db
ms.assetid: 580c03ae-57fc-4562-a6bb-5ec89521e38c
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0dca89f1d5876d437ccce2009db77614ba04ce4c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993628"
---
# <a name="spquerystoreflushdb-transact-sql"></a>sp_query_store_flush_db & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  查詢存放區資料的記憶體中部分會排清至磁碟。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_query_store_flush_db [;]  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
  
## <a name="permissions"></a>Permissions  
 需要**EXECUTE**的資料庫上的權限並**刪除**查詢存放區目錄檢視的權限。  
  
## <a name="examples"></a>範例  
 下列範例會清除查詢存放區資料的記憶體中部分至磁碟。  
  
```  
EXEC sp_query_store_flush_db;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [sp_query_store_remove_query &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [sp_query_store_reset_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [sp_query_store_reset_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [查詢存放區目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [使用查詢存放區監視效能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  
