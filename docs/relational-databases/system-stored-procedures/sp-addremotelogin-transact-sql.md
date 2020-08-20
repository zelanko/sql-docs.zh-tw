---
description: sp_addremotelogin (Transact-SQL)
title: sp_addremotelogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addremotelogin_TSQL
- sp_addremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addremotelogin
ms.assetid: 71b7cd36-a17d-4b12-b102-10aeb0f9268b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: de4f54972fb4a749e6466a81fef88ae8630be698
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464610"
---
# <a name="sp_addremotelogin-transact-sql"></a>sp_addremotelogin (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  在本機伺服器上加入新的遠端登入識別碼。 此舉可讓遠端伺服器連接及執行遠端程序呼叫。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]請改用連結伺服器和連結伺服器預存程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>引數  
 [ @remoteserver **=** ] **'**_remoteserver_**'**  
 這是遠端登入所套用的遠端伺服器名稱。 *remoteserver* 是 **sysname**，沒有預設值。 如果只指定 *remoteserver* ， *remoteserver* 上的所有使用者都會對應到本機伺服器上相同名稱的現有登入。 本機伺服器必須知道這部伺服器。 它可以利用 sp_addserver 加入。 當 *remoteserver* 上的使用者連接到執行的本機伺服器 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以執行遠端預存程式時，它們會以本機登入來連接，以符合其在 *remoteserver*上的登入。 *remoteserver* 是起始遠端程序呼叫的伺服器。  
  
 [ @loginame **=** ] **'**_login_**'**  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本機執行個體上的使用者登入識別碼。 *login* 是預設值為 NULL 的 **sysname**。 *登*入必須已經存在於的本機實例上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果指定 *login* ， *remoteserver* 上的所有使用者都會對應至該特定的本機登入。 當 *remoteserver* 上的使用者連接到的本機實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以執行遠端預存程式時，它們會以 *登*入方式連接。  
  
 [ @remotename **=** ] **'**_remote_name_**'**  
 這是遠端伺服器上的使用者登入識別碼。 *remote_name* 是 **sysname**，預設值是 Null。 *remote_name* 必須存在於 *remoteserver*上。 如果指定 *remote_name* ，特定的使用者 *remote_name* 會對應到本機伺服器上的 *登* 入。 當*remoteserver*上*remote_name*連接到的本機實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，以執行遠端預存程式時，它會以*登*入方式連接。 *Remote_name*的登入識別碼可以與遠端伺服器上的登入識別碼不同，*登*入。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 若要執行分散式查詢，請使用 sp_addlinkedsrvlogin。  
  
 sp_addremotelogin 無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>權限  
 只有系統管理員 (sysadmin) 和安全性管理員 (securityadmin) 固定伺服器角色的成員，才能夠執行 sp_addremotelogin。  
  
## <a name="examples"></a>範例  
  
### <a name="a-mapping-one-to-one"></a>A. 一對一對應  
 下列範例是在遠端伺服器 `ACCOUNTS` 和本機伺服器具有相同的使用者登入時，將遠端名稱對應至本機名稱。  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-mapping-many-to-one"></a>B. 多對一對應  
 下列範例會建立一個項目，將遠端伺服器 `ACCOUNTS` 上所有的使用者，對應至本機登入識別碼 `Albert`。  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-using-explicit-one-to-one-mapping"></a>C. 使用明確的一對一對應  
 下列範例會將來自遠端伺服器 `Chris` 上遠端使用者 `ACCOUNTS` 的遠端登入，對應至本機使用者 `salesmgr`。  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [sp_revokelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
