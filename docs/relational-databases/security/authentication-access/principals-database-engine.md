---
title: 主體 (Database Engine) | Microsoft Docs
description: 深入了解資料庫引擎中的主體，其是可以要求 SQL Server 資源的實體。 有 SQL Server 層級和資料庫層級的主體。
ms.custom: ''
ms.date: 01/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.roleproperties.selectroll.f1
- sql13.swb.databaseuser.permissions.user.f1--May use common.permissions
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ef45a3ade9123288b8d89a44dbfb18b8e626ed5d
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678945"
---
# <a name="principals-database-engine"></a>主體 (Database Engine)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  「主體」是可要求 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源的實體。 主體就像其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 授權模型的元件一樣，可以階層方式安排。 主體的影響範圍，取決於主體定義的範圍：Windows、伺服器、資料庫；以及主體是否為不可分割或集合。 「Windows 登入」是不可分割主體的一個範例，而「Windows 群組」則是主體為集合的範例。 每個主體都有一個安全性識別碼 (SID)。 此主題適用於所有版本的 SQL Server，但 SQL Database 或 Azure Synapse Analytics 中伺服器層級主體有一些限制。 
  
## <a name="sql-server-level-principals"></a>SQL Server 層級主體  
  
- [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證登入   
- Windows 使用者的 Windows 驗證登入  
- Windows 群組的 Windows 驗證登入   
- AD 使用者的 Azure Active Directory 驗證登入
- AD 群組的 Azure Active Directory 驗證登入
- 伺服器角色  
  
## <a name="database-level-principals"></a>資料庫層級主體
  
- 資料庫使用者 (有 12 種類型的使用者。 如需詳細資訊，請參閱 [CREATE USER](../../../t-sql/statements/create-user-transact-sql.md))。
- 資料庫角色
- 應用程式角色
  
## <a name="sa-login"></a>sa 登入  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `sa` 登入為伺服器層級的主體。 根據預設，安裝執行個體時會建立它。 從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]開始，sa 的預設資料庫就是 master。 這是和舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]不同的一項行為變更。 `sa` 登入是 `sysadmin` 固定伺服器層級角色成員。 `sa` 登入具有伺服器的所有權限，因此不受限制。 無法卸除 `sa` 登入，但可透過停用，讓所有人都無法使用它。

## <a name="dbo-user-and-dbo-schema"></a>dbo 使用者和 dbo 結構描述

`dbo` 使用者是每個資料庫中的特殊使用者主體。 所有 SQL Server 系統管理員、`sysadmin` 固定伺服器角色成員、`sa` 登入以及資料庫擁有者，都是以 `dbo` 使用者的身分進入資料庫。 `dbo` 使用者具有資料庫中的所有權限，並且不受限制也無法進行卸除。 `dbo` 代表資料庫擁有者，但 `dbo` 使用者帳戶與 `db_owner` 固定資料庫角色不同，而且 `db_owner` 固定資料庫角色與記錄為資料庫擁有者的使用者帳戶不同。     
`dbo` 使用者擁有 `dbo` 結構描述。 除非指定其他結構描述，否則 `dbo` 結構描述是所有使用者的預設結構描述。  無法卸除 `dbo` 結構描述。
  
## <a name="public-server-role-and-database-role"></a>public 伺服器角色和資料庫角色  
每個登入都屬於 `public` 固定伺服器角色，而每個資料庫使用者都屬於 `public` 資料庫角色。 當登入或使用者未被授與或拒絕安全性實體的特定權限時，該登入或使用者會繼承授與該安全性實體之 public 的權限。 無法卸除 `public` 固定伺服器角色和 `public` 固定資料庫角色。 不過，您可以撤銷 `public` 角色的權限。 預設會將許多權限指派給 `public` 角色。 在資料庫中執行例行作業時，需要其中的大部分權限，而每個人應該都有可以執行的動作類型。 撤銷 public 登入或使用者的權限時請小心，因為它會影響所有登入/使用者。 一般而言，您不應該將拒絕權限授與 public，因為拒絕陳述會覆寫任何可對個人所進行的授與陳述。 
  
## <a name="information_schema-and-sys-users-and-schemas"></a>INFORMATION_SCHEMA 與 sys 使用者和結構描述 
 每個資料庫都包含兩個在目錄檢視中顯示為使用者的實體：`INFORMATION_SCHEMA` 和 `sys`。 需要有這些實體，以供 Database Engine 內部使用。 它們無法進行修改或卸除。  
  
## <a name="certificate-based-sql-server-logins"></a>以憑證為基礎的 SQL Server 登入  
 以兩個 ## 符號括住的伺服器主體名稱僅供內部系統使用。 在安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，將會從憑證建立下列主體，而且不應該刪除它們。  
  
-   \##MS_SQLResourceSigningCertificate##    
-   \##MS_SQLReplicationSigningCertificate##    
-   \##MS_SQLAuthenticatorCertificate##    
-   \##MS_AgentSigningCertificate##   
-   \##MS_PolicyEventProcessingLogin##   
-   \##MS_PolicySigningCertificate##   
-   \##MS_PolicyTsqlExecutionLogin##   
 
 這些主體帳戶沒有系統管理員可以變更的密碼，因為它們是以發行到 Microsoft 的憑證為基礎。
  
## <a name="the-guest-user"></a>guest 使用者  
 每個資料庫都包括 `guest`不同的一項行為變更。 具有資料庫存取權但在資料庫中沒有使用者帳戶的使用者，將繼承授與 `guest` 使用者的權限。 無法卸除 `guest` 使用者，但可透過撤銷其 CONNECT 權限予以停用。 在任何資料庫 (不含 `master` 或 `tempdb`) 內執行 `REVOKE CONNECT FROM GUEST;`，即可撤銷 CONNECT 權限。  
  
  
## <a name="related-tasks"></a>相關工作  
 如需設計權限系統的資訊，請參閱 [資料庫引擎權限使用者入門](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。  
  
 《 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》的本節中包括下列主題：  
  
-   [管理登入、使用者與結構描述的使用說明主題](./create-a-login.md)  
  
-   [伺服器層級角色](../../../relational-databases/security/authentication-access/server-level-roles.md)  
  
-   [資料庫層級角色](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
-   [應用程式角色](../../../relational-databases/security/authentication-access/application-roles.md)  
  
## <a name="see-also"></a>另請參閱  
 [保護 SQL Server 的安全](../../../relational-databases/security/securing-sql-server.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.sql_logins &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [伺服器層級角色](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [資料庫層級角色](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
