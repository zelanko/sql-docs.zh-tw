---
title: sp_migrate_user_to_contained & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_migrate_user_to_contained
- sp_migrate_user_to_contained_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_migrate_user_to_contained
ms.assetid: b3a49ff6-46ad-4ee7-b6fe-7e54213dc33e
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: da98251792db96d766f63183715bd39f0a394406
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031931"
---
# <a name="spmigrateusertocontained-transact-sql"></a>sp_migrate_user_to_contained (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  將對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的資料庫使用者移轉為具有密碼之自主資料庫使用者。 在自主資料庫中，使用這個程序來移除已安裝資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的相依性。 **sp_migrate_user_to_contained**會分隔使用者與原始[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入，以便可以分別管理設定，例如密碼和預設語言，自主資料庫。 **sp_migrate_user_to_contained**自主的資料庫移至另一個執行個體之前，可以使用[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]消除相依性，目前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的登入。  
  
 **請注意**此程序僅用於自主資料庫中。 如需相關資訊，請參閱 [自主資料庫](../../relational-databases/databases/contained-databases.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_migrate_user_to_contained [ @username = ] N'user' ,   
    [ @rename = ] { N'copy_login_name' | N'keep_name' } ,   
    [ @disablelogin = ] { N'disable_login' | N'do_not_disable_login' }   
```  
  
## <a name="arguments"></a>引數  
 [ **@username =** ] **N'***使用者***'**  
 目前自主資料庫中對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已驗證登入的使用者名稱。 值是**sysname**，預設值是**NULL**。  
  
 [ **@rename =** ] **N'***copy_login_name***'** | **N'***keep_name***'**  
 當登入為基礎的資料庫使用者會有不同的使用者名稱的登入名稱時，使用*keep_name*在移轉期間保留的資料庫使用者名稱。 使用*copy_login_name*來建立新的自主的資料庫使用者的登入，而非使用者名稱。 依據登入的資料庫使用者與登入名稱有相同的使用者名稱時，這兩個選項會在不變更名稱的情況下建立自主資料庫使用者。  
  
 [ **@disablelogin =** ] **N'***disable_login***'** | **N'***do_not_disable_login***'**  
 *disable_login*停用的登入 master 資料庫中。 若要連接的登入已停用時，連接必須提供自主的資料庫名稱做為**初始目錄**為連接字串的一部分。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_migrate_user_to_contained**使用密碼，不論屬性或權限的登入建立自主的資料庫使用者。 例如，程序可以成功登入已停用，或如果使用者拒絕**CONNECT**資料庫的權限。  
  
 **sp_migrate_user_to_contained**具有下列限制。  
  
-   使用者名稱不能已存在於資料庫中。  
  
-   無法轉換內建使用者，例如 dbo 和 guest。  
  
-   無法在中指定的使用者**EXECUTE AS**帶正負號的預存程序的子句。  
  
-   使用者不能擁有包含預存程序**EXECUTE AS OWNER**子句。  
  
-   **sp_migrate_user_to_contained**不能在系統資料庫。  
  
## <a name="security"></a>Security  
 當移轉使用者時，小心不要停用或刪除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的所有系統管理員登入。 如果刪除了所有登入，請參閱[連接到 SQL Server 時系統管理員遭到鎖定](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)。  
  
 如果**BUILTIN\Administrators**登入存在，系統管理員可以透過啟動其應用程式使用連接**系統管理員身分執行**選項。  
  
### <a name="permissions"></a>Permissions  
 需要 **CONTROL SERVER** 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-migrating-a-single-user"></a>A. 移轉單一使用者  
 下列範例會將名為 `Barry` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入移轉為具有密碼之自主資料庫使用者。 此範例會保留使用者名稱，而且將登入保留為已啟用。  
  
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
  
  
