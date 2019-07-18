---
title: 資料庫層級角色 | Microsoft 文件
ms.custom: ''
ms.date: 09/22/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.roleproperties.database.f1
- sql12.swb.roleproperties.general.f1
- sql12.swb.roleproperties.object.f1
- SQL12.SWB.DBROLEPROPERTIES.GENERAL.F1
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
manager: craigg
ms.openlocfilehash: 3df05bddf37970ce0ff0d796bc2b5d93d309b4dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011726"
---
# <a name="database-level-roles"></a>資料庫層級角色
  為了輕鬆管理資料庫中的權限， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供了幾個 *「角色」* (Role)，這些角色是分組其他主體的安全性主體。 它們就像是 ***Windows 作業系統中的*** 群組 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 。 資料庫層級角色的權限範圍為整個資料庫。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中有兩種資料庫層級角色類型：在資料庫中預先定義的 *「固定資料庫角色」* (Fixed Database Role) 以及您可以建立的 *「彈性資料庫角色」* (Flexible Database Role)。  
  
 固定資料庫角色義於資料庫層級，並存在每個資料庫中。 **db_owner** 資料庫角色的成員可以管理固定的資料庫角色成員資格。 在 msdb 資料庫中，也有一些特殊用途的固定資料庫角色。  
  
 您可以將任何資料庫帳戶和其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 角色加入資料庫層級角色中。 固定資料庫角色的每個成員可以對相同的角色加入其他登入。  
  
> [!IMPORTANT]  
>  請勿將彈性資料庫角色當做固定角色的成員來加入。 這樣會產生不必要的權限擴大。  
  
 下表顯示固定資料庫層級角色和其功能。 這些角色存在所有資料庫中。  
  
|資料庫層級角色名稱|描述|  
|-------------------------------|-----------------|  
|**db_owner**|**db_owner** 固定資料庫角色的成員可以在資料庫上執行所有的組態和維護活動，也可以卸除資料庫。|  
|**db_securityadmin**|**db_securityadmin** 固定資料庫角色的成員可以修改角色成員資格及管理權限。 將主體加入這個角色可能會產生不必要的權限擴大。|  
|**db_accessadmin**|**db_accessadmin** 固定資料庫角色的成員可以針對 Windows 登入、Windows 群組及 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入加入或移除資料庫的存取權。|  
|**db_backupoperator**|**db_backupoperator** 固定資料庫角色的成員可以備份資料庫。|  
|**db_ddladmin**|**db_ddladmin** 固定資料庫角色的成員可在資料庫中執行任何「資料定義語言」(DDL) 的命令。|  
|**db_datawriter**|**db_datawriter** 固定資料庫角色的成員可以加入、刪除或變更所有使用者資料表中的資料。|  
|**db_datareader**|**db_datareader** 固定資料庫角色的成員可以從所有使用者資料表讀取所有資料。|  
|**db_denydatawriter**|**db_denydatawriter** 固定資料庫角色的成員不能加入、修改或刪除資料庫中使用者資料表的任何資料。|  
|**db_denydatareader**|**db_denydatareader** 固定資料庫角色的成員不能讀取資料庫中使用者資料表的任何資料。|  
  
## <a name="msdb-roles"></a>msdb 角色  
 msdb 資料庫含有下表所示的特殊用途角色。  
  
