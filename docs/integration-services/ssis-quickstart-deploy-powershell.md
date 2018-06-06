---
title: 使用 PowerShell 部署 SSIS 專案 | Microsoft Docs
ms.date: 05/21/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: quick-start
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f245553e318ccdba4f8f5d212e5c4c92ec5564ca
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
ms.locfileid: "34455121"
---
# <a name="deploy-an-ssis-project-with-powershell"></a>使用 PowerShell 部署 SSIS 專案
本快速入門示範如何使用 PowerShell 指令碼連線至資料庫伺服器，並將 SSIS 專案部署到 SSIS 目錄。

## <a name="prerequisites"></a>Prerequisites

Azure SQL Database 伺服器會接聽連接埠 1433。 如果您要嘗試透過公司防火牆連線至 Azure SQL Database 伺服器，則必須在公司防火牆中開啟此連接埠，讓您成功連線。

## <a name="supported-platforms"></a>支援的平台

您可以使用本快速入門中的資訊，將 SSIS 套件部署到下列平台：

-   Windows 上的 SQL Server。

-   Azure SQL Database。 如需在 Azure 部署和執行套件的詳細資訊，請參閱[將 SQL Server Integration Services 工作負載隨即轉移至雲端](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)。

您無法使用本快速入門中的資訊，將 SSIS 套件部署到 Linux 上的 SQL Server。 如需在 Linux 上執行套件詳細資訊，請參閱[使用 SSIS 在 Linux 上擷取、轉換和載入資料](../linux/sql-server-linux-migrate-ssis.md)。

## <a name="for-azure-sql-database-get-the-connection-info"></a>針對 Azure SQL Database，請取得連線資訊

若要將專案部署到 Azure SQL Database，請取得連線至 SSIS 目錄資料庫 (SSISDB) 所需的連線資訊。 在下列程序中，您需要完整伺服器名稱和登入資訊。

1. 登入 [Azure 入口網站](https://portal.azure.com/)。
2. 從左側功能表中選取 [SQL 資料庫]，然後選取 [SQL 資料庫] 頁面上的 SSISDB 資料庫。 
3. 在您資料庫的 [概觀] 頁面上，檢閱完整伺服器名稱。 若要顯示 [按一下以複製] 選項，請將滑鼠指標暫留在伺服器名稱上。 
4. 如果您忘記 Azure SQL Database 伺服器登入資訊，請巡覽至 [SQL Database 伺服器] 頁面來檢視伺服器管理員名稱。 如有需要，您可以重設密碼。
5. 按一下 [顯示資料庫連接字串]。
6. 檢閱完整 **ADO.NET** 連接字串。

## <a name="powershell-script"></a>PowerShell 指令碼
為下列指令碼上方的變數提供適當的值，然後執行指令碼部署 SSIS 專案。

> [!NOTE]
> 下列範例會使用 Windows 驗證來部署至內部部署的 SQL Server。 若要使用 SQL Server 驗證，請使用 `User ID=<user name>;Password=<password>;` 取代 `Integrated Security=SSPI;` 引數。 如果要連線至 Azure SQL Database 伺服器，您無法使用 Windows 驗證。

```powershell
# Variables
$SSISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"
$TargetServerName = "localhost"
$TargetFolderName = "Project1Folder"
$ProjectFilePath = "C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac"
$ProjectName = "Integration Services Project1"

# Load the IntegrationServices assembly
$loadStatus = [System.Reflection.Assembly]::Load("Microsoft.SQLServer.Management.IntegrationServices, "+
    "Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91, processorArchitecture=MSIL")

# Create a connection to the server
$sqlConnectionString = `
    "Data Source=" + $TargetServerName + ";Initial Catalog=master;Integrated Security=SSPI;"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $SSISNamespace".IntegrationServices" $sqlConnection

# Get the Integration Services catalog
$catalog = $integrationServices.Catalogs["SSISDB"]

# Create the target folder
$folder = New-Object $SSISNamespace".CatalogFolder" ($catalog, $TargetFolderName,
    "Folder description")
$folder.Create()

Write-Host "Deploying " $ProjectName " project ..."

# Read the project file and deploy it
[byte[]] $projectFile = [System.IO.File]::ReadAllBytes($ProjectFilePath)
$folder.DeployProject($ProjectName, $projectFile)

Write-Host "Done."
```

## <a name="next-steps"></a>後續步驟
- 請考慮使用其他方式來部署套件。
    - [使用 SSMS 部署 SSIS 套件](./ssis-quickstart-deploy-ssms.md)
    - [使用 Transact-SQL 部署 SSIS 套件 (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [使用 Transact-SQL 部署 SSIS 套件 (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [從命令提示字元中部署 SSIS 套件](./ssis-quickstart-deploy-cmdline.md)
    - [使用 C# 部署 SSIS 套件](./ssis-quickstart-deploy-dotnet.md) 
- 執行已部署的套件。 若要執行套件，您可以從數個工具和語言進行選擇。 如需詳細資訊，請參閱下列文章：
    - [使用 SSMS 執行 SSIS 套件](./ssis-quickstart-run-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元中執行 SSIS 套件](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 套件](ssis-quickstart-run-powershell.md)
    - [使用 C# 執行 SSIS 套件](./ssis-quickstart-run-dotnet.md) 
