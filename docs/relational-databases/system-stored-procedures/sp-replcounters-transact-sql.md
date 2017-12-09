---
title: "sp_replcounters (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_replcounters
- sp_replcounters_TSQL
helpviewer_keywords: sp_replcounters
ms.assetid: fe585b1f-edda-421f-81d6-8a03a3a535d2
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3383f50142e04966a24515adcf08efbc4c5c60bc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spreplcounters-transact-sql"></a>sp_replcounters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回每個已發行的資料庫之延遲、輸送量和交易計數的複寫統計資料。 這個預存程序執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replcounters  
  
```  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**資料庫**|**sysname**|資料庫的名稱。|  
|**複寫的交易**|**int**|記錄中等待傳遞給散發資料庫的交易數目。|  
|**複寫頻率 trans/sec**|**float**|傳遞給散發資料庫的每秒平均交易數目。|  
|**複寫延遲**|**float**|在散發之前，交易在記錄中的平均時間 (以秒為單位)。|  
|**Replbeginlsn**|**binary(10)**|記錄中目前截斷點的日誌序號 (LSN)。|  
|**Replendlsn**|**binary(10)**|等待傳遞給散發資料庫的下一項認可記錄的 LSN。|  
  
## <a name="remarks"></a>備註  
 **sp_replcounters**用於異動複寫中。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**db_owner**固定的資料庫角色或**sysadmin**固定的伺服器角色。  
  
## <a name="see-also"></a>請參閱＜  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
