---
title: 部署、執行和監視 Azure 上的 SSIS 套件 | Microsoft Docs
ms.date: 02/05/2018
ms.topic: article
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2097595a90a44be6285b48be03ac9229749dd419
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="deploy-run-and-monitor-an-ssis-package-on-azure"></a>部署、執行和監視 Azure 上的 SSIS 套件
本教學課程示範如何將 SQL Server Integration Services 專案部署至 Azure SQL Database 上的 SSISDB 目錄資料庫、在 Azure SSIS Integration Runtime 中執行套件，以及監視執行中的套件。

## <a name="prerequisites"></a>Prerequisites

開始之前，請確定您有 17.2 版或更新版本的 SQL Server Management Studio。 若要下載最新版的 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

也請確定您已設定 SSISDB 資料庫和佈建 Azure SSIS Integration Runtime。 如需如何在 Azure 上佈建 SSIS 的相關資訊，請參閱[將 SSIS 套件部署到 Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal)。

> [!NOTE]
> 部署至 Azure 只支援專案部署模型。

## <a name="connect-to-the-ssisdb-database"></a>連線至 SSISDB 資料庫

使用 SQL Server Management Studio，以連線至 Azure SQL Database 伺服器上的 SSIS 目錄。 如需詳細資訊和螢幕擷取畫面，請參閱[連線至 Azure 上的 SSISDB 目錄資料庫](ssis-azure-connect-to-catalog-database.md)。

以下是兩個最重要的注意事項。 這些步驟以下列程序描述。
-   以 **mysqldbserver.database.windows.net** 格式輸入 Azure SQL Database 伺服器的完整名稱。
-   選取 `SSISDB` 作為連線的資料庫。

> [!IMPORTANT]
> Azure SQL Database 伺服器會接聽連接埠 1433。 如果您要嘗試透過公司防火牆連線至 Azure SQL Database 伺服器，則必須在公司防火牆中開啟此連接埠，讓您成功連線。

1. 開啟 SQL Server Management Studio。

2. **連線至伺服器**。 在 [連線至伺服器] 對話方塊中，輸入下列資訊：

   | 設定       | 建議值 | 描述 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器類型** | Database Engine | 這是必要的值。 |
   | **伺服器名稱** | 完整伺服器名稱 | 名稱的格式應如下所示：**mysqldbserver.database.windows.net**。 如果您需要伺服器名稱，請參閱[連線至 Azure 上的 SSISDB 目錄資料庫](ssis-azure-connect-to-catalog-database.md)。 |
   | **驗證** | SQL Server 驗證 | 本快速入門使用 SQL 驗證。 |
   | **登入** | 伺服器系統管理員帳戶 | 其為您在建立伺服器時指定的帳戶。 |
   | **密碼** | 伺服器系統管理員帳戶的密碼 | 其為您在建立伺服器時指定的密碼。 |

3. **連線至 SSISDB 資料庫**。 選取 [選項] 以展開 [連線至伺服器] 對話方塊。 在展開的 [連線至伺服器] 對話方塊中，選取 [連線屬性] 索引標籤。在 [連線至資料庫] 欄位中，選取或輸入 `SSISDB`。

4. 然後選取 [連線]。 [物件總管] 視窗會在 SSMS 中開啟。 

5. 在 [物件總管] 中，展開 [Integration Services 目錄]，然後展開 [SSISDB] 以檢視 SSIS 目錄資料庫中的物件。

## <a name="deploy-a-project-with-the-deployment-wizard"></a>使用部署精靈部署專案

若要進一步了解有關部署套件和部署精靈，請參閱[部署 Integration Services (SSIS) 專案和套件](../packages/deploy-integration-services-ssis-projects-and-packages.md)和 [Integration Services 部署精靈](../packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard)。

### <a name="start-the-integration-services-deployment-wizard"></a>啟動 [Integration Services 部署精靈]
1. 在 SSMS 的 [物件總管] 中，展開 [Integration Services 目錄] 節點和 [SSISDB] 節點之後，請展開專案資料夾。

2.  選取 [專案] 節點。

3.  以滑鼠右鍵按一下 [專案] 節點，然後選取 [部署專案]。 即會開啟 [Integration Services 部署精靈]。 您可以從 SSIS 目錄資料庫或檔案系統部署專案。

    ![從 SSMS 部署專案](media/ssis-azure-deploy-run-monitor-tutorial/ssisdb-deploy-project1.png)

    ![SSIS 部署精靈對話方塊隨即開啟](media/ssis-azure-deploy-run-monitor-tutorial/ssisdb-deploy-project2.png)

### <a name="deploy-a-project-with-the-deployment-wizard"></a>使用部署精靈部署專案
1. 在部署精靈的 [簡介] 頁面上，檢閱簡介。 選取 [下一步] 開啟 [選取來源] 頁面。

2. 在 [選取來源] 頁面上，選取要部署的現有 SSIS 專案。
    -   若要部署您建立的專案部署檔案，請選取 [專案部署檔案]  ，並輸入 .ispac 檔案的路徑。
    -   若要部署位於 SSIS 目錄中的專案，請選取 [Integration Services 目錄]，然後輸入伺服器名稱以及該專案在目錄中的路徑。
    -   選取 [下一步] 查看 [選取目的地] 頁面。
  
