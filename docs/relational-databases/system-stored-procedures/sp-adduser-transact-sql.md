---
title: sp_adduser （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: a2984479c8a1be35f8ccfa63d14b3250939f56c3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68117896"
---
# <a name="sp_adduser-transact-sql"></a>sp_adduser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將新的使用者加入目前資料庫中。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[CREATE USER](../../t-sql/statements/create-user-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_adduser [ @loginame = ] 'login'   
    [ , [ @name_in_db = ] 'user' ]   
    [ , [ @grpname = ] 'role' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @loginame = ] 'login'`這是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入或 Windows 登入的名稱。 *登*入是**sysname**，沒有預設值。 *login*必須是現有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的登入或 Windows 登入。  
  
`[ @name_in_db = ] 'user'`這是新資料庫使用者的名稱。 *user*是**sysname**，預設值是 Null。 如果未指定*user* ，新資料庫使用者的名稱就會預設為*登*入名稱。 指定*user*可讓新使用者在資料庫中的名稱與伺服器層級的登入名稱不同。  
  
`[ @grpname = ] 'role'`這是新使用者成為其成員的資料庫角色。 *role*是**sysname**，預設值是 Null。 *role*必須是目前資料庫中的有效資料庫角色。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_adduser**也會建立一個具有使用者名稱的架構。  
  
 在加入使用者之後，請使用 GRANT、DENY 和 REVOKE 陳述式來定義控制該使用者執行之活動的權限。  
  
 使用 [ **sys.databases] server_principals**顯示有效登入名稱的清單。  
  
 使用 [ **sp_helprole**顯示有效角色名稱的清單。 當您指定角色時，使用者會自動取得為該角色定義的權限。 如果未指定角色，使用者會取得授與預設**public**角色的許可權。 若要將使用者新增至角色，必須提供*使用者名稱*的值。 （使用者*名稱*可以與*login_id*相同）。  
  
 使用者**來賓**已存在於每個資料庫中。 新增使用者**來賓**將會啟用此使用者（如果之前已停用）。 預設會在新的資料庫中停用使用者**來賓**。  
  
 **sp_adduser**不能在使用者自訂交易內執行。  
  
 您無法新增**來賓**使用者，因為每個資料庫中已有**來賓**使用者。 若要啟用**來賓**使用者，請授與**guest** CONNECT 許可權，如下所示：  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
## <a name="permissions"></a>權限  
 需要資料庫的擁有權。  
  
## <a name="examples"></a>範例  
  
### <a name="a-adding-a-database-user"></a>A. 加入資料庫使用者  
 下列範例會利用現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `Vidur`，將資料庫使用者 `Recruiting` 加入目前資料庫現有的 `Vidur` 角色中。  
  
```  
EXEC sp_adduser 'Vidur', 'Vidur', 'Recruiting';  
```  
  
### <a name="b-adding-a-database-user-with-the-same-login-id"></a>B. 以相同的登入識別碼，加入資料庫使用者  
 下列範例會針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `Arvind`，將使用者 `Arvind` 加入目前資料庫中。 此使用者屬於預設的**public**角色。  
  
```  
EXEC sp_adduser 'Arvind';  
```  
  
### <a name="c-adding-a-database-user-with-a-different-name-than-its-server-level-login"></a>C. 以不同於伺服器層級登入的名稱，加入資料庫使用者  
 下列範例會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `BjornR` 加入具有使用者名稱 `Bjorn` 的目前資料庫中，並且將資料庫使用者 `Bjorn` 加入 `Production` 資料庫角色中。  
  
```  
EXEC sp_adduser 'BjornR', 'Bjorn', 'Production';  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性預存程式](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [server_principals &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
