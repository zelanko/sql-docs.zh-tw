---
description: sp_migrate_user_to_contained (Transact-SQL)
title: sp_migrate_user_to_contained (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/11/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_migrate_user_to_contained
- sp_migrate_user_to_contained_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_migrate_user_to_contained
ms.assetid: b3a49ff6-46ad-4ee7-b6fe-7e54213dc33e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 95bd2aa7491b15b2e16172b0761c6dccc8eb5818
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446930"
---
# <a name="sp_migrate_user_to_contained-transact-sql"></a>sp_migrate_user_to_contained (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的資料庫使用者移轉為具有密碼之自主資料庫使用者。 在自主資料庫中，使用這個程序來移除已安裝資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的相依性。 **sp_migrate_user_to_contained** 會將使用者與原始登入分開 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，以便針對自主資料庫分別管理密碼和預設語言等設定。 **sp_migrate_user_to_contained** 可以在將自主資料庫移至不同的實例之前使用， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 以消除目前實例登入的相依性 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
> [!NOTE]
> 使用 **sp_migrate_user_to_contained**時請小心，因為您將無法反轉效果。 此程式只會在自主資料庫中使用。 如需詳細資訊，請參閱自主 [資料庫](../../relational-databases/databases/contained-databases.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_migrate_user_to_contained [ @username = ] N'user' ,   
    [ @rename = ] { N'copy_login_name' | N'keep_name' } ,   
    [ @disablelogin = ] { N'disable_login' | N'do_not_disable_login' }   
```  
  
## <a name="arguments"></a>引數  
 [** @username =** ] **N '***使用者***'**  
 目前自主資料庫中對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已驗證登入的使用者名稱。 此值為 **sysname**，預設值是 **Null**。  
  
 [** @rename =** ] **N '***copy_login_name***'**  | **N '***keep_name***'**  
 當以登入為基礎的資料庫使用者與登入名稱具有不同的使用者名稱時，請使用 *keep_name* 在遷移期間保留資料庫的使用者名稱。 使用 *copy_login_name* 以登入的名稱建立新的自主資料庫使用者，而不是使用者。 依據登入的資料庫使用者與登入名稱有相同的使用者名稱時，這兩個選項會在不變更名稱的情況下建立自主資料庫使用者。  
  
 [** @disablelogin =** ] **N '***disable_login***'**  | **N '***do_not_disable_login***'**  
 *disable_login* 停用 master 資料庫中的登入。 若要在停用登入時進行連接，連接必須提供自主資料庫名稱做為連接字串的一部分做為 **初始目錄** 。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_migrate_user_to_contained** 使用密碼建立自主資料庫使用者，而不論登入的屬性或許可權為何。 例如，如果已停用登入，或如果使用者拒絕資料庫的 **CONNECT** 許可權，程式就會成功。  
  
 **sp_migrate_user_to_contained** 具有下列限制。  
  
-   使用者名稱不能已存在於資料庫中。  
  
-   無法轉換內建使用者，例如 dbo 和 guest。  
  
-   使用者無法在已簽署之預存程式的 **EXECUTE AS** 子句中指定。  
  
-   使用者無法擁有包含 **EXECUTE AS OWNER** 子句的預存程式。  
  
-   **sp_migrate_user_to_contained** 不能用在系統資料庫中。  
  
## <a name="security"></a>安全性  
 當移轉使用者時，小心不要停用或刪除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的所有系統管理員登入。 如果刪除所有登入，請參閱 [當系統管理員遭到鎖定時連接到 SQL Server](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)。  
  
 如果有 **BUILTIN\Administrators** 登入，系統管理員可以使用 [以 **系統管理員身分執行** ] 選項啟動其應用程式來進行連線。  
  
### <a name="permissions"></a>權限  
 需要 **CONTROL SERVER** 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-migrating-a-single-user"></a>A. 移轉單一使用者  
 下列範例會將名為 `Barry` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入移轉為具有密碼之自主資料庫使用者。 此範例不會變更使用者名稱，而且會保留已啟用的登入。  
  
```sql  
sp_migrate_user_to_contained   
@username = N'Barry',  
@rename = N'keep_name',  
@disablelogin = N'do_not_disable_login' ;  
  
```  
  
### <a name="b-migrating-all-database-users-with-logins-to-contained-database-users-without-logins"></a>B. 將所有具有登入的資料庫使用者移轉為沒有登入的自主資料庫使用者  
 下列範例會將以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入為基礎的所有使用者移轉至具有密碼之自主資料庫使用者。 此範例會排除未啟用的登入。 您必須在自主資料庫中執行此範例。  
  
```sql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)   
 [自主資料庫](../../relational-databases/databases/contained-databases.md)  
  
  
