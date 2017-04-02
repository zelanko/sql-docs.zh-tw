---
title: "主體 (Database Engine) | Microsoft Docs"
ms.custom: ""
ms.date: "01/09/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.roleproperties.selectroll.f1"
  - "sql13.swb.databaseuser.permissions.user.f1--May use common.permissions"
helpviewer_keywords: 
  - "憑證 [SQL Server], 主體"
  - "角色 [SQL Server], 主體"
  - "權限 [SQL Server], 主體"
  - "##MS_SQLAuthenticatorCertificate##"
  - "主體 [SQL Server]"
  - "##MS_SQLResourceSigningCertificate##"
  - "群組 [SQL Server], 主體"
  - "##MS_AgentSigningCertificate##"
  - "驗證 [SQL Server], 主體"
  - "結構描述 [SQL Server], 主體"
  - "主體 [SQL Server], 關於主體"
  - "安全性 [SQL Server], 主體"
  - "使用者 [SQL Server], 主體"
  - "##MS_SQLReplicationSigningCertificate##"
ms.assetid: 3f7adbf7-6e40-4396-a8ca-71cbb843b5c2
caps.latest.revision: 57
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 55
---
# 主體 (Database Engine)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

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
  
## SQL Server sa 登入  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sa 登入為伺服器層級的主體。 根據預設，安裝執行個體時會建立它。 從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 開始，sa 的預設資料庫就是 master。 這是和舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不同的一項行為變更。  
  
## public 資料庫角色  
 每個資料庫使用者都屬於 public 資料庫角色。 當使用者未被授與或拒絕安全性實體的特定權限時，該使用者會繼承授與給該安全性實體之 public 的權限。  
  
## INFORMATION_SCHEMA 與 sys  
 每個資料庫都包含兩個在目錄檢視中顯示為使用者的實體：INFORMATION_SCHEMA 和 sys。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 需要這些實體。 它們並非主體，也不能被修改或卸除。  
  
## 以憑證為基礎的 SQL Server 登入  
 以兩個 ## 符號括住的伺服器主體名稱僅供內部系統使用。 在安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，將會從憑證建立下列主體，而且不應該刪除它們。  
  
-   \##MS_SQLResourceSigningCertificate##  
  
-   \##MS_SQLReplicationSigningCertificate##  
  
-   \##MS_SQLAuthenticatorCertificate##  
  
-   \##MS_AgentSigningCertificate##  
  
-   \##MS_PolicyEventProcessingLogin##  
  
-   \##MS_PolicySigningCertificate##  
  
-   \##MS_PolicyTsqlExecutionLogin##  
  
## guest 使用者  
 每個資料庫都包括 **guest**。 具有資料庫存取權但在資料庫中沒有使用者帳戶的使用者，將繼承授與 **guest** 使用者的權限。 無法卸除 **guest** 使用者，但可透過撤銷其 **CONNECT** 權限予以停用。 在任何資料庫 (不含 master 或 tempdb) 內執行 `REVOKE CONNECT FROM GUEST`，即可撤銷 **CONNECT** 權限。  
  
## 用戶端和資料庫伺服器  
 根據定義，用戶端和資料庫伺服器都是安全性主體，而且可以維護其安全。 建立安全的網路連接之前，這些實體可以進行相互驗證。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援 [Kerberos](http://go.microsoft.com/fwlink/?LinkId=100758) 驗證通訊協定，該通訊協定可定義用戶端與網路驗證服務的互動方式。  
  
## 相關工作  
 如需設計權限系統的資訊，請參閱[資料庫引擎權限使用者入門](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。  
  
 《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》的本節中包括下列主題：  
  
-   [管理登入、使用者與結構描述的使用說明主題](../../../relational-databases/security/authentication-access/managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [伺服器層級角色](../../../relational-databases/security/authentication-access/server-level-roles.md)  
  
-   [資料庫層級角色](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
-   [應用程式角色](../../../relational-databases/security/authentication-access/application-roles.md)  
  
## 另請參閱  
 [保護 SQL Server 的安全](../../../relational-databases/security/securing-sql-server.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.sql_logins &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [伺服器層級角色](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [資料庫層級角色](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  