---
title: sp_repltrans （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repltrans_TSQL
- sp_repltrans
helpviewer_keywords:
- sp_repltrans
ms.assetid: 738e2322-335b-44fa-820e-f31c02743978
author: stevestein
ms.author: sstein
ms.openlocfilehash: 40477973efebac9a484e89e7627f0996285b430b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68770856"
---
# <a name="sp_repltrans-transact-sql"></a>sp_repltrans (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  傳回發行集資料庫交易記錄中所有交易的結果集，這些交易標示了複寫但尚未標示為已散發。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_repltrans  
```  
  
## <a name="result-sets"></a>結果集  
 **sp_repltrans**會傳回從中執行之發行集資料庫的相關資訊，讓您可以查看目前尚未散發的交易（交易記錄檔中剩餘尚未傳送給「散發者」的交易）。 結果集會顯示每項交易的第一個和最後一個記錄的記錄序號。 **sp_repltrans**類似于[sp_replcmds &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) ，但不會傳回交易的命令。  
  
## <a name="remarks"></a>備註  
 **sp_repltrans**用於異動複寫中。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)]非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者不支援**sp_repltrans** 。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_repltrans**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_repldone &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
