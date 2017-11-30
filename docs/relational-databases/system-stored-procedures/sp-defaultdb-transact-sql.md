---
title: "sp_defaultdb (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_defaultdb_TSQL
- sp_defaultdb
dev_langs: TSQL
helpviewer_keywords: sp_defaultdb
ms.assetid: 663b859f-c6da-4942-95a6-60b93d05654e
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c44a3f1f26861e3e78e936aeb642e33ead4a4786
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spdefaultdb-transact-sql"></a>sp_defaultdb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更預設資料庫[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_defaultdb [ @loginame = ] 'login', [ @defdb = ] 'database'   
```  
  
## <a name="arguments"></a>引數  
 [  **@loginame=**] **'***登入***'**  
 這是登入名稱。 *登入*是**sysname**，沒有預設值。 *登入*可以是現有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入或 Windows 使用者或群組。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中沒有 Windows 使用者或群組的登入，則會自動加入。  
  
 [  **@defdb=**] **'***資料庫***'**  
 這是新預設資料庫的名稱。 *資料庫*是**sysname**，沒有預設值。 *資料庫*必須已經存在。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_defaultdb**呼叫 ALTER LOGIN。 這個陳述式支援其他選項。 如需變更預設資料庫的詳細資訊，請參閱[ALTER LOGIN &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-login-transact-sql.md).  
  
 **sp_defaultdb**無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY LOGIN 權限。  
  
## <a name="examples"></a>範例  
 下列範例會將 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 設為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `Victoria` 的預設資料庫。  
  
```  
EXEC sp_defaultdb 'Victoria', 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>請參閱  
 [安全性預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
