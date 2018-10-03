---
title: sp_dropremotelogin (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropremotelogin
- sp_dropremotelogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropremotelogin
ms.assetid: 9f097652-a286-40b2-be73-568d77ada698
ms.author: vanto
manager: craigg
ms.openlocfilehash: a834dbb26bfc8c712531084e528f82bba50cd05e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800696"
---
# <a name="spdropremotelogin-transact-sql"></a>sp_dropremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  移除對應至本機登入的遠端登入，它可以對執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本機伺服器執行遠端預存程序。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]請改用連結伺服器和連結伺服器預存程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@remoteserver =** ] **'***remoteserver***'**  
 這是對應至即將移除之遠端登入的遠端伺服器名稱。 *remoteserver*已**sysname**，沒有預設值。 *remoteserver*必須已經存在。  
  
 [ **@loginame =** ] **'***login***'**  
 這是本機伺服器上與遠端伺服器相關聯的選擇性登入名稱。 *login* 是預設值為 NULL 的 **sysname**。 *登入*必須已經存在，如果指定。  
  
 [  **@remotename =** ] **'***remote_name***'**  
 對應至的遠端登入的選擇性名稱*登入*登入時，從遠端伺服器。 *remote_name*已**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 如果只有*remoteserver*指定，則該遠端伺服器的所有遠端登入從本機伺服器中移除。 如果*登入*也是從指定的所有遠端登入*remoteserver*對應至該特定本機登入從本機伺服器中移除。 如果*remote_name*同時指定，則只有從該遠端使用者的遠端登入*remoteserver*會從本機伺服器移除。  
  
 若要加入本機伺服器使用者，請使用**sp_addlogin**。 若要移除本機伺服器使用者，請使用**sp_droplogin**。  
  
 只有當您使用舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，才需要遠端登入。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 版和更新的版本，都改用連結伺服器登入。 使用**sp_addlinkedsrvlogin**並**sp_droplinkedsrvlogin**新增和移除連結的伺服器登入。  
  
 **sp_dropremotelogin**無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**sysadmin**或是**securityadmin**固定伺服器角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-dropping-all-remote-logins-for-a-remote-server"></a>A. 卸除遠端伺服器所有的遠端登入  
 下列範例會移除遠端伺服器 `ACCOUNTS` 的項目，因而移除本機伺服器的登入，以及遠端伺服器的遠端登入之間所有的對應。  
  
```  
EXEC sp_dropremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-dropping-a-login-mapping"></a>B. 卸除登入對應  
 下列範例會移除將遠端伺服器 `ACCOUNTS` 的遠端登入對應至本機登入 `Albert` 的項目。  
  
```  
EXEC sp_dropremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-dropping-a-remote-user"></a>C. 卸除遠端使用者  
 下列範例會針對遠端伺服器 `Chris` 上對應至本機登入 `ACCOUNTS` 的遠端登入 `salesmgr`，而移除登入。  
  
```  
EXEC sp_dropremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addremotelogin &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_addserver &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpremotelogin &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
