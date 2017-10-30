---
title: "SSIS 專案部署使用 PowerShell |Microsoft 文件"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: 37fe358eb7e11cb878ebd9b0c8356ac2295ca7e9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-with-powershell"></a>SSIS 專案部署使用 PowerShell
本快速入門教學課程會示範如何使用 PowerShell 指令碼連接至資料庫伺服器，並將 SSIS 專案部署至 SSIS 目錄。

## <a name="powershell-script"></a>PowerShell 指令碼
在下列指令碼中，最上方的變數提供適當的值，然後執行 將 SSIS 專案部署指令碼。

> [!NOTE]
> 下列範例會使用 Windows 驗證。 若要使用 SQL Server 驗證，取代`Integrated Security=SSPI;`引數與`User ID=<user name>;Password=<password>;`。

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

## <a name="next-steps"></a>後續的步驟
- 考慮以其他方式來部署封裝。
    - [部署 SSIS 封裝使用 SSMS](./ssis-quickstart-deploy-ssms.md)
    - [部署 SSIS 封裝使用 TRANSACT-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [部署 SSIS 封裝使用 TRANSACT-SQL (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [部署 SSIS 封裝從命令提示字元](./ssis-quickstart-deploy-cmdline.md)
    - [部署使用 C# 的 SSIS 封裝](./ssis-quickstart-deploy-dotnet.md) 
- 執行部署的封裝。 若要執行封裝，您可以選擇從數個工具和語言。 如需詳細資訊，請參閱下列文章：
    - [使用 SSMS 執行 SSIS 封裝](./ssis-quickstart-run-ssms.md)
    - [使用 TRANSACT-SQL (SSMS) 執行 SSIS 封裝](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 TRANSACT-SQL (VS Code) 中執行 SSIS 封裝](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元中執行 SSIS 封裝](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 封裝](ssis-quickstart-run-powershell.md)
    - [使用 C# 中執行 SSIS 封裝](./ssis-quickstart-run-dotnet.md) 

