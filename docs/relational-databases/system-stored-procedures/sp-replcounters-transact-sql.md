---
title: sp_replcounters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_replcounters
- sp_replcounters_TSQL
helpviewer_keywords:
- sp_replcounters
ms.assetid: fe585b1f-edda-421f-81d6-8a03a3a535d2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aa7040c897297664b65ee97ca2440b23f0c35d1a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47595136"
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
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**[資料庫備份]**|**sysname**|資料庫的名稱。|  
|**複寫的交易**|**int**|記錄中等待傳遞給散發資料庫的交易數目。|  
|**複寫頻率 trans/sec**|**float**|傳遞給散發資料庫的每秒平均交易數目。|  
|**複寫延遲**|**float**|在散發之前，交易在記錄中的平均時間 (以秒為單位)。|  
|**Replbeginlsn**|**binary(10)**|記錄中目前截斷點的日誌序號 (LSN)。|  
|**Replnextlsn**|**binary(10)**|等待傳遞給散發資料庫的下一項認可記錄的 LSN。|  
  
## <a name="remarks"></a>備註  
 **sp_replcounters**用於異動複寫中。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**db_owner**固定的資料庫角色或**sysadmin**固定的伺服器角色。  
  
## <a name="see-also"></a>另請參閱  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
