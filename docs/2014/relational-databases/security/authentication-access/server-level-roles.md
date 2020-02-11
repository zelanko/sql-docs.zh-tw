---
title: 伺服器層級角色 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.Security.BUILTIN.administrators
- sql12.Security.NT_AUTHORITY.SYSTEM
helpviewer_keywords:
- roles [SQL Server], server-level
- principals [SQL Server], server-level
- CONTROL SERVER permission
- fixed server roles [SQL Server]
- credentials [SQL Server], roles
- sysadmin fixed server role
- server-level roles [SQL Server]
- authentication [SQL Server], roles
ms.assetid: 7adf2ad7-015d-4cbe-9e29-abaefd779008
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 95ffdd52ff4c71039a87f177e67d51cb81830c68
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63011929"
---
# <a name="server-level-roles"></a>伺服器層級角色
  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會提供伺服器層級角色來協助您管理伺服器的權限。 這些角色是將其他主體組成群組的安全性主體。 伺服器層級角色的權限範圍為整個伺服器  (「角色」** 就像是 Windows 作業系統中的「群組」**)。  
  
 固定伺服器角色是為了方便和回溯相容性所提供。 請盡可能指派更特定的權限。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供了九種固定伺服器角色。 您無法變更授與固定伺服器角色的權限。 從 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]開始，您就可以建立使用者定義伺服器角色，並將伺服器層級權限加入至使用者定義伺服器角色。  
  
 您可以將伺服器層級主體 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入、Windows 帳戶和 Windows 群組) 加入伺服器層級角色。 固定伺服器角色的每個成員可以對相同的角色增加其他登入。 使用者定義伺服器角色的成員無法將其他伺服器主體加入至此角色。  
  
## <a name="fixed-server-level-roles"></a>固定伺服器層級角色  
 下表顯示固定伺服器層級角色及其功能。  
  
|固定伺服器層級角色|描述|  
|------------------------------|-----------------|  
|系統管理員 (sysadmin)|系統管理員 (sysadmin) 固定伺服器角色的成員可以執行伺服器中的所有活動。|  
|serveradmin|伺服器管理員 (serveradmin) 固定伺服器角色的成員可以變更整個伺服器的組態選項及關閉伺服器。|  
|securityadmin|安全性管理員 (securityadmin) 固定伺服器角色的成員可以管理登入及其屬性。 他們可以 GRANT、DENY 及 REVOKE 伺服器層級權限。 如果他們擁有資料庫的存取權，也可以 GRANT、DENY 和 REVOKE 資料庫層級權限。 此外，他們可以重設 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入的密碼。<br /><br /> ** \* \*安全性\*注意事項**授與存取權[!INCLUDE[ssDE](../../../includes/ssde-md.md)]和設定使用者權限的能力，可讓安全性管理員指派大部分的伺服器許可權。 `securityadmin`角色應視為等同于`sysadmin`角色。|  
|processadmin|處理序管理員 (processadmin) 固定伺服器角色的成員可以結束在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體中執行的處理序。|  
|setupadmin|setupadmin 固定伺服器角色的成員可以使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式加入和移除連結的伺服器 (使用 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]時需要系統管理員成員資格)。|  
|bulkadmin|大量管理員 (bulkadmin) 固定伺服器角色的成員可以執行 BULK INSERT 陳述式。|  
|diskadmin|diskadmin 固定伺服器角色是用來管理磁碟檔案。|  
|dbcreator|資料庫建立者 (dbcreator) 固定伺服器角色的成員可以建立、改變、卸除及還原任何資料庫。|  
|公開|每一個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入都屬於 public 伺服器角色。 當伺服器主體未被授與或拒絕安全性實體物件的特定權限時，該使用者會繼承授與給該物件之 public 的權限。 只有當您想要將任何物件提供給所有使用者使用時，才指派該物件的 public 權限。 您無法變更 public 的成員資格。<br /><br /> 注意：public 的實作方式與其他角色不同。 不過，您可以在 public 中授與、拒絕或撤銷權限。|  
  
