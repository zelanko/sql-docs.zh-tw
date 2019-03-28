---
title: sp_dropuser (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropuser
- sp_dropuser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropuser
ms.assetid: e28f18f9-7ecf-4568-89f4-fe5c520df386
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d96004357962ee822df7458a30d740fc836de658
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58532950"
---
# <a name="spdropuser-transact-sql"></a>sp_dropuser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從目前資料庫移除資料庫使用者。 **sp_dropuser**提供與舊版的相容性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[DROP USER](../../t-sql/statements/drop-user-transact-sql.md)改。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropuser [ @name_in_db = ] 'user'  
```  
  
## <a name="arguments"></a>引數  
`[ @name_in_db = ] 'user'` 是要移除之使用者的名稱。 *使用者*已**sysname**，沒有預設值。 *使用者*必須存在於目前的資料庫。 在指定 Windows 登入時，請使用該登入在資料庫所用的名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_dropuser**會執行**sp_revokedbaccess**從目前資料庫移除使用者。  
  
 使用**sp_helpuser**顯示一份可以從目前資料庫中移除的使用者名稱。  
  
 移除資料庫使用者時，也會一併移除該使用者的任何別名。 如果該使用者擁有與該使用者同名的空結構描述，則會卸除結構描述。 如果該使用者擁有資料庫中任何其他安全性實體，則不會卸除使用者。 物件的擁有權必須先傳送到另一個主體。 如需詳細資訊，請參閱 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)。 移除資料庫使用者時，也會自動移除與該使用者相關聯的權限，並且從它所屬的任何資料庫角色移除該使用者。  
  
 **sp_dropuser**無法用來移除資料庫擁有者 (**dbo**) **INFORMATION_SCHEMA**的使用者，或有**客體**使用者**master**或是**tempdb**資料庫。 在非系統資料庫`EXEC sp_dropuser 'guest'`將會撤銷 CONNECT 權限與使用者**客體**。 但是使用者本身不會被卸除。  
  
 **sp_dropuser**無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 ALTER ANY USER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從目前資料庫移除使用者 `Albert`。  
  
```  
EXEC sp_dropuser 'Albert';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [sp_revokedbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
