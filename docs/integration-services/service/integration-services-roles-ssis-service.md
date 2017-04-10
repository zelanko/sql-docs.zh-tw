---
title: "Integration Services 角色 (SSIS 服務) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "安全性 [Integration Services], 角色"
  - "db_ssisoperator 角色"
  - "db_ssisadmin 角色"
  - "固定資料庫角色 [Integration Services]"
  - "封裝 [Integration Services], 安全性"
  - "角色 [Integration Services]"
  - "db_ssisltduser 角色"
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
caps.latest.revision: 50
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Integration Services 角色 (SSIS 服務)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供特定固定資料庫層級角色來協助保護對於儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的封裝的存取。 可用的角色根據您將封裝儲存在 SSIS 目錄資料庫 (SSISDB) 或 msdb 資料庫而有所不同。  
  
## SSIS 目錄資料庫 (SSISDB) 中的角色  
 SSIS 目錄資料庫 (SSISDB) 提供下列固定資料庫層級角色，來協助保護對於封裝和封裝相關資訊的存取。  
  
-   **ssis_admin**： 此角色提供 SSIS 目錄資料庫的完整系統管理存取權。  
  
-   **ssis_logreader**：此角色提供存取所有 SSISDB 作業記錄相關檢視的權限。  
  
     檢視清單包括：[catalog].[projects]、[catalog].[packages]、[catalog].[operations]、[catalog].[extended_operation_info]、[catalog].[operation_messages]、[catalog].[event_messages]、[catalog].[execution_data_statistics]、[catalog].[execution_component_phases]、[catalog].[execution_data_taps]、[catalog].[event_message_context]、[catalog].[executions]、[catalog].[executables]、[catalog].[executable_statistics]、[catalog].[validations]、[catalog].[execution_parameter_values] 和 [catalog].[execution_property_override_values]。  
  
## msdb 資料庫中的角色  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含以下三個固定資料庫層級角色：**db_ssisadmin**、**db_ssisltduser** 和 **db_ssisoperator**，可用於控制對儲存至 **msdb** 資料庫之封裝的存取。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 將角色指派給封裝。 角色指派會儲存到 **msdb** 資料庫。  
  
### 讀取和寫入動作  
 下表描述 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中 Windows 及固定資料庫層級角色的讀取和寫入動作。  
  
|角色|讀取動作|寫入動作|  
|----------|-----------------|------------------|  
|**db_ssisadmin**<br /><br /> 或<br /><br /> **sysadmin**|列舉自己的封裝。<br /><br /> 列舉所有封裝。<br /><br /> 檢視自己的封裝。<br /><br /> 檢視所有封裝。<br /><br /> 執行自己的封裝。<br /><br /> 執行所有封裝。<br /><br /> 匯出自己的封裝。<br /><br /> 匯出所有封裝。<br /><br /> 執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 中的所有封裝。|匯入封裝。<br /><br /> 刪除自己的封裝。<br /><br /> 刪除所有封裝。<br /><br /> 變更自己的封裝角色。<br /><br /> 變更所有封裝角色。<br /><br /> <br /><br /> **\*\* 警告 \*\***db_ssisadmin 角色和 dc_admin 角色的成員可以將其權限提高為系統管理員。 之所以能夠進行此權限提高，是因為這些角色可以修改 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，而且 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可藉由使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的 sysadmin 安全性內容由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行。 若要在執行維護計畫、資料收集組和其他 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝時預防此權限提高，請將執行封裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業設為使用有限權限的 Proxy 帳戶，或是只將系統管理員 (sysadmin) 成員加入 db_ssisadmin 和 dc_admin 角色。|  
|**db_ssisltduser**|列舉自己的封裝。<br /><br /> 列舉所有封裝。<br /><br /> 檢視自己的封裝。<br /><br /> 執行自己的封裝。<br /><br /> 匯出自己的封裝。|匯入封裝。<br /><br /> 刪除自己的封裝。<br /><br /> 變更自己的封裝角色。|  
|**db_ssisoperator**|列舉所有封裝。<br /><br /> 檢視所有封裝。<br /><br /> 執行所有封裝。<br /><br /> 匯出所有封裝。<br /><br /> 執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 中的所有封裝。|無|  
|**Windows administrators**|檢視所有正在執行之封裝的執行詳細資料。|停止所有目前正在執行的封裝。|  
  
### Sysssispackages 資料表  
 **msdb** 中的 **sysssispackages** 資料表包含儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的封裝。 如需詳細資訊，請參閱 [sysssispackages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackages-transact-sql.md)。  
  
 **sysssispackages** 資料表包括的資料行包含指派給封裝之角色的相關資訊。  
  
-   **readerrole** 資料行會指定擁有封裝之讀取權限的角色。  
  
-   **writerrole** 資料行會指定擁有封裝之寫入權限的角色。  
  
-   **ownersid** 資料行包含建立封裝之使用者的唯一安全性識別碼。 此資料行會定義封裝的擁有者。  
  
### Permissions  
 依預設，**db_ssisadmin** 和 **db_ssisoperator** 固定資料庫層級角色的權限以及建立封裝之使用者的唯一安全性識別碼會套用至封裝的讀取者角色，而 **db_ssisadmin** 角色的權限以及建立封裝之使用者的唯一安全性識別碼則會套用至封裝的寫入者角色。 使用者必須是 **db_ssisadmin**、**db_ssisltduser** 或 **db_ssisoperator** 角色的成員，才能擁有封裝的讀取權限。 使用者必須是 **db_ssisadmin** 角色的成員，才能擁有寫入權限。  
  
### 對封裝的存取權  
 固定資料庫層級角色要與使用者定義角色搭配使用。 使用者定義角色是您在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中建立後用以指派權限給封裝的角色。 若要存取封裝，使用者必須是使用者定義角色和適當 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 固定資料庫層級角色的成員。 例如，如果使用者是指派給封裝之 **AuditUsers** 使用者定義角色的成員，他們還必須是 **db_ssisadmin**、**db_ssisltduser** 或 **db_ssisoperator** 角色的成員，才能擁有封裝的讀取權限。  
  
 如果您沒有指派使用者定義角色給封裝，則對封裝的存取是由固定的資料庫層級角色決定的。  
  
 如果想要使用使用者定義角色，則必須先將這些角色加入 **msdb** 資料庫，然後才能將它們指派給封裝。 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中建立新資料庫角色。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料庫層級角色會授與 msdb 資料庫中 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 系統資料表的權限。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER 服務) 必須啟動，才能連接到 Database Engine 並存取 **msdb** 資料庫。  
  
 若要將角色指派給封裝，您需要完成下列工作。  
  
-   **開啟物件總管並連接到 Integration Services**  
  
     必須先在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中開啟 [物件總管]，並連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，才能使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 指派角色給封裝。  
  
     必須先啟動 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務，才能連接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。  
  
-   **指派讀取器和寫入器角色給封裝**  
  
     您可將讀取器和寫入器角色指派給每個封裝。  
  
## 相關工作  
  
-   [指派讀取器和寫入器角色給封裝](../../integration-services/service/assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [建立使用者定義角色](../../integration-services/service/create-a-user-defined-role.md)  
  
-   [連接到 Integration Services](../../integration-services/service/connect-to-integration-services.md)  
  
  