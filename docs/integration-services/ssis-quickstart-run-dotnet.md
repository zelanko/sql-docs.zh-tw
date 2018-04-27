---
title: 使用 .NET 程式碼執行 SSIS 專案 (C#) | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: quick-start
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82e928aed1c5d460ff03332912e670582434fbad
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="run-an-ssis-package-with-c-code-in-a-net-app"></a>在 .NET 應用程式中使用 C# 程式碼執行 SSIS 套件
本快速入門教學課程示範如何撰寫 C# 程式碼，來連線至資料庫伺服器並執行 SSIS 套件。

您可以使用 Visual Studio、Visual Studio Code 或您選擇的另一個工具，來建立 C# 應用程式。

## <a name="prerequisites"></a>Prerequisites

開始之前，請確定已安裝 Visual Studio 或 Visual Studio Code。 從 [Visual Studio 下載](https://www.visualstudio.com/downloads/)，下載免費的 Visual Studio Community Edition 或免費的 Visual Studio Code。

> [!NOTE]
> Azure SQL Database 伺服器會接聽連接埠 1433。 如果您要嘗試透過公司防火牆連線至 Azure SQL Database 伺服器，則必須在公司防火牆中開啟此連線埠，讓您成功連線。

## <a name="get-the-connection-info-if-deployed-to-sql-database"></a>取得部署至 SQL Database 時的連線資訊

如果您的套件是部署至 Azure SQL Database，請取得連線至 SSIS 目錄資料庫 (SSISDB) 所需的連線資料。 在下列程序中，您需要完整伺服器名稱和登入資訊。

1. 登入 [Azure 入口網站](https://portal.azure.com/)。
2. 從左側功能表中選取 [SQL 資料庫]，然後按一下 [SQL 資料庫] 頁面上的 SSISDB 資料庫。 
3. 在您資料庫的 [概觀] 頁面上，檢閱完整伺服器名稱。 若要啟動 [按一下以複製] 選項，請將滑鼠指標放在伺服器名稱上方。 
4. 如果您忘記 Azure SQL Database 伺服器登入資訊，請巡覽至 [SQL Database 伺服器] 頁面來檢視伺服器管理員名稱。 如有需要，您可以重設密碼。
5. 按一下 [顯示資料庫連接字串]。
6. 檢閱完整 **ADO.NET** 連接字串。 範例程式碼使用 `SqlConnectionStringBuilder`，以使用您提供的個別參數值來重新建立此連接字串。

## <a name="create-a-new-visual-studio-project"></a>建立新的 Visual Studio 專案

1. 在 Visual Studio 中，依序選擇 [檔案]、[新增] 和 [專案]。 
2. 在 [新增專案] 對話方塊中，展開 [Visual C#]。
3. 選取 [主控台應用程式]，然後輸入 *run_ssis_project* 作為專案名稱。
4. 按一下 [確定]，在 Visual Studio 中建立和開啟新的專案。

## <a name="add-references"></a>新增參考
1. 在方案總管中，以滑鼠右鍵按一下 [參考] 資料夾，然後選取 [新增參考]。 [參考管理員] 對話方塊隨即開啟。
2. 在 [參考管理員] 對話方塊中，展開 [組件]，然後選取 [延伸模組]。
3. 選取下列兩個要新增的參考：
    -   Microsoft.SqlServer.Management.Sdk.Sfc
    -   Microsoft.SqlServer.Smo
4. 按一下 [瀏覽] 按鈕，新增 **Microsoft.SqlServer.Management.IntegrationServices** 的參考  (只會在全域組件快取 (GAC) 中安裝此組件)。[選取要參考的檔案] 對話方塊隨即開啟。
5. 在 [選取要參考的檔案] 對話方塊中，巡覽至包含組件的 GAC 資料夾。 此資料夾通常是 `C:\Windows\assembly\GAC_MSIL\Microsoft.SqlServer.Management.IntegrationServices\14.0.0.0__89845dcd8080cc91`。
6. 選取資料夾中的組件 (即 .dll 檔案)，然後按一下 [新增]。
7. 按一下 [確定] 關閉 [參考管理員] 對話方塊，然後新增三個參考。 若要確認是否有參考，請檢查方案總管中的 [參考] 清單。

## <a name="add-the-c-code"></a>新增 C# 程式碼 
1. 開啟 **Program.cs**。

2. 將 **Program.cs** 的內容取代為下列程式碼。 新增適當的伺服器、資料庫、使用者和密碼值。

> [!NOTE]
> 下列範例使用 Windows 驗證。 若要使用 SQL Server 驗證，請將 `Integrated Security=SSPI;` 引數取代為 `User ID=<user name>;Password=<password>;`。


```csharp
using Microsoft.SqlServer.Management.IntegrationServices;
using System.Data.SqlClient;

namespace run_ssis_package
{
    class Program
    {
        static void Main(string[] args)
        {
            // Variables
            string targetServerName = "localhost";
            string folderName = "Project1Folder";
            string projectName = "Integration Services Project1";
            string packageName = "Package.dtsx";

            // Create a connection to the server
            string sqlConnectionString = "Data Source=" + targetServerName +
                ";Initial Catalog=master;Integrated Security=SSPI;";
            SqlConnection sqlConnection = new SqlConnection(sqlConnectionString);

            // Create the Integration Services object
            IntegrationServices integrationServices = new IntegrationServices(sqlConnection);

            // Get the Integration Services catalog
            Catalog catalog = integrationServices.Catalogs["SSISDB"];

            // Get the folder
            CatalogFolder folder = catalog.Folders[folderName];

            // Get the project
            ProjectInfo project = folder.Projects[projectName];

            // Get the package
            PackageInfo package = project.Packages[packageName];

            // Run the package
            package.Execute(false, null);

        }
    }
}
```

## <a name="run-the-code"></a>執行程式碼

1. 若要執行應用程式，請按 **F5**。
2. 確認套件已如預期般執行，然後關閉應用程式視窗。

## <a name="next-steps"></a>後續步驟
- 請考慮使用其他方式來執行套件。
    - [使用 SSMS 執行 SSIS 套件](./ssis-quickstart-run-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元中執行 SSIS 套件](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 套件](ssis-quickstart-run-powershell.md)
