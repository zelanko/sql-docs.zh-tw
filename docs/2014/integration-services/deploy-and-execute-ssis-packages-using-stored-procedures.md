---
title: 部署和使用預存程序執行 SSIS 套件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 60914b0c-1f65-45f8-8132-0ca331749fcc
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5aee74a2b0bd632e2efcb780a52f1b05f1949669
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210937"
---
# <a name="deploy-and-execute-ssis-packages-using-stored-procedures"></a>使用預存程序部署及執行 SSIS 封裝
  當您設定 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案來使用專案部署模型時，您可以使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 目錄中的預存程序來部署專案及執行封裝。 如需有關專案部署模型的詳細資訊，請參閱＜ [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)＞。  
  
 您也可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 部署專案及執行封裝。 如需詳細資訊，請參閱＜ **另請參閱** ＞一節中的主題。  
  
> [!TIP]
>  您可以執行以下動作，輕鬆地針對底下程序中所列的預存程序產生 Transact-SQL 陳述式 (除了 catalog.deploy_project 以外)：  
> 
>  1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中，展開 [物件總管] 中的 **Integration Services 目錄** 節點，並導覽到您要執行的封裝。  
> 2.  以滑鼠右鍵按一下封裝，然後按一下 [執行]。  
> 3.  請視需要在 **[進階]** 索引標籤中設定參數值、連接管理員屬性和選項，例如記錄層次。  
> 
>      如需有關記錄層級的詳細資訊，請參閱＜ [在 SSIS 伺服器上啟用封裝執行的記錄功能](../../2014/integration-services/enable-logging-for-package-execution-on-the-ssis-server.md)＞。  
> 4.  在按一下 **[確定]** 執行封裝之前，請按一下 **[指令碼]**。 Transact-SQL 會出現在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的 [查詢編輯器] 視窗中。  
  
## <a name="to-deploy-and-execute-a-package-using-stored-procedures"></a>若要使用預存程序部署及執行封裝  
  
1.  呼叫 [catalog.deploy_project &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database) 將包含封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器。  
  
     若要擷取 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案部署檔案的二進位內容，請針對 *@project_stream* 參數使用 SELECT 陳述式搭配 OPENROWSET 函數和 BULK 資料列集提供者。 BULK 資料列集提供者可讓您從檔案讀取資料。 BULK 資料列集提供者的 SINGLE_BLOB 引數會傳回資料檔的內容當做類型為 varbinary(max) 的單一資料列、單一資料行資料列集。 如需詳細資訊，請參閱 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)。  
  
     在下列範例中，SSISPackages_ProjectDeployment 專案會部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器上的 [SSIS 封裝] 資料夾。 二進位資料會從專案檔 (SSISPackage_ProjectDeployment.ispac) 讀取，並且儲存在類型為 varbinary(max) 的 *@ProjectBinary* 參數中。 *@ProjectBinary* 參數值會指派給 *@project_stream* 參數。  
  
    ```  
    DECLARE @ProjectBinary as varbinary(max)  
    DECLARE @operation_id as bigint  
    Set @ProjectBinary = (SELECT * FROM OPENROWSET(BULK 'C:\MyProjects\ SSISPackage_ProjectDeployment.ispac', SINGLE_BLOB) as BinaryData)  
  
    Exec catalog.deploy_project @folder_name = 'SSIS Packages', @project_name = 'DeployViaStoredProc_SSIS', @Project_Stream = @ProjectBinary, @operation_id = @operation_id out  
  
    ```  
  
2.  呼叫 [catalog.create_execution &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) 來建立封裝執行的執行個體，並選擇性地呼叫 [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) 來設定執行階段參數值。  
  
     在下列範例中，catalog.create_execution 會針對 SSISPackage_ProjectDeployment 專案中包含的 package.dtsx 建立執行個體。 此專案位於 SSIS 封裝資料夾內。 此預存程序傳回的 execution_id 是用在 catalog.set_execution_parameter_value 的呼叫中。 此第二個預存程序會將 LOGGING_LEVEL 參數設定為 3 (詳細資訊記錄)，並將名為 Parameter1 的封裝參數設定為 1 的值。  
  
     對於參數 (例如 LOGGING_LEVEL)，object_type 的值為 50。 若為封裝參數，object_type 的值為 30。  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    GO  
  
    ```  
  
3.  呼叫 [catalog.start_execution &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) 來執行封裝。  
  
     在下列範例中，catalog.start_execution 的呼叫會加入至 Transact-SQL 來開始執行封裝。 使用 catalog.create_execution 預存程序所傳回的 execution_id。  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    EXEC [SSISDB].[catalog].[start_execution] @execution_id  
    GO  
  
    ```  
  
## <a name="to-deploy-a-project-from-server-to-server-using-stored-procedures"></a>若要使用預存程序在不同伺服器之間部署專案  
 您可以使用 [catalog.get_project &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-get-project-ssisdb-database) 和 [catalog.deploy_project &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database) 預存程序在不同伺服器之間部署專案。  
  
 在執行預存程序之前，您必須執行下列動作。  
  
-   建立連結的伺服器物件。 如需詳細資訊，請參閱[建立連結的伺服器 &#40;SQL Server Database Engine&#41;](../database-engine/sql-server-database-engine-overview.md)。  
  
     在 **[連結的伺服器屬性]** 對話方塊的 **[伺服器選項]** 頁面上，將 **[RPC]** 和 **[RPC 輸出]** 設定為 **[True]**。 此外，也將 **[啟用 RPC 的分散式交易促銷]** 設定為 **[False]**。  
  
-   若要針對您為連結的伺服器選取的提供者啟用動態參數，請在物件總管中展開 [連結的伺服器] 下方的 [提供者] 節點，以滑鼠右鍵按一下此提供者，然後按一下 [屬性]。 選取 **[動態參數]** 旁邊的 **[啟用]**。  
  
-   確認兩部伺服器上都已啟動分散式交易協調器 (DTC)。  
  
 呼叫 catalog.get_project 來傳回專案的二進位內容，然後呼叫 catalog.deploy_project。 catalog.get_project 傳回的值會插入 varbinary(max) 類型的資料表變數中。 連結的伺服器無法傳回屬於 varbinary(max) 的結果。  
  
 在下列範例中，catalog.get_project 會針對連結的伺服器上的 SSISPackages 專案傳回二進位內容。 catalog.deploy_project 會將專案部署到本機伺服器的 DestFolder 資料夾。  
  
```  
declare @resultsTableVar table (  
project_binary varbinary(max)  
)  
  
INSERT @resultsTableVar (project_binary)  
EXECUTE [MyLinkedServer].[SSISDB].[catalog].[get_project] 'Packages', 'SSISPackages'  
  
declare @project_binary varbinary(max)  
select @project_binary = project_binary from @resultsTableVar  
  
exec [SSISDB].[CATALOG].[deploy_project] 'DestFolder', 'SSISPackages', @project_binary  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [將專案部署至 Integration Services 伺服器](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [在 SQL Server Data Tools 中執行封裝](../../2014/integration-services/run-a-package-in-sql-server-data-tools.md)   
 [使用 SQL Server Management Studio 在 SSIS 伺服器上執行封裝](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
  
