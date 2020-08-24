---
title: 從命令列建置專案
description: 從命令列建置 SQL Server 資料庫專案
ms.custom: seodec18
ms.date: 08/07/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: ec3c9224e0cf93ae24ba1a4858b0299f7b303076
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180699"
---
# <a name="build-a-database-project-from-command-line"></a>從命令列建置資料庫專案

儘管適用於 Azure Data Studio 的 SQL 資料庫專案延伸模組會提供圖形化使用者介面來[建置資料庫專案](sql-database-project-extension-build.md)，但也可針對 Windows、macOS 與 Linux 環境使用命令列建置體驗。 此文章概述從命令列建置 SQL 專案以進行 dacpac 所需的先決條件與語法。

## <a name="prerequisites"></a>必要條件
1. 安裝並設定[適用於 Azure Data Studio 的 SQL 資料庫專案延伸模組](sql-database-project-extension.md)。

2. 需要有下列 .NET Core dll 與目標檔案 `Microsoft.Data.Tools.Schema.SqlTasts.targets`，才能在適用於 SQL 資料庫專案之 Azure Data Studio 延伸模組所支援的所有平台中，從命令列建置 SQL 資料庫專案。 這些檔案是在 Azure Data Studio 介面中完成的第一個組建期間由延伸模組所建立，並放置於 `BuildDirectory` 之下延伸模組的資料夾中。  例如，在 Linux 上，這些檔案會放置於 `~\.azuredatastudio\extensions\microsoft.sql-database-projects-x.x.x\BuildDirectory\` 中。  將這 10 個檔案複製到可存取的新資料夾，或記下其位置。  在此文件中，此位置將稱為 `DotNet Core build folder`。
- Microsoft.Data.Tools.Schema.Sql.dll

- Microsoft.Data.Tools.Schema.Tasks.Sql.dll

- Microsoft.Data.Tools.Utilities.dll 

- Microsoft.SqlServer.Dac.dll 

- Microsoft.SqlServer.Dac.Extensions.dll 

- Microsoft.SqlServer.TransactSql.ScriptDom.dll 

- Microsoft.SqlServer.Types.dll 

- Microsoft.Data.Tools.Schema.SqlTasks.targets 

- System.ComponentModel.Composition.dll 

- Microsoft.Data.SqlClient.dll 


3. 如果專案在 Azure Data Studio 中建立的，請直接跳到[從命令列建置專案](#build-the-project-from-the-command-line)。 如果專案是在 SQL Server Data Tools (SSDT) 中建立的，則在 Azure Data Studio SQL 資料庫專案延伸模組中開啟專案。  在 Azure Data Studio 中開啟專案，即會自動更新包含三個編輯的 `sqlproj` 檔案，如下所示：
    1. 匯入條件 
    ```
    <Import Condition="'$(NetCoreBuild)' == 'true'" Project="$(NETCoreTargetsPath)\Microsoft.Data.Tools.Schema.SqlTasks.targets"/> 
    <Import Condition="'$(NetCoreBuild)' != 'true' AND '$(SQLDBExtensionsRefPath)' != ''" Project="$(SQLDBExtensionsRefPath)\Microsoft.Data.Tools.Schema.SqlTasks.targets"/> 
    <Import Condition="'$(NetCoreBuild)' != 'true' AND '$(SQLDBExtensionsRefPath)' == ''" Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets"/> 
    ```
    2. 套件參考
    ```
    <ItemGroup> 
        <PackageReference Condition="'$(NetCoreBuild)' == 'true'" Include="Microsoft.NETFramework.ReferenceAssemblies" Version="1.0.0" PrivateAssets="All"/> 
    </ItemGroup> 
    ```
    3. 清除在 SQL Server Data Tools (SSDT) 與 Azure Data Studio 中支援雙重編輯所需的目標
    ```
    <Target Name="AfterClean"> 
        <Delete Files="$(BaseIntermediateOutputPath)\project.assets.json"/> 
    </Target> 
    ```

## <a name="build-the-project-from-the-command-line"></a>從命令列建置專案
從完整的 .NET 資料夾中，使用下列命令：
```
dotnet build "<sqlproj file path>" /p:NetCoreBuild=true /p:NETCoreTargetsPath="<DotNet Core build folder>"
```
例如，從 Linux 上的 `/usr/share/dotnet`：
```
dotnet build "/home/myuser/Documents/DatabaseProject1/DatabaseProject1.sqlproj" /p:NetCoreBuild=true /p:NETCoreTargetsPath="/home/myuser/.azuredatastudio-insiders/extensions/microsoft.sql-database-projects-0.1.2/BuildDirectory"  
```
## <a name="next-steps"></a>後續步驟

- [適用於 Azure Data Studio 的 SQL 資料庫專案延伸模組](sql-database-project-extension.md)
- [發佈 SQL 資料庫專案](sql-database-project-extension-build.md#publish-a-database-project)
