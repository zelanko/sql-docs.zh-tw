---
title: "sp_repltrans (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_repltrans_TSQL
- sp_repltrans
helpviewer_keywords:
- sp_repltrans
ms.assetid: 738e2322-335b-44fa-820e-f31c02743978
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2123841f5819842df4a4833e1a243dbfbeddf7dc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sprepltrans-transact-sql"></a>sp_repltrans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回發行集資料庫交易記錄中所有交易的結果集，這些交易標示了複寫但尚未標示為已散發。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_repltrans  
```  
  
## <a name="result-sets"></a>結果集  
 **sp_repltrans**傳回從中執行時，可讓您檢視目前尚未散發的交易在發行集資料庫的相關資訊 (尚未傳送至交易記錄檔中的那些交易散發者）。 結果集會顯示每項交易的第一個和最後一個記錄的記錄序號。 **sp_repltrans**類似於[sp_replcmds &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) 、 但未傳回之交易的命令。  
  
## <a name="remarks"></a>備註  
 **sp_repltrans**用於異動複寫中。  
  
 **sp_repltrans**不支援非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_repltrans**。  
  
## <a name="see-also"></a>請參閱＜  
 [sp_repldone &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
