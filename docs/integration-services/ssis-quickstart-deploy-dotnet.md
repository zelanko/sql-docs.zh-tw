---
title: "SSIS 專案部署以.NET 程式碼 (C#) |Microsoft 文件"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: c83ad5be88951b92c59a7517ed2676ff30692d02
ms.contentlocale: zh-tw
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-with-c-code-in-a-net-app"></a>SSIS 專案部署.NET 應用程式中的 C# 程式碼
本快速入門教學課程會示範如何撰寫 C# 程式碼以連接到資料庫伺服器和部署 SSIS 專案。

若要建立 C# 應用程式，您可以使用 Visual Studio、 Visual Studio 程式碼或您選擇的另一個工具。

## <a name="prerequisites"></a>必要條件

開始之前，請確定您有 Visual Studio，或安裝 Visual Studio 程式碼。 從下載免費的 Community 版本的 Visual Studio 中或免費的 Visual Studio Code， [Visual Studio 下載](https://www.visualstudio.com/downloads/)。

> [!NOTE]
> Azure SQL Database 伺服器通訊埠 1433年上接聽。 如果您嘗試連接到 Azure SQL Database 伺服器從公司防火牆內，此連接埠必須開啟在公司防火牆中針對您已成功連接。

## <a name="get-the-connection-info-if-deployed-to-sql-database"></a>如果部署到 SQL Database，取得的連接資訊 

如果您的封裝部署到 Azure SQL Database，取得您需要連接到 SSIS 目錄資料庫 (SSISDB) 的連接資訊。 您需要完整的伺服器名稱和登入資訊，請依照下列程序中。

1. 登入 [Azure 入口網站](https://portal.azure.com/)。
2. 選取**SQL 資料庫**SSISDB 資料庫按一下左側功能表中，與**SQL 資料庫**頁面。 
3. 在**概觀**為您的資料庫頁面上，檢閱完整的伺服器名稱。 若要啟動**按一下以複製**選項時，暫留在 伺服器名稱。 
4. 如果您忘記您的 Azure SQL Database 伺服器登入資訊時，瀏覽至 [SQL 資料庫伺服器] 頁面來檢視伺服器管理員的名稱。 如有必要，您可以重設密碼。
5. 按一下**顯示資料庫的連接字串**。
6. 檢閱完整**ADO.NET**連接字串。 範例程式碼使用`SqlConnectionStringBuilder`重新建立此連接字串，使用您提供個別的參數值。

## <a name="create-a-new-visual-studio-project"></a>建立新的 Visual Studio 專案

1. 在 Visual Studio 中，選擇 **檔案**，**新增**，**專案**。 
2. 在**新專案** 對話方塊中，展開**Visual C#**。
3. 選取**主控台應用程式**輸入*deploy_ssis_project*針對專案名稱。
4. 按一下**確定**建立與 Visual Studio 中開啟新的專案。

## <a name="add-references"></a>加入參考
1. 在 [方案總管] 中，以滑鼠右鍵按一下**參考**資料夾，然後選取**加入參考**。 **參考管理員**對話方塊隨即開啟。
2. 在**參考管理員**對話方塊方塊中，展開 **組件**選取**延伸**。
3. 選取要新增的下列兩個參考：
    -   Microsoft.SqlServer.Management.Sdk.Sfc
    -   Microsoft.SqlServer.Smo
4. 按一下**瀏覽** 按鈕，將參考加入**Microsoft.SqlServer.Management.IntegrationServices**。 （這個組件只能在全域組件快取 (GAC) 中安裝）。**選取要參考的檔案**對話方塊隨即開啟。
5. 在**選取要參考的檔案**對話方塊方塊中，瀏覽至 GAC 資料夾包含組件。 這個資料夾通常是`C:\Windows\assembly\GAC_MSIL\Microsoft.SqlServer.Management.IntegrationServices\14.0.0.0__89845dcd8080cc91`。
6. 選取組件 （也就是.dll 檔案） 中的資料夾，然後按一下**新增**。
7. 按一下**確定**關閉**參考管理員**對話方塊方塊中，並加入三個參考。 若要確認是否有參考，請檢查**參考**方案總管 中的清單。

## <a name="add-the-c-code"></a>加入 C# 程式碼 
1. 開啟**Program.cs**。

2. 取代內容**Program.cs**為下列程式碼。 新增適當的伺服器、 資料庫、 使用者和密碼值。

> [!NOTE]
> 下列範例會使用 Windows 驗證。 若要使用 SQL Server 驗證，取代`Integrated Security=SSPI;`引數與`User ID=<user name>;Password=<password>;`。

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

1. 若要執行應用程式，請按**F5**。
2. 在 SSMS 中，確認已部署專案。

## <a name="next-steps"></a>後續的步驟
- 考慮以其他方式來部署封裝。
    - [部署 SSIS 封裝使用 SSMS](./ssis-quickstart-deploy-ssms.md)
    - [部署 SSIS 封裝使用 TRANSACT-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [部署 SSIS 封裝使用 TRANSACT-SQL (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [部署 SSIS 封裝從命令提示字元](./ssis-quickstart-deploy-cmdline.md)
    - [部署 SSIS 封裝使用 PowerShell](ssis-quickstart-deploy-powershell.md)
- 執行部署的封裝。 若要執行封裝，您可以選擇從數個工具和語言。 如需詳細資訊，請參閱下列文章：
    - [使用 SSMS 執行 SSIS 封裝](./ssis-quickstart-run-ssms.md)
    - [使用 TRANSACT-SQL (SSMS) 執行 SSIS 封裝](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 TRANSACT-SQL (VS Code) 中執行 SSIS 封裝](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元中執行 SSIS 封裝](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 封裝](ssis-quickstart-run-powershell.md)
    - [使用 C# 中執行 SSIS 封裝](./ssis-quickstart-run-dotnet.md) 