|msdb 角色名稱|描述|  
|--------------------|-----------------|  
|`db_ssisadmin`<br /><br /> **db_ssisoperator**<br /><br /> **db_ssisltduser**|這些資料庫角色的成員可以管理和使用 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]。 從舊版升級的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體可能會包含使用 Data Transformation Services (DTS) 而非 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 所命名的舊版角色。 如需詳細資訊，請參閱 [Integration Services 角色 &#40;SSIS 服務&#41;](../../../integration-services/security/integration-services-roles-ssis-service.md)。|  
|`dc_admin`<br /><br /> **dc_operator**<br /><br /> **dc_proxy**|這些資料庫角色的成員可以管理和使用資料收集器。 如需相關資訊，請參閱 [Data Collection](../../data-collection/data-collection.md)。|  
|**PolicyAdministratorRole**|**db_ PolicyAdministratorRole** 資料庫角色的成員可以在以原則為基礎的管理原則和條件上執行所有組態和維護活動。 如需詳細資訊，請參閱 [使用原則式管理來管理伺服器](../../policy-based-management/administer-servers-by-using-policy-based-management.md)。|  
|**ServerGroupAdministratorRole**<br /><br /> **ServerGroupReaderRole**|這些資料庫角色的成員可以管理和使用已註冊的伺服器群組。|  
|**dbm_monitor**|在中建立`msdb`時資料庫鏡像監視器 」 中註冊的第一個資料庫的資料庫。 **dbm_monitor** 角色沒有任何成員，必須由系統管理員指派使用者給該角色。|  
  
> [!IMPORTANT]  
>  db_ssisadmin 角色和 dc_admin 角色的成員可以將其權限提高為系統管理員 (sysadmin)。 之所以能夠進行此權限提高，是因為這些角色可以修改 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 封裝，而且 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 可藉由使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 的 sysadmin 安全性內容由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行。 若要在執行維護計畫、資料收集組和其他 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 封裝時預防此權限提高，請將執行封裝的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業設為使用有限權限的 Proxy 帳戶，或是只將系統管理員 (sysadmin) 成員加入 db_ssisadmin 和 dc_admin 角色。  
  
## <a name="working-with-database-level-roles"></a>使用資料庫層級角色  
 下表說明用於使用資料庫層級角色的命令、檢視及函數。  
  
|功能|類型|描述|  
|-------------|----------|-----------------|  
|[sp_helpdbfixedrole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql)|中繼資料|傳回固定資料庫角色的清單。|  
|[sp_dbfixedrolepermission &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql)|中繼資料|顯示固定資料庫角色的權限。|  
|[sp_helprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprole-transact-sql)|中繼資料|傳回目前資料庫中角色的相關資訊。|  
|[sp_helprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql)|中繼資料|傳回目前資料庫中角色成員的相關資訊。|  
|[sys.database_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)|中繼資料|針對每個資料庫角色的每個成員，各傳回一個資料列。|  
|[IS_MEMBER &#40;Transact-SQL&#41;](/sql/t-sql/functions/is-member-transact-sql)|中繼資料|指出目前使用者是指定之 Microsoft Windows 群組或 Microsoft SQL Server 資料庫角色的成員。|  
|[CREATE ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-role-transact-sql)|命令|在目前資料庫中建立新的資料庫角色。|  
|[ALTER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-role-transact-sql)|命令|變更資料庫角色的名稱。|  
|[DROP ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-role-transact-sql)|命令|從資料庫中移除角色。|  
|[sp_addrole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrole-transact-sql)|命令|在目前資料庫中建立新的資料庫角色。|  
|[sp_droprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprole-transact-sql)|命令|從目前資料庫移除資料庫角色。|  
|[sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)|命令|在目前資料庫的資料庫角色中，加入資料庫使用者、資料庫角色、Windows 登入或 Windows 群組。|  
|[sp_droprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)|命令|從目前資料庫中的 SQL Server 角色移除安全性帳戶。|  
  
## <a name="public-database-role"></a>public 資料庫角色  
 每個資料庫使用者都屬於 **public** 資料庫角色。 當使用者未授與或拒絕安全物件的特定權限時，該使用者會繼承授與給該物件之 **public** 的權限。  
  
## <a name="related-content"></a>相關內容  
 [安全性目錄檢視 &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)  
  
 [安全性預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/security-stored-procedures-transact-sql)  
  
 [安全性函數 &#40;Transact-SQL&#41;](/sql/t-sql/functions/security-functions-transact-sql)  
  
 [保護 SQL Server 的安全](../securing-sql-server.md)  
  
 [sp_helprotect &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprotect-transact-sql)  
  
  
