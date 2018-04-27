---
title: Integration Services 角色 (SSIS 服務) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.dtsserver.packageroles.f1
helpviewer_keywords:
- security [Integration Services], roles
- db_ssisoperator role
- db_ssisadmin role
- fixed database roles [Integration Services]
- packages [Integration Services], security
- roles [Integration Services]
- db_ssisltduser role
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 79b84fc3f52cb12a77d1a2e51acbc074f810c6d0
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="integration-services-roles-ssis-service"></a>Integration Services 角色 (SSIS 服務)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供特定固定資料庫層級角色來協助保護對於儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的封裝的存取。 可用的角色根據您將封裝儲存在 SSIS 目錄資料庫 (SSISDB) 或 msdb 資料庫而有所不同。  
  
## <a name="roles-in-the-ssis-catalog-database-ssisdb"></a>SSIS 目錄資料庫 (SSISDB) 中的角色  
 SSIS 目錄資料庫 (SSISDB) 提供下列固定資料庫層級角色，來協助保護對於封裝和封裝相關資訊的存取。  
  
-   **ssis_admin**： 此角色提供 SSIS 目錄資料庫的完整系統管理存取權。  
  
-   **ssis_logreader** ：此角色提供存取所有 SSISDB 作業記錄相關檢視的權限。  
  
     檢視清單包括：[catalog].[projects]、[catalog].[packages]、[catalog].[operations]、[catalog].[extended_operation_info]、[catalog].[operation_messages]、[catalog].[event_messages]、[catalog].[execution_data_statistics]、[catalog].[execution_component_phases]、[catalog].[execution_data_taps]、[catalog].[event_message_context]、[catalog].[executions]、[catalog].[executables]、[catalog].[executable_statistics]、[catalog].[validations]、[catalog].[execution_parameter_values] 和 [catalog].[execution_property_override_values]。  
  
## <a name="roles-in-the-msdb-database"></a>msdb 資料庫中的角色  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含以下三個固定資料庫層級角色： **db_ssisadmin**、 **db_ssisltduser**和 **db_ssisoperator**，可用於控制對儲存至 **msdb** 資料庫之封裝的存取。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]將角色指派給封裝。 角色指派會儲存到 **msdb** 資料庫。  
  
### <a name="read-and-write-actions"></a>讀取和寫入動作  
 下表描述 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中 Windows 及固定資料庫層級角色的讀取和寫入動作。  
  
|角色|讀取動作|寫入動作|  
|----------|-----------------|------------------|  
|**db_ssisadmin**<br /><br /> 中的多個<br /><br /> **sysadmin**|列舉自己的封裝。<br /><br /> 列舉所有封裝。<br /><br /> 檢視自己的封裝。<br /><br /> 檢視所有封裝。<br /><br /> 執行自己的封裝。<br /><br /> 執行所有封裝。<br /><br /> 匯出自己的封裝。<br /><br /> 匯出所有封裝。<br /><br /> 執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 中的所有封裝。|匯入封裝。<br /><br /> 刪除自己的封裝。<br /><br /> 刪除所有封裝。<br /><br /> 變更自己的封裝角色。<br /><br /> 變更所有封裝角色。<br /><br /> <br /><br /> **\*\* 警告 \*\*** db_ssisadmin 角色和 dc_admin 角色的成員可以將其權限提高為系統管理員。 之所以能夠進行此權限提高，是因為這些角色可以修改 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，而且 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可藉由使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的 sysadmin 安全性內容由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行。 若要在執行維護計畫、資料收集組和其他 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝時預防此權限提高，請將執行封裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業設為使用有限權限的 Proxy 帳戶，或是只將系統管理員 (sysadmin) 成員加入 db_ssisadmin 和 dc_admin 角色。|  
|**db_ssisltduser**|列舉自己的封裝。<br /><br /> 列舉所有封裝。<br /><br /> 檢視自己的封裝。<br /><br /> 執行自己的封裝。<br /><br /> 匯出自己的封裝。|匯入封裝。<br /><br /> 刪除自己的封裝。<br /><br /> 變更自己的封裝角色。|  
|**db_ssisoperator**|列舉所有封裝。<br /><br /> 檢視所有封裝。<br /><br /> 執行所有封裝。<br /><br /> 匯出所有封裝。<br /><br /> 執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 中的所有封裝。|無|  
|**Windows administrators**|檢視所有正在執行之封裝的執行詳細資料。|停止所有目前正在執行的封裝。|  
  
### <a name="sysssispackages-table"></a>Sysssispackages 資料表  
 **msdb** 中的 **sysssispackages** 資料表包含儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的封裝。 如需詳細資訊，請參閱 [sysssispackages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackages-transact-sql.md)。  
  
 **sysssispackages** 資料表包括的資料行包含指派給封裝之角色的相關資訊。  
  
-   **readerrole** 資料行會指定擁有封裝之讀取權限的角色。  
  
-   **writerrole** 資料行會指定擁有封裝之寫入權限的角色。  
  
-   **ownersid** 資料行包含建立封裝之使用者的唯一安全性識別碼。 此資料行會定義封裝的擁有者。  
  
