---
title: "使用 PowerShell 執行 SSIS 封裝 |Microsoft 文件"
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
ms.openlocfilehash: d392ac49442ef0f04961908fff7acf553fa1aa57
ms.contentlocale: zh-tw
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-with-powershell"></a>使用 PowerShell 執行 SSIS 封裝
本快速入門教學課程會示範如何使用 PowerShell 指令碼，若要連接到資料庫伺服器和執行 SSIS 封裝。

## <a name="powershell-script"></a>PowerShell 指令碼
在下列指令碼中，最上方的變數提供適當的值，然後執行指令碼執行 SSIS 封裝。

> [!NOTE]
> 下列範例會使用 Windows 驗證。 若要使用 SQL Server 驗證，取代`Integrated Security=SSPI;`引數與`User ID=<user name>;Password=<password>;`。

```powershell
# Variables
$SSISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"
$TargetServerName = "localhost"
$TargetFolderName = "Project1Folder"
$ProjectName = "Integration Services Project1"
$PackageName = "Package.dtsx"

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

# Get the folder
$folder = $catalog.Folders[$TargetFolderName]

# Get the project
$project = $folder.Projects[$ProjectName]

# Get the package
$package = $project.Packages[$PackageName]

Write-Host "Running " $PackageName "..."

$result = $package.Execute("false", $null)

Write-Host "Done."
```

## <a name="next-steps"></a>後續的步驟
- 考慮以其他方式來執行封裝。
    - [使用 SSMS 執行 SSIS 封裝](./ssis-quickstart-run-ssms.md)
    - [使用 TRANSACT-SQL (SSMS) 執行 SSIS 封裝](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 TRANSACT-SQL (VS Code) 中執行 SSIS 封裝](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元中執行 SSIS 封裝](./ssis-quickstart-run-cmdline.md)
    - [使用 C# 中執行 SSIS 封裝](./ssis-quickstart-run-dotnet.md) 