## <a name="permissions-of-fixed-server-roles"></a>固定伺服器角色的權限  
 每個固定伺服器角色都擁有指派給它的特定權限。 如需指派給伺服器角色之權限的圖表，請參閱 [Database Engine Fixed Server and Fixed Database Roles](https://social.technet.microsoft.com/wiki/contents/articles/2024.database-engine-fixed-server-and-fixed-database-roles.aspx) (資料庫引擎固定伺服器與固定資料庫角色)。  
  
> [!IMPORTANT]  
>  
  `CONTROL SERVER` 權限與 `sysadmin` 固定伺服器角色類似但沒有完全相同。 權限不代表角色成員資格，角色成員資格也不會授與權限。 (例如， `CONTROL SERVER`不代表固定伺服器角色中`sysadmin`的成員資格）。不過，有時候可以在角色和對等的許可權之間進行模擬。 大部分 `DBCC` 命令與許多系統程序都需要 `sysadmin` 固定伺服器角色中的成員資格。 如需需要`sysadmin`成員資格的171系統預存程式清單，請參閱 Andreas WOLTER [CONTROL SERVER 與 sysadmin/sa 的下列 blog 文章：許可權、系統程式、DBCC、自動建立架構和許可權擴大-注意事項](http://www.insidesql.org/blogs/andreaswolter/2013/08/control-server-vs-sysadmin-sa-permissions-privilege-escalation-caveats)。  
  
## <a name="server-level-permissions"></a>伺服器層級權限  
 只有伺服器層級權限可加入至使用者定義伺服器角色。 若要列出伺服器層級權限，請執行以下陳述式。 伺服器層級權限為：  
  
```sql  
SELECT * FROM sys.fn_builtin_permissions('SERVER') ORDER BY permission_name;  
```  
  
 如需權限的詳細資訊，請參閱[權限 &#40;Database Engine&#41;](../permissions-database-engine.md) 和 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql)。  
  
## <a name="working-with-server-level-roles"></a>處理伺服器層級角色  
 下表將說明可用來處理伺服器層級角色的命令、檢視和函數。  
  
|功能|類型|描述|  
|-------------|----------|-----------------|  
|[sp_helpsrvrole &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql)|中繼資料|傳回伺服器層級角色的清單。|  
|[sp_helpsrvrolemember &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql)|中繼資料|傳回伺服器層級角色成員的相關資訊。|  
|[sp_srvrolepermission &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql)|中繼資料|顯示伺服器層級角色的權限。|  
|[IS_SRVROLEMEMBER &#40;Transact-sql&#41;](/sql/t-sql/functions/is-srvrolemember-transact-sql)|中繼資料|指出 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入是否為指定之伺服器層級角色的成員。|  
|[sys.server_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-role-members-transact-sql)|中繼資料|針對每個伺服器層級角色的每個成員，各傳回一個資料列。|  
|[sp_addsrvrolemember &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql)|Command|加入一個登入，做為伺服器層級角色的成員。 已被取代。 請改用 [ALTER SERVER ROLE](/sql/t-sql/statements/alter-server-role-transact-sql) 。|  
|[sp_dropsrvrolemember &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql)|Command|從伺服器層級角色移除 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入或是 Windows 使用者或群組。 已被取代。 請改用 [ALTER SERVER ROLE](/sql/t-sql/statements/alter-server-role-transact-sql) 。|  
|[建立伺服器角色 &#40;Transact-sql&#41;](/sql/t-sql/statements/create-server-role-transact-sql)|Command|建立使用者定義伺服器角色。|  
|[ALTER SERVER ROLE &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-server-role-transact-sql)|Command|變更伺服器角色的成員資格或變更使用者定義伺服器角色的名稱。|  
|[DROP SERVER ROLE &#40;Transact-sql&#41;](/sql/t-sql/statements/drop-server-role-transact-sql)|Command|移除使用者定義伺服器角色。|  
|[IS_SRVROLEMEMBER &#40;Transact-sql&#41;](/sql/t-sql/functions/is-srvrolemember-transact-sql)|函式|判斷伺服器角色的成員資格。|  
  
## <a name="see-also"></a>另請參閱  
 [資料庫層級角色](../authentication-access/database-level-roles.md)   
 [&#40;Transact-sql&#41;的安全性目錄檢視](/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)   
 [&#40;Transact-sql&#41;的安全性函數](/sql/t-sql/functions/security-functions-transact-sql)   
 [保護 SQL Server](../securing-sql-server.md)   
 [&#40;Transact-sql&#41;授與伺服器主體許可權](/sql/t-sql/statements/grant-server-principal-permissions-transact-sql)   
 [REVOKE 伺服器主體許可權 &#40;Transact-sql&#41;](/sql/t-sql/statements/revoke-server-principal-permissions-transact-sql)   
 [&#40;Transact-sql&#41;拒絕伺服器主體許可權](/sql/t-sql/statements/deny-server-principal-permissions-transact-sql)   
 [建立伺服器角色](../authentication-access/create-a-server-role.md)  
  
  
