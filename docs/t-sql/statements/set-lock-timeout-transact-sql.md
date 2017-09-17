---
title: "SET LOCK_TIMEOUT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOCK_TIMEOUT_TSQL
- SET_LOCK_TIMEOUT_TSQL
- SET LOCK_TIMEOUT
- LOCK_TIMEOUT
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- releasing locks
- LOCK_TIMEOUT option
- SET LOCK_TIMEOUT statement
- locking [SQL Server], time-outs
- wait time for lock releases [SQL Server]
ms.assetid: dd0c389e-956d-435e-bf71-e16624a0a215
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 754242a86367b07b98caa9f70f457b70d0840075
ms.openlocfilehash: 3de86c7f33afd6e708ad8e773470ec650e092d2c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/12/2017

---
# <a name="set-locktimeout-transact-sql"></a>SET LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定陳述式等待鎖定釋出的毫秒數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SET LOCK_TIMEOUT timeout_period  
```  
  
## <a name="arguments"></a>引數  
 *timeout_period*  
 是之前，所經歷的毫秒數[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回鎖定錯誤。 -1 值 (預設值) 表示沒有逾時期限 (也就是永久等待)。  
  
 當等待鎖定超出逾時值時，會傳回錯誤。 0 值表示完全不等待，且在發現鎖定之後，儘快傳回一則訊息。  
  
## <a name="remarks"></a>備註  
 在開始連線時，這個設定的值為 -1。 變更之後，新設定會在接下來的連線時間內維持有效。  
  
 SET LOCK_TIMEOUT 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
 READPAST 鎖定提示提供這個 SET 選項的替代方案。  
  
 CREATE DATABASE、ALTER DATABASE 和 DROP DATABASE 陳述式不接受 SET LOCK_TIMEOUT 設定。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-set-the-lock-timeout-to-1800-milliseconds"></a>答： 設定為 1800年毫秒的鎖定逾時  
 下列範例將鎖定逾時期限設為 `1800` 毫秒。  
  
```sql  
SET LOCK_TIMEOUT 1800;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-set-the-lock-timeout-to-wait-forever-for-a-lock-to-be-released"></a>B. 設定永久等待鎖定釋出鎖定逾時。  
 下列範例會設定在鎖定逾時，永遠等候，並永遠不過期。 這是預設行為，已設定每個連線的開頭。  
  
```sql  
SET LOCK_TIMEOUT -1;  
```  
  
 下列範例將鎖定逾時期限設為 `1800` 毫秒。 在此版本中，[!INCLUDE[ssDW](../../includes/ssdw-md.md)]將會剖析陳述式成功，但會忽略此值為 1800年並繼續使用預設行為。  
  
```sql  
SET LOCK_TIMEOUT 1800;  
```  
  
## <a name="see-also"></a>另請參閱  
 [@@LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/functions/lock-timeout-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  


