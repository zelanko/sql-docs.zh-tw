---
title: 使用 .NET 程式碼部署 SSIS 專案 (C#) | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 43820f44e789330ed437c104e385090a8179a2b3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "74947109"
---
# <a name="deploy-an-ssis-project-with-c-code-in-a-net-app"></a>在 .NET 應用程式中使用 C# 程式碼部署 SSIS 專案

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本快速入門示範如何撰寫 C# 程式碼，來連線至資料庫伺服器並部署 SSIS 專案。

若要建立 C# 應用程式，您可以使用 Visual Studio、Visual Studio Code 或您選擇的另一個工具。

## <a name="prerequisites"></a>Prerequisites

開始之前，請確定已安裝 Visual Studio 或 Visual Studio Code。 從 [Visual Studio 下載](https://www.visualstudio.com/downloads/)，下載免費的 Visual Studio Community Edition 或免費的 Visual Studio Code。

Azure SQL Database 伺服器會接聽連接埠 1433。 如果您要嘗試透過公司防火牆連線至 Azure SQL Database 伺服器，則必須在公司防火牆中開啟此連接埠，讓您成功連線。

## <a name="supported-platforms"></a>支援的平台

您可以使用本快速入門中的資訊，將 SSIS 套件部署到下列平台：

-   Windows 上的 SQL Server。

-   Azure SQL Database。 如需在 Azure 中部署和執行套件的詳細資訊，請參閱[將 SQL Server Integration Services 工作負載隨即轉移至雲端](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)。

您無法使用本快速入門中的資訊，將 SSIS 套件部署到 Linux 上的 SQL Server。 如需在 Linux 上執行套件的詳細資訊，請參閱[使用 SSIS 在 Linux 上擷取、轉換和載入資料](../linux/sql-server-linux-migrate-ssis.md)。

## <a name="for-azure-sql-database-get-the-connection-info"></a>針對 Azure SQL Database，請取得連線資訊

若要將專案部署到 Azure SQL Database，請取得連線至 SSIS 目錄資料庫 (SSISDB) 所需的連線資訊。 在下列程序中，您需要完整伺服器名稱和登入資訊。

1. 登入 [Azure 入口網站](https://portal.azure.com/)。
2. 從左側功能表中選取 [SQL 資料庫]  ，然後選取 [SQL 資料庫]  頁面上的 SSISDB 資料庫。 
3. 在您資料庫的 [概觀]  頁面上，檢閱完整伺服器名稱。 若要顯示 [按一下以複製]  選項，請將滑鼠指標暫留在伺服器名稱上。 
4. 如果您忘記 Azure SQL Database 伺服器登入資訊，請巡覽至 [SQL Database 伺服器] 頁面來檢視伺服器管理員名稱。 如有需要，您可以重設密碼。
5. 按一下 [顯示資料庫連接字串]  。
6. 檢閱完整 **ADO.NET** 連接字串。 您的程式碼可以選擇性地使用 `SqlConnectionStringBuilder`，以使用您提供的個別參數值來重新建立此連接字串。

## <a name="supported-authentication-method"></a>支援的驗證方法

請參閱[適用於部署的驗證方法](ssis-quickstart-deploy-ssms.md#authentication-methods-for-deployment)。

## <a name="create-a-new-visual-studio-project"></a>建立新的 Visual Studio 專案

1. 在 Visual Studio 中，依序選擇 [檔案]  、[新增]  和 [專案]  。 
2. 在 [新增專案]  對話方塊中，展開 [Visual C#]  。
3. 選取 [主控台應用程式]  ，然後輸入 *deploy_ssis_project* 作為專案名稱。
4. 按一下 [確定]  ，在 Visual Studio 中建立和開啟新的專案。

## <a name="add-references"></a>新增參考
1. 在方案總管中，以滑鼠右鍵按一下 [參考]  資料夾，然後選取 [新增參考]  。 [參考管理員]  對話方塊隨即開啟。
2. 在 [參考管理員]  對話方塊中，展開 [組件]  ，然後選取 [延伸模組]  。
3. 選取下列兩個要新增的參考：
    -   Microsoft.SqlServer.Management.Sdk.Sfc
    -   Microsoft.SqlServer.Smo
4. 按一下 [瀏覽]  按鈕，新增 **Microsoft.SqlServer.Management.IntegrationServices** 的參考 (只會在全域組件快取 (GAC) 中安裝此組件)。[選取要參考的檔案]  對話方塊隨即開啟。
5. 在 [選取要參考的檔案]  對話方塊中，巡覽至包含組件的 GAC 資料夾。 此資料夾通常是 `C:\Windows\assembly\GAC_MSIL\Microsoft.SqlServer.Management.IntegrationServices\14.0.0.0__89845dcd8080cc91`。
6. 選取資料夾中的組件 (即 .dll 檔案)，然後按一下 [新增]  。
7. 按一下 [確定]  關閉 [參考管理員]  對話方塊，然後新增三個參考。 若要確認是否有參考，請檢查方案總管中的 [參考]  清單。

## <a name="add-the-c-code"></a>新增 C# 程式碼 
1. 開啟 **Program.cs**。

2. 將 **Program.cs** 的內容取代為下列程式碼。 新增適當的伺服器、資料庫、使用者和密碼值。

> [!NOTE]
> 下列範例使用 Windows 驗證。 若要使用 SQL Server 驗證，請使用 `User ID=<user name>;Password=<password>;` 取代 `Integrated Security=SSPI;` 引數。 如果要連線至 Azure SQL Database 伺服器，您無法使用 Windows 驗證。

```csharp
using Microsoft.SqlServer.Management.IntegrationServices;
using System;
using System.Data.SqlClient;
using System.IO;

namespace deploy_ssis_project
{
    class Program
    {
        static void Main(string[] args)
        {
            // Variables
            string targetServerName = "localhost";
            string targetFolderName = "Project1Folder";
            string projectName = "Integration Services Project1";
            string projectFilePath = @"C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac";

            // Create a connection to the server
            string sqlConnectionString = "Data Source=" + targetServerName +
                ";Initial Catalog=master;Integrated Security=SSPI;";
            SqlConnection sqlConnection = new SqlConnection(sqlConnectionString);

            // Create the Integration Services object
            IntegrationServices integrationServices = new IntegrationServices(sqlConnection);

            // Get the Integration Services catalog
            Catalog catalog = integrationServices.Catalogs["SSISDB"];

            // Create the target folder
            CatalogFolder folder = new CatalogFolder(catalog,
                targetFolderName, "Folder description");
            folder.Create();

            Console.WriteLine("Deploying " + projectName + " project.");

            byte[] projectFile = File.ReadAllBytes(projectFilePath);
            folder.DeployProject(projectName, projectFile);

            Console.WriteLine("Done.");
        }
    }
}
```

## <a name="run-the-code"></a>執行程式碼

1. 若要執行應用程式，請按 **F5**。
2. 在 SSMS 中，確認已部署專案。

## <a name="next-steps"></a>後續步驟
- 請考慮使用其他方式來部署套件。
    - [使用 SSMS 部署 SSIS 套件](./ssis-quickstart-deploy-ssms.md)
    - [使用 Transact-SQL 部署 SSIS 套件 (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [使用 Transact-SQL 部署 SSIS 套件 (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [從命令提示字元中部署 SSIS 套件](./ssis-quickstart-deploy-cmdline.md)
    - [使用 PowerShell 部署 SSIS 套件](ssis-quickstart-deploy-powershell.md)
- 執行已部署的套件。 若要執行套件，您可以從數個工具和語言進行選擇。 如需詳細資訊，請參閱下列文章：
    - [使用 SSMS 執行 SSIS 套件](./ssis-quickstart-run-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元執行 SSIS 套件](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 套件](ssis-quickstart-run-powershell.md)
    - [使用 C# 執行 SSIS 套件](./ssis-quickstart-run-dotnet.md) 
