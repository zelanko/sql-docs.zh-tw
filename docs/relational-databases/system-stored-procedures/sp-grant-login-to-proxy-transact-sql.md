---
title: sp_grant_login_to_proxy （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_proxy
- sp_grant_login_to_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_login_to_proxy
ms.assetid: 90e1a6d5-a692-4462-a163-4b0709d83150
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: d7ac6bfbd157a72cee716b4a5a916cf2c7069ba8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750543"
---
# <a name="sp_grant_login_to_proxy-transact-sql"></a>sp_grant_login_to_proxy (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  授與 Proxy 的安全性主體存取權。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_grant_login_to_proxy   
     { [ @login_name = ] 'login_name'   
     | [ @fixed_server_role = ] 'fixed_server_role'   
     | [ @msdb_role = ] 'msdb_role' } ,   
     { [ @proxy_id = ] id | [ @proxy_name = ] 'proxy_name' }  
```  
  
## <a name="arguments"></a>引數  
`[ @login_name = ] 'login_name'`要授與存取權的登入名稱。 *Login_name*是**Nvarchar （256）**，預設值是 Null。 必須指定** \@ login_name**、 ** \@ fixed_server_role**或** \@ msdb_role**的其中一個，否則預存程式會失敗。  
  
`[ @fixed_server_role = ] 'fixed_server_role'`要授與存取權的固定伺服器角色。 *Fixed_server_role*是**Nvarchar （256）**，預設值是 Null。 必須指定** \@ login_name**、 ** \@ fixed_server_role**或** \@ msdb_role**的其中一個，否則預存程式會失敗。  
  
`[ @msdb_role = ] 'msdb_role'`**Msdb**資料庫中要授與存取權的資料庫角色。 *Msdb_role*是**Nvarchar （256）**，預設值是 Null。 必須指定** \@ login_name**、 ** \@ fixed_server_role**或** \@ msdb_role**的其中一個，否則預存程式會失敗。  
  
`[ @proxy_id = ] id`要授與存取權的 proxy 識別碼。 *識別碼*是**int**，預設值是 Null。 必須指定** \@ proxy_id**或** \@ proxy_name**的其中一個，否則預存程式會失敗。  
  
`[ @proxy_name = ] 'proxy_name'`要授與存取權的 proxy 名稱。 *Proxy_name*是**Nvarchar （256）**，預設值是 Null。 必須指定** \@ proxy_id**或** \@ proxy_name**的其中一個，否則預存程式會失敗。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_grant_login_to_proxy**必須從**msdb**資料庫中執行。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行**sp_grant_login_to_proxy**。  
  
## <a name="examples"></a>範例  
 下列範例可讓登入 `adventure-works\terrid` 使用 proxy `Catalog application proxy` 。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_login_to_proxy  
    @login_name = N'adventure-works\terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_add_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
