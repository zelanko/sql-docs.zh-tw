---
title: 主體 (Database Engine) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.roleproperties.selectroll.f1
- sql12.swb.databaseuser.permissions.user.f1--May use common.permissions
helpviewer_keywords:
- certificates [SQL Server], principals
- roles [SQL Server], principals
- permissions [SQL Server], principals
- '##MS_SQLAuthenticatorCertificate##'
- principals [SQL Server]
- '##MS_SQLResourceSigningCertificate##'
- groups [SQL Server], principals
- '##MS_AgentSigningCertificate##'
- authentication [SQL Server], principals
- schemas [SQL Server], principals
- principals [SQL Server], about principals
- security [SQL Server], principals
- users [SQL Server], principals
- '##MS_SQLReplicationSigningCertificate##'
ms.assetid: 3f7adbf7-6e40-4396-a8ca-71cbb843b5c2
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 6d91a6c21bc162ff1f6100e88101f34a0a275cd8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084548"
---
# <a name="principals-database-engine"></a>主體 (Database Engine)
  「主體」是可要求 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源的實體。 主體就像其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 授權模型的元件一樣，可以階層方式安排。 主體的影響範圍視主體的定義範圍 (Windows、伺服器、資料庫)，以及主體是否可分割或者是一個集合而定。 「Windows 登入」是不可分割主體的一個範例，而「Windows 群組」則是主體為集合的範例。 每個主體都有一個安全性識別碼 (SID)。  
  
 **Windows 層級主體**  
  
-   Windows 網域登入  
  
-   Windows 本機登入  
  
 **SQL Server**-**層級** **主體**  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入  
  
-   伺服器角色  
  
 **資料庫層級主體**  
  
-   資料庫使用者  
  
-   資料庫角色  
  
-   應用程式角色  
  
## <a name="the-sql-server-sa-login"></a>SQL Server sa 登入  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sa 登入為伺服器層級的主體。 根據預設，安裝執行個體時會建立它。 從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]開始，sa 的預設資料庫就是 master。 這是和舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]不同的一項行為變更。  
  
## <a name="public-database-role"></a>public 資料庫角色  
 每個資料庫使用者都屬於 public 資料庫角色。 當使用者未被授與或拒絕安全性實體的特定權限時，該使用者會繼承授與給該安全性實體之 public 的權限。  
  
## <a name="informationschema-and-sys"></a>INFORMATION_SCHEMA 與 sys  
 每個資料庫都包含兩個在目錄檢視中顯示為使用者的實體：INFORMATION_SCHEMA 和 sys。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]需要這些實體。 它們並非主體，也不能被修改或卸除。  
  
## <a name="certificate-based-sql-server-logins"></a>以憑證為基礎的 SQL Server 登入  
 以兩個 ## 符號括住的伺服器主體名稱僅供內部系統使用。 在安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，將會從憑證建立下列主體，而且不應該刪除它們。  
  
-   \##MS_SQLResourceSigningCertificate##  
  
-   \##MS_SQLReplicationSigningCertificate##  
  
-   \##MS_SQLAuthenticatorCertificate##  
  
-   \##MS_AgentSigningCertificate##  
  
-   \##MS_PolicyEventProcessingLogin##  
  
-   \##MS_PolicySigningCertificate##  
  
-   \##MS_PolicyTsqlExecutionLogin##  
  
## <a name="the-guest-user"></a>guest 使用者  
 每個資料庫都包括 **guest**。 具有資料庫存取權但在資料庫中沒有使用者帳戶的使用者，將繼承授與 **guest** 使用者的權限。 **客體**無法卸除使用者，但可透過撤銷其停用的`CONNECT`權限。 `CONNECT`權限可以執行撤銷`REVOKE CONNECT FROM GUEST`master 或 tempdb 以外的任何資料庫中。  
  
## <a name="client-and-database-server"></a>用戶端和資料庫伺服器  
 根據定義，用戶端和資料庫伺服器都是安全性主體，而且可以維護其安全。 建立安全的網路連接之前，這些實體可以進行相互驗證。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援[Kerberos](http://go.microsoft.com/fwlink/?LinkId=100758)驗證通訊協定，可定義用戶端與網路驗證服務互動的方式。  
  
## <a name="related-tasks"></a>相關工作  
 《 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》的本節中包括下列主題：  
  
-   [管理登入、使用者與結構描述的使用說明主題](managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [伺服器層級角色](server-level-roles.md)  
  
-   [資料庫層級角色](database-level-roles.md)  
  
-   [應用程式角色](application-roles.md)  
  
## <a name="see-also"></a>另請參閱  
 [保護 SQL Server 的安全](../securing-sql-server.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-principals-transact-sql)   
 [sys.server_principals &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql)   
 [sys.sql_logins &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql)   
 [sys.database_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)   
 [伺服器層級角色](server-level-roles.md)   
 [資料庫層級角色](database-level-roles.md)  
  
  
