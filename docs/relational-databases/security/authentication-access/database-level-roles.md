---
title: 資料庫層級角色 | Microsoft 文件
ms.custom: ''
ms.date: 07/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.roleproperties.database.f1
- sql13.swb.roleproperties.object.f1
- SQL13.SWB.DBROLEPROPERTIES.GENERAL.F1
- sql13.swb.roleproperties.general.f1
helpviewer_keywords:
- db_denydatareader role
- users [SQL Server], database roles
- database-level roles [SQL Server]
- db_denydatawriter role
- roles [SQL Server], database
- principals [SQL Server], database-level
- db_backupoperator role
- credentials [SQL Server], roles
- db_accessadmin role
- schemas [SQL Server], roles
- permissions [SQL Server], roles
- database roles [SQL Server], listed
- db_datareader role
- db_ddladmin role
- db_datawriter role
- db_securityadmin role
- db_owner role
- database roles [SQL Server]
- fixed database roles [SQL Server]
- authentication [SQL Server], roles
- groups [SQL Server], roles
ms.assetid: 7f3fa5f6-6b50-43bb-9047-1544ade55e39
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6e91fcd2281082bbef88f0a8387d3ed6cef603d9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68742838"
---
# <a name="database-level-roles"></a>資料庫層級角色

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  為了輕鬆管理資料庫中的權限， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供了幾個 *「角色」* (Role)，這些角色是分組其他主體的安全性主體。 它們就像是 ***Windows 作業系統中的*** 群組 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 。 資料庫層級角色的權限範圍為整個資料庫。  

若要新增和移除資料庫角色的使用者，請使用 `ADD MEMBER` ALTER ROLE `DROP MEMBER` 陳述式的 [和](../../../t-sql/statements/alter-role-transact-sql.md) 選項。 [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] 不支援使用 `ALTER ROLE`。 請改用舊版的 [sp_addrolemember](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) 和 [sp_droprolemember](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) 程序。
  
 資料庫層級角色類型有兩種：在資料庫中預先定義的「固定資料庫角色」  以及您可以建立的「使用者定義資料庫角色」  。  
  
 固定資料庫角色義於資料庫層級，並存在每個資料庫中。 **db_owner** 資料庫角色的成員可以管理固定的資料庫角色成員資格。 在 msdb 資料庫中，也有一些特殊用途的資料庫角色。  
  
 您可以將任何資料庫帳戶和其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 角色加入資料庫層級角色中。
  
> [!TIP]  
>  請勿將使用者定義資料庫角色當作固定角色成員加入。 這樣會產生不必要的權限擴大。  

使用者定義資料庫角色的權限可以使用 GRANT、DENY 和 REVOKE 陳述式自訂。 如需詳細資訊，請參閱 [權限 (Database Engine)](../../../relational-databases/security/permissions-database-engine.md)。

如需所有權限的清單，請參閱 [Database Engine 權限](https://aka.ms/sql-permissions-poster) 海報。 (資料庫角色不能獲派伺服器層級權限。 登入和其他伺服器層級主體 (例如伺服器角色) 無法加入資料庫角色。 如需 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)]的伺服器層級安全性，請改用 [伺服器角色](../../../relational-databases/security/authentication-access/server-level-roles.md) 。 伺服器層級權限不能透過 [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] 和 [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)]的角色授與。)

## <a name="fixed-database-roles"></a>固定資料庫角色
  
 下表顯示固定資料庫角色及其功能。 這些角色存在所有資料庫中。 除了**公用**資料庫角色外，指派給固定資料庫角色的權限無法變更。   
  
|固定資料庫角色名稱|描述|  
|-------------------------------|-----------------|  
|**db_owner**|**db_owner** 固定資料庫角色的成員可以在資料庫上執行所有的組態和維護活動，也可以在 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)]中卸除資料庫。 (在 [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] 和 [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)]中，某些維護活動需要伺服器層級的權限，而且無法由 **db_owners**執行。)|  
|**db_securityadmin**|**db_securityadmin** 固定資料庫角色的成員可以修改角色成員資格 (僅自訂角色) 以及管理權限。 此角色的成員可能會提升其權限，因此其動作應受到監視。|  
|**db_accessadmin**|**db_accessadmin** 固定資料庫角色的成員可以針對 Windows 登入、Windows 群組及 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入加入或移除資料庫的存取權。|  
|**db_backupoperator**|**db_backupoperator** 固定資料庫角色的成員可以備份資料庫。|  
|**db_ddladmin**|**db_ddladmin** 固定資料庫角色的成員可在資料庫中執行任何「資料定義語言」(DDL) 的命令。|  
|**db_datawriter**|**db_datawriter** 固定資料庫角色的成員可以加入、刪除或變更所有使用者資料表中的資料。|  
|**db_datareader**|**db_datareader** 固定資料庫角色的成員可以從所有使用者資料表讀取所有資料。|  
|**db_denydatawriter**|**db_denydatawriter** 固定資料庫角色的成員不能加入、修改或刪除資料庫中使用者資料表的任何資料。|  
|**db_denydatareader**|**db_denydatareader** 固定資料庫角色的成員不能讀取資料庫中使用者資料表的任何資料。|  