3.  在 [選取目的地] 頁面上，選取專案目的地。
    -   輸入完整伺服器名稱，格式如下：`<server_name>.database.windows.net`。
    -   然後選取 [瀏覽] 在 SSISDB 中選取目標資料夾。
    -   選取 [下一步] 開啟 [檢閱] 頁面。  
  
4.  在 [檢閱] 頁面上，檢閱您選取的設定。
    -   您可以選取 **[上一步]**，或選取左窗格中的任何步驟來變更您的選取項目。
    -   選取 [部署]  開始部署程序。

    > ![注意] 如果您收到**沒有使用中的背景工作代理程式。(.Net SqlClient 資料提供者)** 錯誤訊息，請確認 Azure-SSIS Integration Runtime 正在執行。 如果您在 Azure SSIS IR 處於停止狀態時嘗試部署，就會發生這個錯誤。

5.  完成部署程序之後，會開啟 [結果] 頁面。 此頁面會顯示每個動作執行成功或失敗。
    -   如果動作失敗，請選取 [結果] 資料行中的 [失敗] 以顯示錯誤的說明。
    -   選擇性：選取 [儲存報表...]，將結果儲存到 XML 檔案。
    -   選取 [關閉] 結束此精靈。

## <a name="deploy-a-project-with-powershell"></a>使用 PowerShell 部署專案

若要使用 PowerShell 將專案部署到 Azure SQL Database 上的 SSISDB，請根據您的需求調整下列指令碼。 指令碼會列舉 `$ProjectFilePath` 下的子資料夾及各個子資料夾中的專案，然後在 SSISDB 中建立相同資料夾，並將專案部署到這些資料夾。

此指令碼要求在您執行指令碼的電腦上，安裝 SQL Server Data Tools 17.x 版或 SQL Server Management Studio。

```powershell
# Variables
$ProjectFilePath = "C:\<folder>"
$SSISDBServerEndpoint = "<servername>.database.windows.net"
$SSISDBServerAdminUserName = "<username>"
$SSISDBServerAdminPassword = "<password>"

# Load the IntegrationServices Assembly
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices") | Out-Null;

# Store the IntegrationServices Assembly namespace to avoid typing it every time
$ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"

Write-Host "Connecting to server ..."

# Create a connection to the server
$sqlConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword + ";Initial Catalog=SSISDB"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection

# Get the catalog
$catalog = $integrationServices.Catalogs['SSISDB']

write-host "Enumerating all folders..."

$folders = ls -Path $ProjectFilePath -Directory

if ($folders.Count -gt 0)
{
    foreach ($filefolder in $folders)
    {
        Write-Host "Creating Folder " $filefolder.Name " ..."

        # Create a new folder
        $folder = New-Object $ISNamespace".CatalogFolder" ($catalog, $filefolder.Name, "Folder description")
        $folder.Create()

        $projects = ls -Path $filefolder.FullName -File -Filter *.ispac
        if ($projects.Count -gt 0)
        {
            foreach($projectfile in $projects)
            {
                $projectfilename = $projectfile.Name.Replace(".ispac", "")
                Write-Host "Deploying " $projectfilename " project ..."

                # Read the project file, and deploy it to the folder
                [byte[]] $projectFileContent = [System.IO.File]::ReadAllBytes($projectfile.FullName)
                $folder.DeployProject($projectfilename, $projectFileContent)
            }
        }
    }
}

Write-Host "All done." 
```

## <a name="run-a-package"></a>執行套件

1. 在 SSMS 的 [物件總管] 中，選取您要執行的套件。

2. 按一下滑鼠右鍵並選取 [執行]，以開啟 [執行套件] 對話方塊。

3.  在 [執行套件] 對話方塊中，使用 [參數]、[連線管理員] 和 [進階] 索引標籤上的設定，設定套件執行。

4.  選取 [確定] 以執行套件。

## <a name="monitor-the-running-package-in-ssms"></a>監視 SSMS 的執行中套件

若要檢視 Integration Services 伺服器上目前正在執行中的 Integration Services 作業 (例如，部署、驗證及套件執行) 的狀態，請使用 [作用中的作業] 對話方塊。 若要開啟 [作用中的作業] 對話方塊，請以滑鼠右鍵按一下 [SSISDB]，然後選取 [作用中的作業]。

您也可以在 [物件總管] 中選取套件，並按一下滑鼠右鍵，然後依序選取 [報表]、[標準報表] 和 [所有執行]。

如需如何監視 SSMS 之執行中套件的詳細資訊，請參閱[監視執行中的套件和其他作業](https://docs.microsoft.com/sql/integration-services/performance/monitor-running-packages-and-other-operations)。

## <a name="monitor-the-azure-ssis-integration-runtime"></a>監視 Azure SSIS Integration Runtime

若要取得套件執行所在之 Azure SSIS Integration Runtime 的相關狀態資訊，請使用下列 PowerShell 命令：針對每個命令，提供資料處理站、Azure SSIS IR 和資源群組的名稱。

### <a name="get-metadata-about-the-azure-ssis-integration-runtime"></a>取得 Azure SSIS Integration Runtime 的相關中繼資料

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

### <a name="get-the-status-of-the-azure-ssis-integration-runtime"></a>取得 Azure SSIS Integration Runtime 的狀態

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -Status -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

## <a name="next-steps"></a>後續步驟
- 了解如何排程套件執行。 如需詳細資訊，請參閱[排程 Azure 上的 SSIS 套件執行](ssis-azure-schedule-packages.md)
