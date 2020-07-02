---
title: sp_dropuser （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a231ed2809f387f58ccedef9acb8555a6569e992
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772211"
---
# <a name="sp_dropuser-transact-sql"></a>sp_dropuser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  從目前資料庫移除資料庫使用者。 **sp_dropuser**提供與舊版的相容性 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[DROP USER](../../t-sql/statements/drop-user-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropuser [ @name_in_db = ] 'user'  
```  
  
## <a name="arguments"></a>引數  
`[ @name_in_db = ] 'user'`這是要移除的使用者名稱。 *使用者*是**sysname**，沒有預設值。 *使用者*必須存在於目前的資料庫中。 在指定 Windows 登入時，請使用該登入在資料庫所用的名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_dropuser**會執行**sp_revokedbaccess** ，以從目前資料庫中移除使用者。  
  
 使用 [ **sp_helpuser** ] 顯示可從目前資料庫移除的使用者名稱清單。  
  
 移除資料庫使用者時，也會一併移除該使用者的任何別名。 如果該使用者擁有與該使用者同名的空結構描述，則會卸除結構描述。 如果該使用者擁有資料庫中任何其他安全性實體，則不會卸除使用者。 物件的擁有權必須先傳送到另一個主體。 如需詳細資訊，請參閱 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)。 移除資料庫使用者時，也會自動移除與該使用者相關聯的權限，並且從它所屬的任何資料庫角色移除該使用者。  
  
 **sp_dropuser**不能用來移除**master**或**tempdb**資料庫中的資料庫擁有者（**dbo**） **INFORMATION_SCHEMA**使用者或**來賓**使用者。 在非系統資料庫中， `EXEC sp_dropuser 'guest'` 將會撤銷使用者**來賓**的 CONNECT 許可權。 但是使用者本身不會被卸除。  
  
 **sp_dropuser**不能在使用者自訂交易內執行。  
  
## <a name="permissions"></a>權限  
 需要資料庫的 ALTER ANY USER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從目前資料庫移除使用者 `Albert`。  
  
```  
EXEC sp_dropuser 'Albert';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性預存程式](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [DROP USER &#40;Transact-sql&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [sp_revokedbaccess &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