指派給固定資料庫角色的權限無法變更。 下圖顯示指派給固定資料庫角色的權限：

![fixed_database_role_permissions](../../../relational-databases/security/authentication-access/media/permissions-of-database-roles.png)

## <a name="special-roles-for-includesssds_mdincludessssds-mdmd-and-includesssdw_mdincludessssdw-mdmd"></a>針對 [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] 及 [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)]的特殊角色

這些資料庫角色只存在於虛擬 master 資料庫中。 其權限僅限於能在 master 中執行的動作。 只有 master 資料庫使用者可以加入這些角色中。 這些角色中不能加入登入，但可以根據登入建立使用者，然後將這些使用者加入角色中。 包含的 master 資料庫使用者，也可加入這些角色中。 但是，加入到 **dbmanager** 角色的包含的 master 資料庫使用者不能用來建立新的資料庫。

|角色名稱|描述|  
|--------------------|-----------------|
|**dbmanager** | 可以建立和刪除資料庫。 建立資料庫的 dbmanager 角色成員會變成該資料庫的擁有者，讓使用者能夠像 dbo 使用者一樣連線至該資料庫。 dbo 使用者具有資料庫的所有資料庫權限。 dbmanager 角色成員不一定有非其所有之資料庫的存取權限。|
|**loginmanager** | 可以建立及刪除虛擬 master 資料庫的登入。|

