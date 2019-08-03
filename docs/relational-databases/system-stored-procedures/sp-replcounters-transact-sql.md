---
title: sp_replcounters (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replcounters
- sp_replcounters_TSQL
helpviewer_keywords:
- sp_replcounters
ms.assetid: fe585b1f-edda-421f-81d6-8a03a3a535d2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 12ddbfe11a2b1a29dadaacde845f96e70959bebb
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771005"
---
# <a name="spreplcounters-transact-sql"></a>sp_replcounters (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
|**複寫速率交易數/秒**|**float**|傳遞給散發資料庫的每秒平均交易數目。|  
|**複寫延遲**|**float**|在散發之前，交易在記錄中的平均時間 (以秒為單位)。|  
|**Dbtable replbeginlsn**|**binary(10)**|記錄中目前截斷點的日誌序號 (LSN)。|  
|**Replnextlsn**|**binary(10)**|等待傳遞給散發資料庫的下一項認可記錄的 LSN。|  
  
## <a name="remarks"></a>備註  
 **sp_replcounters**用於異動複寫中。  
  
## <a name="permissions"></a>Permissions  
 需要**db_owner**固定資料庫角色或**系統管理員 (sysadmin** ) 固定伺服器角色中的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
