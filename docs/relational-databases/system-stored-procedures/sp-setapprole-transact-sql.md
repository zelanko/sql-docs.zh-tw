---
title: "sp_setapprole (TRANSACT-SQL) |Microsoft 文件"
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
- sp_setapprole
- sp_setapprole_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_setapprole
ms.assetid: cf0901c0-5f90-42d4-9d5b-8772c904062d
caps.latest.revision: "42"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc1376391dcf0fefd0fb621d73817b8257b95bf9
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spsetapprole-transact-sql"></a>sp_setapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  啟動目前資料庫中，與應用程式角色相關聯的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_setapprole [ @rolename = ] 'role',  
    [ @password = ] { encrypt N'password' }   
      |  
        'password' [ , [ @encrypt = ] { 'none' | 'odbc' } ]  
        [ , [ @fCreateCookie = ] true | false ]  
    [ , [ @cookie = ] @cookie OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@rolename =** ] **'***角色***'**  
 目前資料庫所定義之應用程式角色的名稱。 *角色*是**sysname**，沒有預設值。 *角色*必須存在於目前的資料庫。  
  
 [  **@password =** ] **{加密 N'***密碼***'}**  
 啟動應用程式角色所需的密碼。 *密碼*是**sysname**，沒有預設值。 *密碼*可以利用 ODBC 來模糊化**加密**函式。 當您使用**加密**函式，密碼必須轉換成 Unicode 字串放入**N**第一個引號之前。  
  
 使用的連接不支援加密 選項**SqlClient**。  
  
> [!IMPORTANT]  
>  ODBC**加密**函式不會提供加密。 您不應該依賴這個函數來保護透過網路傳輸的密碼。 若要透過網路傳輸這項資訊，請使用 SSL 或 IPSec。  
  
 **@encrypt= 'none'**  
 指定不使用模糊化。 密碼會以純文字格式傳遞至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這是預設值。  
  
 **@encrypt= 'odbc'**  
 指定 ODBC 將模糊化密碼，使用 ODBC**加密**密碼傳送至之前的函式[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。 只有在使用 ODBC 用戶端或 SQL Server 的 OLE DB Provider 時才可以作這項指定。  
  
 [  **@fCreateCookie =** ] **true** | **false**  
 指定是否要建立 Cookie。 **true**會隱含地轉換成 1。 **false**隱含地轉換成 0。  
  
 [  **@cookie =** ]  **@cookie輸出**  
 指定輸出參數要包含該 Cookie。 才會產生 cookie 的值 **@fCreateCookie** 是**true**。 **varbinary （8000)**  
  
> [!NOTE]  
>  **sp_setapprole** 的 Cookie **OUTPUT** 參數目前記載成 **varbinary(8000)** ，這是正確的長度上限。 但目前的實作會傳回 **varbinary(50)**。 應用程式應繼續保留**varbinary （8000)** ，讓應用程式能夠繼續正常運作的 cookie 傳回大小如有增加未來的版本。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 和 1 (失敗)  
  
## <a name="remarks"></a>備註  
 應用程式後啟動角色使用**sp_setapprole**，角色會保持作用中直到使用者從伺服器中斷連接或執行**sp_unsetapprole**。 **sp_setapprole**可以執行只能利用直接[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。 **sp_setapprole**另一個預存程序內或在使用者自訂交易內，無法執行。  
  
 如需應用程式角色的概觀，請參閱[應用程式角色](../../relational-databases/security/authentication-access/application-roles.md)。  
  
> [!IMPORTANT]  
>  若要保護透過網路傳輸的應用程式角色密碼，您一定要在啟用應用程式角色時使用加密的連接。  
>   
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC**加密**選項不支援**SqlClient**。 如果必須保存認證，請利用 crypto API 函數來加密認證。 參數*密碼*儲存為單向雜湊。 若要保留與舊版的相容性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，密碼複雜性原則不會強制執行**sp_addapprole**。 若要強制執行密碼複雜性原則，請使用[CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**公用**和角色的密碼的知識。  
  
## <a name="examples"></a>範例  
  
### <a name="a-activating-an-application-role-without-the-encrypt-option"></a>A. 不使用加密選項而啟動應用程式角色  
 下列範例會啟動一個名為 `SalesAppRole` 的應用程式角色，其純文字密碼為 `AsDeF00MbXX`，而且是利用專門針對目前的使用者使用之應用程式設計的權限來建立的。  
  
```  
EXEC sp_setapprole 'SalesApprole', 'AsDeF00MbXX';  
GO  
```  
  
### <a name="b-activating-an-application-role-with-a-cookie-and-then-reverting-to-the-original-context"></a>B. 啟動內含 Cookie 的應用程式角色，再還原成原始內容  
 下列範例會啟動含有密碼 `Sales11` 的 `fdsd896#gfdbfdkjgh700mM` 應用程式角色，然後建立 Cookie。 這個範例會傳回目前使用者的名稱，然後執行 `sp_unsetapprole` 來還原為原始內容。  
  
```  
DECLARE @cookie varbinary(8000);  
EXEC sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.   
GO   
```  
  
## <a name="see-also"></a>請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全性預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [建立應用程式角色 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [sp_unsetapprole &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md)  
  
  
