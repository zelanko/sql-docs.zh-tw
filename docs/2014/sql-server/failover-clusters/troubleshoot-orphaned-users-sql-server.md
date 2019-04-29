---
title: 被遺棄使用者疑難排解 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- orphaned users [SQL Server]
- logins [SQL Server], orphaned users
- troubleshooting [SQL Server], user accounts
- user accounts [SQL Server], orphaned users
- failover [SQL Server], managing metadata
- database mirroring [SQL Server], metadata
- users [SQL Server], orphaned
ms.assetid: 11eefa97-a31f-4359-ba5b-e92328224133
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 38a33b34b64cf285e94f66c547b2309b8daf1ae8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63035653"
---
# <a name="troubleshoot-orphaned-users-sql-server"></a>被遺棄使用者疑難排解 (SQL Server)
  若要登入 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，則主體必須提供有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 此登入是用於驗證處理序，可確認是否允許該主體連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入伺服器執行個體上的會顯示在**sys.server_principals**目錄檢視和**sys.syslogins**相容性檢視。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入會使用對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的資料庫使用者來存取個別資料庫。 這項規則有兩個例外狀況：  
  
-   guest 帳戶  
  
     在資料庫中啟用此帳戶時，會使未對應到資料庫使用者的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入都能以 guest 使用者的身分進入資料庫。  
  
-   Microsoft Windows 群組成員資格。  
  
     如果 Windows 使用者是 Windows 群組的成員，而且也是資料庫中的使用者，則從 Windows 使用者建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入可進入該資料庫。  
  
 有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入對應到資料庫使用者的資訊會儲存在資料庫內。 它包括資料庫使用者的名稱和對應之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的 SID。 此資料庫使用者的權限使用於資料庫中的授權。  
  
 在伺服器執行個體上未定義或定義不正確之對應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的資料庫使用者無法登入此執行個體。 這類使用者就是伺服器執行個體上的資料庫 *「被遺棄使用者」* (Orphaned User)。 如果卸除了對應的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，則資料庫使用者可能遭到遺棄。 此外，資料庫還原或附加到其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，也會讓資料庫使用者遭到遺棄。 如果資料庫使用者對應到的 SID 未出現在新的伺服器執行個體中，則會遭到遺棄。  
  
> [!NOTE]  
>  A[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入無法存取的資料庫，在其中缺少對應資料庫使用者除非**客體**啟用該資料庫中。 如需建立資料庫使用者帳戶資訊，請參閱 < [CREATE USER &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)。  
  
## <a name="to-detect-orphaned-users"></a>若要偵測被遺棄使用者  
 若要偵測被遺棄使用者，請執行以下 Transact-SQL 陳述式：  
  
```  
USE <database_name>;  
GO;   
sp_change_users_login @Action='Report';  
GO;  
```  
  
 輸出會列出使用者及對應的安全性識別碼 (SID)，這些使用者皆為目前資料庫中的使用者，且並未與任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入有連結。 如需詳細資訊，請參閱 < [sp_change_users_login &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql)。  
  
> [!NOTE]  
>  **sp_change_users_login**不能搭配[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從 Windows 建立登入。  
  
## <a name="to-resolve-an-orphaned-user"></a>若要解析被遺棄使用者  
 若要解析被遺棄使用者，請使用以下程序：  
  
1.  下列命令會重新連結伺服器登入帳戶所指定 *< login_name >* 與所指定的資料庫使用者 *< database_user >*。  
  
    ```  
    USE <database_name>;  
    GO  
    sp_change_users_login @Action='update_one', @UserNamePattern='<database_user>', @LoginName='<login_name>';  
    GO  
  
    ```  
  
     如需詳細資訊，請參閱 < [sp_change_users_login &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql)。  
  
2.  執行先前步驟中的程式碼後，使用者就能夠存取伺服器。 使用者接著可以改變的密碼 *< login_name >* 使用的登入帳戶**sp_password**預存程序，如下所示：  
  
    ```  
    USE master   
    GO  
    sp_password @old=NULL, @new='password', @loginame='<login_name>';  
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  只有具有 ALTER ANY LOGIN 權限的登入，才能夠變更其他使用者登入的密碼。 不過，只有 **sysadmin** 角色成員才能修改 **sysadmin** 角色成員的密碼。  
  
    > [!NOTE]  
    >  **sp_password**無法用於[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 帳戶。 透過 Windows 網路帳戶連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的使用者是由 Windows 驗證，因此他們的密碼只能在 Windows 中變更。  
  
     如需詳細資訊，請參閱 < [sp_password &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [sp_change_users_login &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql)   
 [sp_addlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)   
 [sp_grantlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-grantlogin-transact-sql)   
 [sp_password &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql)   
 [sys.sysusers &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysusers-transact-sql)   
 [sys.syslogins &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslogins-transact-sql)  
  
  
