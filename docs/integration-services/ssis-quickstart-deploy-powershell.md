---
title: "使用 PowerShell 部署 SSIS 專案 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: quick-start
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d23639aa98492228fdec5d45799718f59b809425
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="deploy-an-ssis-project-with-powershell"></a>使用 PowerShell 部署 SSIS 專案
本快速入門教學課程示範如何使用 PowerShell 指令碼連線至資料庫伺服器，並將 SSIS 專案部署到 SSIS 目錄。

## <a name="powershell-script"></a>PowerShell 指令碼
為下列指令碼上方的變數提供適當的值，然後執行指令碼部署 SSIS 專案。

> [!NOTE]
> 下列範例使用 Windows 驗證。 若要使用 SQL Server 驗證，請使用 `User ID=<user name>;Password=<password>;` 取代 `Integrated Security=SSPI;` 引數。

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