> [!NOTE]
> 伺服器層級主體和 Azure Active Directory 系統管理員 (如已設定) 具有 [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] 和 [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)] 的所有權限，而不必是任何角色成員。 如需詳細資訊，請參閱 [SQL Database 驗證和授權：授與存取](https://azure.microsoft.com/documentation/articles/sql-database-manage-logins/)。 
  
## <a name="msdb-roles"></a>msdb 角色  
 msdb 資料庫含有下表所示的特殊用途角色。  
  
|msdb 角色名稱|描述|  
|--------------------|-----------------|  
|**db_ssisadmin**<br /><br /> **db_ssisoperator**<br /><br /> **db_ssisltduser**|這些資料庫角色的成員可以管理和使用 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]。 從舊版升級的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體可能會包含使用 Data Transformation Services (DTS) 而非 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 所命名的舊版角色。 如需詳細資訊，請參閱 [Integration Services 角色 &#40;SSIS 服務&#41;](../../../integration-services/security/integration-services-roles-ssis-service.md)。|  
|**dc_admin**<br /><br /> **dc_operator**<br /><br /> **dc_proxy**|這些資料庫角色的成員可以管理和使用資料收集器。 如需相關資訊，請參閱 [Data Collection](../../../relational-databases/data-collection/data-collection.md)。|  
|**PolicyAdministratorRole**|**db_ PolicyAdministratorRole** 資料庫角色的成員可以在以原則為基礎的管理原則和條件上執行所有組態和維護活動。 如需詳細資訊，請參閱 [使用原則式管理來管理伺服器](../../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)。|  
|**ServerGroupAdministratorRole**<br /><br /> **ServerGroupReaderRole**|這些資料庫角色的成員可以管理和使用已註冊的伺服器群組。|  
|**dbm_monitor**|在「資料庫鏡像監視器」中註冊第一個資料庫時，於 **msdb** 資料庫中建立的。 **dbm_monitor** 角色沒有任何成員，必須由系統管理員指派使用者給該角色。|  
  
> [!IMPORTANT]  
>  **db_ssisadmin** 角色和 **dc_admin** 角色的成員可以將其權限提高為系統管理員。 之所以能夠進行此權限提高，是因為這些角色可以修改 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 封裝，而且 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 可藉由使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 的 sysadmin 安全性內容由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行。 若要在執行維護計畫、資料收集組和其他 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 封裝時預防此權限提高，請將執行封裝的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業設為使用有限權限的 Proxy 帳戶，或是只將 **系統管理員** 成員加入 **db_ssisadmin** 和 **dc_admin** 角色。  

## <a name="working-with-r-services"></a>使用 R 服務  

**適用於：** SQL Server (從 [!INCLUDE[ssSQLv14_md](../../../includes/sssqlv14-md.md)]   

安裝 R 服務時，可使用額外的資料庫角色來管理封裝。 如需詳細資訊，請參閱 [SQL Server 的 R 封裝管理](../../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。

|角色名稱 |描述|  
|-------------|-----------------|
|**rpkgs-users** |可讓使用者使用 rpkgs-shared 角色成員所安裝的任何共用封裝。|
|**rpkgs-private** |提供與 rpkgs-users 角色相同的權限來存取共用封裝。 此角色成員也可以安裝、移除和使用具有私用範圍的封裝。|
|**rpkgs-shared** |提供與 rpkgs-private 角色相同的權限。 屬於此角色成員的使用者也可以安裝或移除共用封裝。|
  
## <a name="working-with-database-level-roles"></a>使用資料庫層級角色  
 下表說明用於使用資料庫層級角色的命令、檢視及函數。  
  
|功能|類型|描述|  
|-------------|----------|-----------------|  
|[sp_helpdbfixedrole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md)|中繼資料|傳回固定資料庫角色的清單。|  
|[sp_dbfixedrolepermission &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql.md)|中繼資料|顯示固定資料庫角色的權限。|  
|[sp_helprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)|中繼資料|傳回目前資料庫中角色的相關資訊。|  
|[sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)|中繼資料|傳回目前資料庫中角色成員的相關資訊。|  
|[sys.database_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)|中繼資料|針對每個資料庫角色的每個成員，各傳回一個資料列。|  
|[IS_MEMBER &#40;Transact-SQL&#41;](../../../t-sql/functions/is-member-transact-sql.md)|中繼資料|指出目前使用者是指定之 Microsoft Windows 群組或 Microsoft SQL Server 資料庫角色的成員。|  
|[CREATE ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-role-transact-sql.md)|Command|在目前資料庫中建立新的資料庫角色。|  
|[ALTER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md)|Command|變更資料庫角色的名稱或成員資格。|  
|[DROP ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-role-transact-sql.md)|Command|從資料庫中移除角色。|  
|[sp_addrole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)|Command|在目前資料庫中建立新的資料庫角色。|  
|[sp_droprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)|Command|從目前資料庫移除資料庫角色。|  
|[sp_addrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)|Command|在目前資料庫的資料庫角色中，加入資料庫使用者、資料庫角色、Windows 登入或 Windows 群組。 除 [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] 外，所有平台都應該改用 `ALTER ROLE` 。|  
|[sp_droprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)|Command|從目前資料庫中的 SQL Server 角色移除安全性帳戶。 除 [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] 外，所有平台都應該改用 `ALTER ROLE` 。|
|[GRANT](../../../t-sql/statements/grant-transact-sql.md)| 權限 | 新增角色權限。
|[DENY](../../../t-sql/statements/deny-transact-sql.md)| 權限 | 拒絕角色權限。
|[REVOKE](../../../t-sql/statements/revoke-transact-sql.md)| 權限 | 移除先前授與或拒絕的權限。
  
  
## <a name="public-database-role"></a>public 資料庫角色  
 每個資料庫使用者都屬於 **public** 資料庫角色。 當使用者未授與或拒絕安全物件的特定權限時，該使用者會繼承授與給該物件之 **public** 的權限。 無法移除 **公用** 角色中的資料庫使用者。 
  
## <a name="related-content"></a>相關內容  
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
 [安全性函數 &#40;Transact-SQL&#41;](../../../t-sql/functions/security-functions-transact-sql.md)  
  
 [保護 SQL Server 的安全](../../../relational-databases/security/securing-sql-server.md)  
  
 [sp_helprotect &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)  
  
  
