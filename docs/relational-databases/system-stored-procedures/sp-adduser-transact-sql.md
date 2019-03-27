---
title: sp_adduser (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_adduser
- sp_adduser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adduser
ms.assetid: 61a40eb4-573f-460c-9164-bd1bbfaf8b25
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 46b1548f1eb587aa62c0d0427661d97d97bf3cc7
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492936"
---
# <a name="spadduser-transact-sql"></a>sp_adduser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將新的使用者加入目前資料庫中。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE USER](../../t-sql/statements/create-user-transact-sql.md)改。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_adduser [ @loginame = ] 'login'   
    [ , [ @name_in_db = ] 'user' ]   
    [ , [ @grpname = ] 'role' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @loginame = ] 'login'` 名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入或 Windows 登入。 *登入*已**sysname**，沒有預設值。 *登入*必須是現有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入或 Windows 登入。  
  
`[ @name_in_db = ] 'user'` 是新的資料庫使用者的名稱。 *使用者*已**sysname**，預設值是 NULL。 如果*使用者*未指定，則新的資料庫使用者名稱預設為*登入*名稱。 指定*使用者*給予新使用者名稱和伺服器層級登入名稱不同資料庫中。  
  
`[ @grpname = ] 'role'` 是的新使用者成為成員的資料庫角色。 *角色*已**sysname**，預設值是 NULL。 *角色*必須是目前資料庫中的有效資料庫角色。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_adduser**也會建立結構描述中有使用者的名稱。  
  
 在加入使用者之後，請使用 GRANT、DENY 和 REVOKE 陳述式來定義控制該使用者執行之活動的權限。  
  
 使用**sys.server_principals**顯示一份有效的登入名稱。  
  
 使用**sp_helprole**顯示一份有效的角色名稱。 當您指定角色時，使用者會自動取得為該角色定義的權限。 如果未指定角色，使用者會獲得授與預設的權限**公開**角色。 若要將使用者新增至角色，值*使用者名*必須提供。 (*使用者名稱*可以是相同*login_id*。)  
  
 使用者**客體**已存在於每個資料庫。 將使用者新增**客體**可讓這個使用者而言，如果之前已停用。 根據預設，使用者**客體**新的資料庫中已停用。  
  
 **sp_adduser**無法在使用者自訂交易內執行。  
  
 No puede agregar**客體**使用者因為**客體**使用者已經存在每一個資料庫。 若要啟用**客體**使用者，授與**客體**CONNECT 權限所示：  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的擁有權。  
  
## <a name="examples"></a>範例  
  
### <a name="a-adding-a-database-user"></a>A. 加入資料庫使用者  
 下列範例會利用現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `Vidur`，將資料庫使用者 `Recruiting` 加入目前資料庫現有的 `Vidur` 角色中。  
  
```  
EXEC sp_adduser 'Vidur', 'Vidur', 'Recruiting';  
```  
  
### <a name="b-adding-a-database-user-with-the-same-login-id"></a>B. 以相同的登入識別碼，加入資料庫使用者  
 下列範例會針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `Arvind`，將使用者 `Arvind` 加入目前資料庫中。 此使用者屬於預設**公開**角色。  
  
```  
EXEC sp_adduser 'Arvind';  
```  
  
### <a name="c-adding-a-database-user-with-a-different-name-than-its-server-level-login"></a>C. 以不同於伺服器層級登入的名稱，加入資料庫使用者  
 下列範例會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `BjornR` 加入具有使用者名稱 `Bjorn` 的目前資料庫中，並且將資料庫使用者 `Bjorn` 加入 `Production` 資料庫角色中。  
  
```  
EXEC sp_adduser 'BjornR', 'Bjorn', 'Production';  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
