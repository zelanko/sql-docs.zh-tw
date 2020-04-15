---
title: sp_setapprole(轉算 SQL) |微軟文件
ms.custom: ''
ms.date: 10/12/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_setapprole
- sp_setapprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setapprole
ms.assetid: cf0901c0-5f90-42d4-9d5b-8772c904062d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b158c4571deadadeaee23ffa6e46eb48a8c8446e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299594"
---
# <a name="sp_setapprole-transact-sql"></a>sp_setapprole (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  啟動目前資料庫中，與應用程式角色相關聯的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  

```sql
sp_setapprole [ @rolename = ] 'role',  
    [ @password = ] { encrypt N'password' }
      |  
        'password' [ , [ @encrypt = ] { 'none' | 'odbc' } ]  
        [ , [ @fCreateCookie = ] true | false ]  
    [ , [ @cookie = ] @cookie OUTPUT ]  
```

## <a name="arguments"></a>引數

`[ @rolename = ] 'role'`是當前資料庫中定義的應用程式角色的名稱。 *角色*是**sysname,** 沒有預設值。 *角色*必須存在於當前資料庫中。  
  
`[ @password = ] { encrypt N'password' }`是啟動應用程式角色所需的密碼。 *密碼*是**sysname,** 沒有預設值。 密碼*可以使用*ODBC**加密**功能進行模糊處理。 使用**加密**函數時,密碼必須透過在第一個引號之前放置**N**轉換為Unicode字串。  
  
 使用**SqlClient**的連線不支援加密選項。  
  
> [!IMPORTANT]  
> ODBC**加密**功能不提供加密。 您不應該依賴這個函數來保護透過網路傳輸的密碼。 如果此資訊將透過網路傳輸,請使用 TLS 或 IPSec。
  
 **@encrypt• "無"**  
 指定不使用模糊化。 密碼會以純文字格式傳遞至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這是預設值。  
  
 **@encrypt• "奧德布"**  
 指定 ODBC 在將密碼傳送到**encrypt**之前使用 ODBC[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]加密功能混淆密碼 。 只有在使用 ODBC 用戶端或 SQL Server 的 OLE DB Provider 時才可以作這項指定。  
  
`[ @fCreateCookie = ] true | false`指定是否要創建 Cookie。 **true**隱式轉換為 1。 **false**隱式轉換為 0。  
  
`[ @cookie = ] @cookie OUTPUT`指定包含 Cookie 的輸出參數。 僅當**\@fCreateCookie**的值**為 true**時,才會生成 Cookie。 **varbinary(8000)**  
  
> [!NOTE]  
> **sp_setapprole** 的 Cookie **OUTPUT** 參數目前記載成 **varbinary(8000)** ，這是正確的長度上限。 但目前的實作會傳回 **varbinary(50)**。 應用程式應繼續保留**varbinary(8000),** 以便在將來版本中 Cookie 返回大小增加時應用程式繼續正常運行。
  
## <a name="return-code-values"></a>傳回碼值

 0 (成功) 和 1 (失敗)  
  
## <a name="remarks"></a>備註

 使用**sp_setapprole**啟動應用程式角色後,該角色將保持活動狀態,直到使用者斷開與伺服器的連線或執行**sp_unsetapprole**。 **sp_setapprole**只能由[!INCLUDE[tsql](../../includes/tsql-md.md)]直接 語句執行。 **sp_setapprole**不能在另一個存儲過程或使用者定義的事務中執行。  
  
 有關應用程式角色的概述,請參閱[應用程式角色](../../relational-databases/security/authentication-access/application-roles.md)。  
  
> [!IMPORTANT]  
> 為了在應用程式角色密碼通過網路傳輸時保護它,在啟用應用程式角色時應始終使用加密連接。
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] **SqlClient**不支援 ODBC**加密**選項。 如果必須保存認證，請利用 crypto API 函數來加密認證。 參數*密碼*儲存為單向哈希。 為了保持與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]早期版本的 的相容性 **,sp_addapprole**不強制執行密碼複雜性策略。 要強制進行密碼複雜性原則,請使用[建立應用程式角色](../../t-sql/statements/create-application-role-transact-sql.md)。  
  
## <a name="permissions"></a>權限

需要**成為公共**成員,並瞭解角色的密碼。  
  
## <a name="examples"></a>範例  
  
### <a name="a-activating-an-application-role-without-the-encrypt-option"></a>A. 不使用加密選項而啟動應用程式角色

 下列範例會啟動一個名為 `SalesAppRole` 的應用程式角色，其純文字密碼為 `AsDeF00MbXX`，而且是利用專門針對目前的使用者使用之應用程式設計的權限來建立的。

```sql
EXEC sys.sp_setapprole 'SalesApprole', 'AsDeF00MbXX';  
GO
```

### <a name="b-activating-an-application-role-with-a-cookie-and-then-reverting-to-the-original-context"></a>B. 啟動內含 Cookie 的應用程式角色，再還原成原始內容

 下列範例會啟動含有密碼 `Sales11` 的 `fdsd896#gfdbfdkjgh700mM` 應用程式角色，然後建立 Cookie。 這個範例會傳回目前使用者的名稱，然後執行 `sp_unsetapprole` 來還原為原始內容。  

```sql
DECLARE @cookie varbinary(8000);  
EXEC sys.sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sys.sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.
GO
```

## <a name="see-also"></a>另請參閱

 [系統儲存過程&#40;處理-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)[安全儲存過程&#40;處理-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)[創建應用程式角色&#40;處理-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md) [DROP 應用角色&#40;處理-SQL](../../t-sql/statements/drop-application-role-transact-sql.md) [&#41;sp_unsetapprole&#40;處理-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md)
