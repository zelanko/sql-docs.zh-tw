---
title: "sp_dropremotelogin (TRANSACT-SQL) |Microsoft 文件"
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
- sp_dropremotelogin
- sp_dropremotelogin_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_dropremotelogin
ms.assetid: 9f097652-a286-40b2-be73-568d77ada698
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd2ef0424aea68d4d770ddeda9909c9c1a81f4a9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spdropremotelogin-transact-sql"></a>sp_dropremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  移除對應至本機登入的遠端登入，它可以對執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本機伺服器執行遠端預存程序。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]請改用連結伺服器和連結伺服器預存程序。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@remoteserver =** ] **'***remoteserver***'**  
 這是對應至即將移除之遠端登入的遠端伺服器名稱。 *remoteserver*是**sysname**，沒有預設值。 *remoteserver*必須已經存在。  
  
 [  **@loginame =** ] **'***登入***'**  
 這是本機伺服器上與遠端伺服器相關聯的選擇性登入名稱。 *登入*是**sysname**，預設值是 NULL。 *登入*必須已經存在，如果指定。  
  
 [  **@remotename =** ] **'***remote_name***'**  
 對應至的遠端登入的選擇性名稱*登入*登入時，從遠端伺服器。 *remote_name*是**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 如果只有*remoteserver*指定，則所有的遠端登入該遠端伺服器會從本機伺服器移除。 如果*登入*也是指定的所有遠端登入，從*remoteserver*對應至該特定本機登入從本機伺服器中移除。 如果*remote_name*同時指定，只有從該遠端使用者的遠端登入*remoteserver*會從本機伺服器移除。  
  
 若要加入本機伺服器使用者，請使用**sp_addlogin**。 若要移除本機伺服器使用者，請使用**sp_droplogin**。  
  
 只有當您使用舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，才需要遠端登入。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 版和更新的版本，都改用連結伺服器登入。 使用**sp_addlinkedsrvlogin**和**sp_droplinkedsrvlogin**新增和移除連結的伺服器登入。  
  
 **sp_dropremotelogin**無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**sysadmin**或**securityadmin**固定伺服器角色。  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [安全性預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addremotelogin &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_addserver &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpremotelogin &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
