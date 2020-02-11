---
title: SSIS 目錄 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 24bd987e-164a-48fd-b4f2-cbe16a3cd95e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 14de3fa15fa5a648c2d41824d237040b5aa085e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62771574"
---
# <a name="ssis-catalog"></a>SSIS 目錄
  `SSISDB`目錄是處理您已部署至[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]伺服器之[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] （SSIS）專案的中心點。 例如，您可以設定專案和封裝參數、設定環境以指定封裝的執行值、執行和疑難排解封裝，以及管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器作業。  
  
 儲存在`SSISDB`目錄中的物件包括專案、封裝、參數、環境和操作歷程記錄。  
  
 您可以藉由查詢`SSISDB` `SSISDB`資料庫中的 views，檢查儲存在目錄中的物件、設定和運算元據。 您可以藉由呼叫`SSISDB`資料庫中的預存程式，或使用`SSISDB`目錄的 UI 來管理物件。 在許多情況下，可以在此 UI 中或是藉由呼叫預存程序來執行相同的工作。  
  
 若要維護 `SSISDB` 資料庫，建議您套用管理使用者資料庫的標準企業原則。 如需有關建立維護計畫的詳細資訊，請參閱＜ [Maintenance Plans](../../relational-databases/maintenance-plans/maintenance-plans.md)＞。  
  
 `SSISDB`目錄和`SSISDB`資料庫支援 Windows PowerShell。 如需有關使用 SQL Server 搭配 Windows PowerShell 的詳細資訊，請參閱＜ [SQL Server PowerShell](../../powershell/sql-server-powershell.md)＞。 如需有關如何使用 Windows PowerShell 完成部署專案等工作的範例，請參閱 blogs.msdn.com 上的部落格文章： [SQL Server 2012 中的 SSIS 和 PowerShell](https://go.microsoft.com/fwlink/?LinkId=242539)。  
  
 如需有關如何查看作業資料的詳細資訊，請參閱[監視封裝執行和其他作業](../performance/monitor-running-packages-and-other-operations.md)。  
  
 若要存取`SSISDB`中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的目錄，請連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到資料庫引擎，然後在物件總管中展開 [ **Integration Services 目錄**] 節點。 您可以藉`SSISDB`由展開[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]物件總管中的 [資料庫] 節點來存取中的資料庫。  
  
> [!NOTE]  
>  您無法重新命名`SSISDB`資料庫。  
  
> [!NOTE]  
>  如果`SSISDB`資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所連接的實例已停止或沒有回應，isserverexec.exe 程式就會結束。 會在 Windows 事件記錄檔中寫入一則訊息。  
>   
>  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源的容錯移轉是叢集容錯移轉的一部分，就不會重新啟動執行中的封裝。 您可以使用檢查點重新啟動封裝。 如需詳細資訊，請參閱[使用檢查點來重新啟動封裝](../packages/restart-packages-by-using-checkpoints.md)。  
  
## <a name="catalog-object-identifiers"></a>目錄物件識別碼  
 當您在目錄中建立新的物件時，請為此物件指派名稱。 物件名稱是識別碼。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會定義哪些字元可以在識別碼中使用的規則。 隨後的物件名稱必須遵照識別碼規則。  
  
-   資料夾  
  
-   隨附此逐步解說的專案  
  
-   環境  
  
-   參數  
  
-   環境變數  
  
### <a name="folder-project-environment"></a>資料夾、專案、環境  
 在重新命名資料夾、專案或環境時，請考慮以下規則。  
  
-   無效的字元包括 ASCII/Unicode 字元 1 到 31、引號 (")、小於 (\<)、大於 (>)、直立線符號 (|)、退格鍵 (\b)、null (\0) 和 Tab 鍵 (\t)。  
  
-   名稱不得包含開頭或尾端空格。  
  
-   不允許以 \@ 作為第一個字元，但隨後的字元可以使用 \@。  
  
-   名稱的長度必須大於 0 且小於或等於 128。  
  
### <a name="parameter"></a>參數  
 在命名參數時，請考慮以下規則。  
  
-   名稱的第一個字元必須是 Unicode Standard 2.0 中所定義的字母，或是底線 (_)。  
  
-   後續的字元可以是 Unicode Standard 2.0 中定義的字母或數字，或是底線 (_)。  
  
### <a name="environment-variable"></a>環境變數  
 在命名環境變數時，請考慮以下規則。  
  
-   無效的字元包括 ASCII/Unicode 字元 1 到 31、引號 (")、小於 (\<)、大於 (>)、直立線符號 (|)、退格鍵 (\b)、null (\0) 和 Tab 鍵 (\t)。  
  
-   名稱不得包含開頭或尾端空格。  
  
-   不允許以 \@ 作為第一個字元，但隨後的字元可以使用 \@。  
  
-   名稱的長度必須大於 0 且小於或等於 128。  
  
-   名稱的第一個字元必須是 Unicode Standard 2.0 中所定義的字母，或是底線 (_)。  
  
-   後續的字元可以是 Unicode Standard 2.0 中定義的字母或數字，或是底線 (_)。  
  
## <a name="catalog-configuration"></a>目錄組態  
 您會藉由調整目錄屬性來微調目錄的行為模式。 目錄屬性會定義如何加密敏感性資料以及如何保留作業和專案版本設定資料。 若要設定目錄屬性，請使用 [目錄屬性]**** 對話方塊，或是呼叫 [catalog.configure_catalog &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database) 預存程序。 若要檢視屬性，請使用對話方塊或查詢 [catalog.catalog_properties &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database)。 您可在 [物件總管] 中以滑鼠右鍵按一下 `SSISDB` 來存取此對話方塊。  
  
### <a name="operations-and-project-version-cleanup"></a>作業和專案版本清除  
 目錄中許多作業的狀態資料會儲存在內部資料庫資料表中。 例如，目錄會追蹤封裝執行和專案部署的狀態。 為了維護作業資料的大小， **中的** [SSIS Server 維護作業] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會用來移除舊的資料。 安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時會建立此 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Agent 作業。  
  
 若要更新或重新部署 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，請使用相同名稱將它部署到目錄中的相同資料夾。 根據預設，每次您重新部署專案時， `SSISDB`目錄都會保留舊版的專案。 為了維護作業資料的大小， **[SSIS Server 維護作業]** 會用來移除專案的舊版。  
  
 下列`SSISDB`目錄屬性會定義此[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式作業的行為。 您可以使用 [目錄屬性]**** 對話方塊或使用 [catalog.catalog_properties &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database) 和 [catalog.configure_catalog &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database) 檢視及修改屬性。  
  
 **定期清除記錄檔**  
 當這個屬性設定為 `True` 時，便會執行作業清除的作業步驟。  
  
 **保留期間（天）**  
 定義可允許的作業資料存在時間上限 (以天為單位)。 移除較舊的資料。  
  
 最小值是一天。 最大值只受限於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `int`資料的最大值。 如需此資料類型的資訊，請參閱 [int、bigint、smallint 和 tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)。  
  
 **定期移除舊版本**  
 當這個屬性設定為 `True` 時，便會執行專案版本清除的作業步驟。  
  
 **每個專案的版本數目上限**  
 定義多少個專案版本儲存在目錄中。 移除專案的舊版。  
  
### <a name="encryption-algorithm"></a>加密演算法  
 
  **[加密演算法]** 屬性會指定用來加密敏感性參數值的加密類型。 您可以從以下類型的加密中選擇。  
  
-   AES_256 (預設)  
  
-   AES_192  
  
-   AES_128  
  
-   DESX  
  
-   TRIPLE_DES_3KEY  
  
-   TRIPLE_DES  
  
-   DES  
  
 當您將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]伺服器時，目錄會自動將封裝資料與敏感值加密。 當您擷取時，目錄也會自動解密資料。 SSISDB 目錄會使用 `ServerStorage` 保護等級。 如需詳細資訊，請參閱 [Access Control for Sensitive Data in Packages](../security/access-control-for-sensitive-data-in-packages.md)。  
  
 變更加密演算法是需要大量時間的作業。 首先，伺服器必須使用先前指定的演算法來解密所有組態值。 然後，伺服器必須使用新的演算法來重新加密值。 在這段期間，伺服器上不能有其他的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 作業。 因此，為了讓 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 作業持續不受干擾，在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的此對話方塊中，加密演算法會是唯讀值。  
  
 若要變更 [**加密演算法]** 屬性設定， `SSISDB`請將資料庫設定為單一使用者模式，然後呼叫 catalog. configure_catalog 預存程式。 使用 ENCRYPTION_ALGORITHM 指定 *property_name* 引數。 如需支援的屬性值，請參閱 [catalog.catalog_properties &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database)。 如需預存程序的詳細資訊，請參閱 [catalog.configure_catalog &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database)。  
  
 如需單一使用者模式的詳細資訊，請參閱 [將資料庫設定為單一使用者模式](../../relational-databases/databases/set-a-database-to-single-user-mode.md)。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中加密和加密演算法的資訊，請參閱 [SQL Server 加密](../../relational-databases/security/encryption/sql-server-encryption.md)一節中的主題。  
  
 資料庫主要金鑰會用於加密。 當您建立目錄時會建立此金鑰。 如需詳細資訊，請參閱 [建立 SSIS 目錄](ssis-catalog.md)。  
  
 下表列出 **[目錄屬性]** 對話方塊中所顯示的屬性名稱，以及資料庫檢視中的對應屬性。  
  
|屬性名稱 (**[目錄屬性]** 對話方塊)|屬性名稱 (資料庫檢視)|  
|---------------------------------------------------------|-------------------------------------|  
|加密演算法名稱|ENCRYPTION_ALGORITHM|  
|定期清除記錄檔|OPERATION_CLEANUP_ENABLED|  
|保留週期 (天)|RETENTION_WINDOW|  
|定期移除舊版本|VERSION_CLEANUP_ENABLED|  
|每一專案的版本數目上限|MAX_PROJECT_VERSIONS|  
|全伺服器的預設記錄層次|SERVER_LOGGING_LEVEL|  
  
## <a name="permissions"></a>權限  
 專案、環境和封裝會包含在屬於安全性實體物件的資料夾中。 您可以將權限授與資料夾，包括 MANAGE_OBJECT_PERMISSIONS 權限。 MANAGE_OBJECT_PERMISSIONS 可讓您將資料夾內容管理委派給使用者，而不必將使用者成員資格授與 ssis_admin 角色。 您還可以授與權限給專案、環境和作業。 作業包括初始化[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、部署專案、建立和啟動執行、驗證專案和封裝，以及設定`SSISDB`目錄。  
  
 如需資料庫角色的詳細資訊，請參閱 [資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)。  
  
 SSISDB 目錄會使用 DDL 觸發程序 ddl_cleanup_object_permissions 來強制 SSIS 安全性實體之權限資訊的完整性。 當資料庫主體 (例如資料庫使用者、資料庫角色或資料庫應用程式角色) 從 SSISDB 資料庫中移除時，便會引發此觸發程序。  
  
 如果此主體已被授與或拒絕其他主體的權限，請撤銷授與者所提供的權限，然後才可移除該主體。 否則，當系統嘗試移除此主體時，便會傳回錯誤訊息。 此觸發程序會移除所有權限記錄，在這些記錄中，資料庫主體為被授與者。  
  
 建議您不要停用觸發程式，因為它可確保在從`SSISDB`資料庫卸載資料庫主體之後，不會有任何孤立的許可權記錄。  
  
### <a name="managing-permissions"></a>管理權限  
 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] UI、預存程序及 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空間來管理權限。  
  
 若要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] UI 管理權限，請使用以下對話方塊。  
  
-   針對資料夾，使用 **Folder Properties Dialog Box** 的 [&#91;權限&#93;](folder-properties-dialog-box.md)頁面。  
  
-   針對專案中，使用 **權限** 頁面 [Project Properties Dialog Box](project-properties-dialog-box.md)。  
  
 若要使用 Transact-sql 管理許可權，請呼叫[catalog. grant_permission &#40;ssisdb 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database)，[目錄。 deny_permission &#40;ssisdb](/sql/integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database)資料庫&#41;和[目錄。 revoke_permission &#40;ssisdb 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database)。 若要檢視對所有物件之目前主體有效的權限，請查詢 [catalog.effective_object_permissions &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-effective-object-permissions-ssisdb-database)。 此主題會提供不同類型之權限的描述。 若要檢視已明確指派給使用者的權限，請查詢 [catalog.explicit_object_permissions &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database)。  
  
## <a name="folders"></a>資料夾  
 資料夾包含目錄中的`SSISDB`一個或多個專案和環境。 您可以使用 [catalog.folders &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-folders-ssisdb-database) 檢視來存取目錄中資料夾的相關資訊。 您可以使用以下預存程序來管理資料夾。  
  
-   [catalog.create_folder &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database)  
  
-   [catalog.delete_folder &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database)  
  
-   [catalog.rename_folder &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database)  
  
-   [catalog.set_folder_description &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database)  
  
## <a name="projects-and-packages"></a>專案和封裝  
 每一個專案都可包含多個封裝。 專案和封裝都可以包含參數及環境的參考。 您可以使用 [Configure Dialog Box](configure-dialog-box.md)來存取參數和環境參考。  
  
 您可以藉由呼叫以下預存程序來完成其他專案工作。  
  
-   [catalog.delete_project &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database)  
  
-   [catalog.deploy_project &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database)  
  
-   [catalog.get_project &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-get-project-ssisdb-database)  
  
-   [catalog.move_project &#40;&#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-move-project-ssisdb-database)  
  
-   [catalog.restore_project &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database)  
  
 這些檢視表會提供有關封裝、專案和專案版本的詳細資料。  
  
-   [catalog.projects &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-projects-ssisdb-database)  
  
-   [catalog.packages &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-packages-ssisdb-database)  
  
-   [catalog.object_versions &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-object-versions-ssisdb-database)  
  
## <a name="parameters"></a>參數  
 您在封裝執行時，可使用參數將值指派給封裝屬性。 若要設定封裝或專案參數的值及清除該值，請呼叫 [catalog.set_object_parameter_value &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database) 和 [catalog.clear_object_parameter_value &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database)。 若要為執行的執行個體設定參數值，請呼叫 [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)。 您可以藉由呼叫 [catalog.get_parameter_values &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database) 擷取預設參數值。  
  
 這些檢視表會顯示所有封裝和專案的參數，以及用於執行執行個體的參數值。  
  
-   [catalog.object_parameters &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database)  
  
-   [catalog.execution_parameter_values &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-execution-parameter-values-ssisdb-database)  
  
## <a name="server-environments-server-variables-and-server-environment-references"></a>伺服器環境、伺服器變數和伺服器環境參考  
 伺服器環境包含伺服器變數。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上執行或驗證封裝時，可以使用變數值。  
  
 以下預存程序可讓您執行環境與變數的許多其他管理工作。  
  
-   [catalog.create_environment &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database)  
  
-   [catalog.delete_environment &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database)  
  
-   [catalog.move_environment &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database)  
  
-   [catalog.rename_environment &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database)  
  
-   [catalog.set_environment_property &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database)  
  
-   [catalog.create_environment_variable &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database)  
  
-   [catalog.delete_environment_variable &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database)  
  
-   [catalog.set_environment_variable_property &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database)  
  
-   [catalog.set_environment_variable_value &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database)  
  
 您可以藉由呼叫 [catalog.set_environment_variable_protection &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database) 預存程序，設定變數的敏感度位元。  
  
 若要使用伺服器變數的值，請指定專案與伺服器環境之間的參考。 您可以使用以下預存程序來建立和刪除參考。 您也可以指出環境是否位於與專案相同的資料夾中，或是在不同的資料夾中。  
  
-   [catalog.create_environment_reference &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database)  
  
-   [catalog.delete_environment_reference &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database)  
  
-   [catalog.set_environment_reference_type &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database)  
  
 如需有關環境和變數的其他詳細資料，請查詢這些檢視表。  
  
-   [catalog.environments &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-environments-ssisdb-database)  
  
-   [catalog.environment_variables &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-environment-variables-ssisdb-database)  
  
-   [catalog.environment_references &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-environment-references-ssisdb-database)  
  
## <a name="executions-and-validations"></a>執行和驗證  
 執行是封裝執行的執行個體。 呼叫 [catalog.create_execution &#40;SSISDB Database&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) 及 [catalog.start_execution &#40;SSISDB Database&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) 可建立並開始執行。 若要停止執行或封裝/專案驗證，請呼叫 [catalog.stop_operation &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database)。  
  
 若要使執行中的封裝暫停並建立傾印檔案，請呼叫 catalog.create_execution_dump 預存程序。 傾印檔案會提供有關封裝執行的資訊，可幫助您針對執行問題進行疑難排解。 如需有關產生及設定傾印檔案的詳細資訊，請參閱＜ [Generating Dump Files for Package Execution](../troubleshooting/generating-dump-files-for-package-execution.md)＞。  
  
 如需有關作業期間所記錄之執行、驗證和訊息以及與錯誤相關之內容資訊的詳細資料，請查詢這些檢視表。  
  
-   [catalog.executions &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database)  
  
-   [catalog.operations &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database)  
  
-   [catalog.operation_messages &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database)  
  
-   [catalog.extended_operation_info &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-extended-operation-info-ssisdb-database)  
  
-   [catalog.event_messages](/sql/integration-services/system-views/catalog-event-messages)  
  
-   [catalog.event_message_context](/sql/integration-services/system-views/catalog-event-message-context)  
  
 您可以藉由呼叫 [catalog.validate_project &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database) 和 [catalog.validate_package &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database) 預存程序來驗證專案與封裝。 
  [catalog.validations &#40;SSISDB Database&#41;](/sql/integration-services/system-views/catalog-validations-ssisdb-database) 檢視會提供有關驗證的詳細資料，例如驗證時所考量的伺服器環境參考、這是相依性驗證還是完整驗證，以及使用 32 位元執行階段還是 64 位元執行階段來執行封裝。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [建立 SSIS 目錄](ssis-catalog.md)  
  
-   [備份、 還原和移動的 SSIS 目錄](../backup-restore-and-move-the-ssis-catalog.md)  
  
## <a name="related-content"></a>相關內容  
  
-   blogs.msdn.com 上的部落格文章： [SQL Server 2012 中的 SSIS 和 PowerShell](https://go.microsoft.com/fwlink/?LinkId=242539)。  
  
-   blogs.msdn.com 上的部落格文章： [SSIS 目錄存取控制提示](https://go.microsoft.com/fwlink/?LinkId=246669)。  
  
-   blogs.msdn.com 上的部落格文章 [SSIS 目錄管理物件模型初探](https://go.microsoft.com/fwlink/?LinkId=254267)。  
  
  