### <a name="permissions"></a>Permissions  
 依預設， **db_ssisadmin** 和 **db_ssisoperator** 固定資料庫層級角色的權限以及建立封裝之使用者的唯一安全性識別碼會套用至封裝的讀取者角色，而 **db_ssisadmin** 角色的權限以及建立封裝之使用者的唯一安全性識別碼則會套用至封裝的寫入者角色。 使用者必須是 **db_ssisadmin**、 **db_ssisltduser**或 **db_ssisoperator** 角色的成員，才能擁有封裝的讀取權限。 使用者必須是 **db_ssisadmin** 角色的成員，才能擁有寫入權限。  
  
### <a name="access-to-packages"></a>對封裝的存取權  
 固定資料庫層級角色要與使用者定義角色搭配使用。 使用者定義角色是您在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中建立後用以指派權限給封裝的角色。 若要存取封裝，使用者必須是使用者定義角色和適當 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 固定資料庫層級角色的成員。 例如，如果使用者是指派給封裝之 **AuditUsers** 使用者定義角色的成員，他們還必須是 **db_ssisadmin**、 **db_ssisltduser**或 **db_ssisoperator** 角色的成員，才能擁有封裝的讀取權限。  
  
 如果您沒有指派使用者定義角色給封裝，則對封裝的存取是由固定的資料庫層級角色決定的。  
  
 如果想要使用使用者定義角色，則必須先將這些角色加入 **msdb** 資料庫，然後才能將它們指派給封裝。 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中建立新資料庫角色。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料庫層級角色會授與 msdb 資料庫中 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 系統資料表的權限。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER 服務) 必須啟動，才能連接到 Database Engine 並存取 **msdb** 資料庫。  
  
 若要將角色指派給封裝，您需要完成下列工作。  
  
-   **開啟物件總管並連接到 Integration Services**  
  
     必須先在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中開啟 [物件總管]，並連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，才能使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]指派角色給封裝。  
  
     必須先啟動 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務，才能連接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。  
  
-   **指派讀取器和寫入器角色給封裝**  
  
     您可將讀取器和寫入器角色指派給每個封裝。  

## <a name="assign"></a> 指派讀取器和寫入器角色給封裝
  您可將讀取器和寫入器角色指派給每個封裝。  
  
### <a name="assign-a-reader-and-writer-role-to-a-package"></a>指派讀取器和寫入器角色給封裝  
  
1.  在 [物件總管] 中，尋找 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 連接。  
  
2.  展開 [Stored Packages] 資料夾，然後展開包含想要為其指派角色之封裝的子資料夾。  
  
3.  以滑鼠右鍵按一下想要為其指派角色的封裝。  
  
4.  在 **[封裝角色]** 對話方塊中，選取 **[讀取器角色]** 清單中的讀取器角色和 **[寫入器角色]** 清單中的寫入器角色。  
  
5.  按一下 [確定] 。

## <a name="create"></a> 建立使用者定義角色
    
### <a name="to-create-a-user-defined-role"></a>建立使用者定義角色  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
2.  在 **[檢視]** 功能表上，按一下 **[物件總管]** 。  
  
3.  在 [物件總管] 工具列上，按一下 **[連接]**，再按一下 **[Database Engine]**。  
  
4.  在 [連接到伺服器] 對話方塊中，提供伺服器名稱並選取驗證模式。 您可以使用句號 (.)、(local) 或 **localhost** 表示本機伺服器。  
  
5.  按一下 **[連接]**。  
  
6.  展開 [資料庫]、[系統資料庫]、[msdb]、[安全性] 和 [角色]。  
  
7.  在 [角色] 節點中，以滑鼠右鍵按一下 [資料庫角色]，並按一下 [新增資料庫角色]。  
  
8.  在 [一般] 頁面上提供名稱，選擇性地指定擁有者和擁有的結構描述，並加入角色成員。  
  
9. 選擇性地按一下 [權限]，並設定物件權限。  
  
10. 選擇性地按一下 [擴充屬性]，並設定任何擴充屬性。  
  
11. 按一下 [確定] 。

## <a name="roles_dialog"></a> 套件角色對話方塊 UI 參考
  使用 [封裝角色] 對話方塊 (可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用)，即可指定擁有封裝之讀取權限的資料庫層級角色以及擁有封裝之寫入權限的資料庫層級角色。 資料庫層級角色僅適用於儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** 資料庫中的封裝。  
  
 對話方塊中所列出的角色是 **msdb** 系統資料庫的目前資料庫角色。 如果沒有選取角色，則會套用預設 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 角色。 依預設，讀取者角色包含 **db_ssisadmin**、 **db_ssisoperator**和建立封裝的使用者。 上述其中一個角色之成員或是建立封裝的使用者可以列舉、檢視、匯出和執行封裝。 依預設，寫入者角色包含 **db_ssisadmin** 以及建立封裝的使用者。 這個角色的成員使用者以及建立封裝的使用者，可以匯入、刪除和變更封裝。  
  
 **sysssispackages** 資料表中的 **ownersid** 資料行列出建立封裝之使用者的唯一安全性識別碼。  
  
### <a name="options"></a>選項。  
 **封裝名稱**  
 指定封裝的名稱。  
  
 **讀取器角色**  
 選取清單中的角色。  
  
 **寫入器角色**  
 選取清單中的角色  
