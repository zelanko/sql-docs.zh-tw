---
title: "被遺棄使用者疑難排解 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 07/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- orphaned users [SQL Server]
- logins [SQL Server], orphaned users
- troubleshooting [SQL Server], user accounts
- user accounts [SQL Server], orphaned users
- failover [SQL Server], managing metadata
- database mirroring [SQL Server], metadata
- users [SQL Server], orphaned
ms.assetid: 11eefa97-a31f-4359-ba5b-e92328224133
caps.latest.revision: 41
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5f76cf5789d67f93443149074b0c4e8708f90000
ms.lasthandoff: 04/11/2017

---
# <a name="troubleshoot-orphaned-users-sql-server"></a>被遺棄使用者疑難排解 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的被遺棄使用者，當資料庫中的使用者登入是根據 **master** 資料庫，但登入已不存在於 **master**時就會發生。 當登入遭到刪除，或當資料庫移動到另一個登入不存在的資料庫時，就可能發生。 本主題說明如何尋找被遺棄使用者，並將他們重新對應至登入。  
  
> [!NOTE]  
>  針對可能會移動的資料庫，使用自主資料庫使用者可減少被遺棄使用者產生的可能性。 如需詳細資訊，請參閱 [自主資料庫使用者 - 使資料庫可攜](../../relational-databases/security/contained-database-users-making-your-database-portable.md)。  
  
## <a name="background"></a>背景  
 若要使用以登入為基礎的安全性主體 (資料庫使用者身分識別) 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的資料庫，主體在 **master** 資料庫必須有有效的登入。 此登入適用於驗證程序，可確認主體身份識別並決定主體是否允許連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。 伺服器執行個體上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入可以在 **sys.server_principals** 目錄檢視和 **sys.sql_logins** 相容性檢視中看到。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入會以對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的「資料庫使用者」來存取個別資料庫。 這項規則有三個例外狀況：  
  
-   自主資料庫使用者  
  
     自主資料庫使用者驗證位於使用者資料庫層級，且與登入沒有關連。 這是建議項目，因為資料庫會有更佳的可攜性，且自主資料庫使用者不會成為被遺棄使用者。 不過，它們也必須在每個資料庫上重新建立。 這在具有許多資料庫的環境中並不實用。  
  
-   **guest** 帳戶。  
  
     在資料庫中啟用時，此帳戶會使未對應到資料庫使用者的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入都能以 **guest** 使用者的身分進入資料庫。 **guest** 帳戶預設為停用。  
  
-   Microsoft Windows 群組成員資格。  
  
     如果 Windows 使用者是 Windows 群組的成員，而且也是資料庫中的使用者，則從 Windows 使用者建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入可進入該資料庫。  
  
 有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入對應到資料庫使用者的資訊會儲存在資料庫內。 它包括資料庫使用者的名稱和對應之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的 SID。 此資料庫使用者的權限適用於資料庫中的授權。  
  
 在伺服器執行個體上未定義或定義不正確之對應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的資料庫使用者 (以登入為基礎) 無法登入此執行個體。 這類使用者就是伺服器執行個體上的資料庫 *「被遺棄使用者」* (Orphaned User)。 如果資料庫使用者對應到的登入 SID 未出現在 `master` 執行個體中，則會遭到遺棄。 資料庫還原或附加到其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未建立登入的執行個體，也會讓資料庫使用者遭到遺棄。 如果卸除了對應的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，則資料庫使用者也會遭到遺棄。 即使重新建立登入，它的 SID 也會不同，因此資料庫使用者仍會遭到遺棄。  
  
## <a name="to-detect-orphaned-users"></a>若要偵測被遺棄使用者  

**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 PDW**

若要根據遺失的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入來偵測 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的孤立使用者，請在使用者資料庫中執行下列陳述式：  
  
```  
SELECT dp.type_desc, dp.SID, dp.name AS user_name  
FROM sys.database_principals AS dp  
LEFT JOIN sys.server_principals AS sp  
    ON dp.SID = sp.SID  
WHERE sp.SID IS NULL  
    AND authentication_type_desc = 'INSTANCE';  
```  
  
 輸出會列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證使用者及對應的安全性識別碼 (SID)，這些使用者皆為目前資料庫中的使用者，且並未與任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入相連結。  

**SQL 資料庫和 SQL 資料倉儲**

`sys.server_principals` 資料表不適用於 SQL 資料庫或 SQL 資料倉儲。 請執行下列步驟來識別這些環境中的孤立使用者：

1. 連接到 `master` 資料庫，然後使用下列查詢選取登入的 SID：
    ```
    SELECT sid 
    FROM sys.sql_logins 
    WHERE type = 'S'; 
    ```

2. 連接到使用者資料庫，然後使用下列查詢檢閱 `sys.database_principals` 資料表中的使用者 SID：

    ```
    SELECT name, sid, principal_id
    FROM sys.database_principals 
    WHERE type = 'S' 
      AND name NOT IN ('guest', 'INFORMATION_SCHEMA', 'sys')
      AND authentication_type_desc = 'INSTANCE';
    ```

3. 比較這兩份清單，以判斷使用者資料庫 `sys.database_principals` 資料表中是否有使用者 SID 不符合 master 資料庫 `sql_logins` 資料表中的登入 SID。 
  
## <a name="to-resolve-an-orphaned-user"></a>若要解析被遺棄使用者  
在 master 資料庫中，使用 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 陳述式搭配 SID 選項以重新建立遺失的登入，提供在上一節取得之資料庫使用者的 `SID` ：  
  
```  
CREATE LOGIN <login_name>   
WITH PASSWORD = '<use_a_strong_password_here>',  
SID = <SID>;  
```  
  
 若要將孤立使用者對應到已存在 **master**中的登入，請在使用者資料庫中執行 [ALTER USER](../../t-sql/statements/alter-user-transact-sql.md) 陳述式，並指定登入名稱。  
  
```  
ALTER USER <user_name> WITH Login = <login_name>;  
```  
  
 當您重新建立遺失的登入時，使用者可以使用提供的密碼存取資料庫。 接著使用者可以使用 ALTER LOGIN 陳述式改變登入帳戶的密碼。  
  
```  
ALTER LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
```  
  
> [!IMPORTANT]  
>  任何登入都可以變更其密碼。 只有具有 `ALTER ANY LOGIN` 權限的登入，才能夠變更其他使用者登入的密碼。 不過，只有 **sysadmin** 角色成員才能修改 **sysadmin** 角色成員的密碼。  
  
 已被取代的程序 [sp_change_users_login](../../relational-databases/system-stored-procedures/sp-change-users-login-transact-sql.md) 也適用於孤立使用者。 `sp_change_users_login` 不能搭配 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]使用。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER USER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_change_users_login &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-users-login-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)   
 [sys.sysusers &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysusers-transact-sql.md)   
 [sys.sql_logins](../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)
 [sys.syslogins &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslogins-transact-sql.md)  
  
  

