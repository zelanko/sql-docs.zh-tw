---
title: "使用 TRANSACT-SQL (VS Code) 中執行 SSIS 封裝 |Microsoft 文件"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: a912bf7f7944d4af3d41c5596e67aa77f3214112
ms.contentlocale: zh-tw
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-visual-studio-code-with-transact-sql"></a>從 Visual Studio 程式碼，以 TRANSACT-SQL 執行 SSIS 封裝
本快速入門示範如何連接到 SSIS 目錄資料庫，並接著使用 TRANSACT-SQL 陳述式執行 SSIS 封裝儲存在 SSIS 目錄中使用 Visual Studio 程式碼。

Visual Studio 程式碼是程式碼編輯器視窗、 macOS，及可支援擴充功能，包括 Linux`mssql`延伸模組連接到 Microsoft SQL Server、 Azure SQL Database 或 Azure SQL 資料倉儲。 如需 VS 程式碼的詳細資訊，請參閱[Visual Studio Cod](https://code.visualstudio.com/)。

## <a name="prerequisites"></a>必要條件

開始之前，請確定您已安裝最新版的 Visual Studio 程式碼並載入`mssql`延伸模組。 若要下載這些工具，請參閱下列頁面：
-   [下載 Visual Studio Code](https://code.visualstudio.com/Download)
-   [mssql 延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="set-language-mode-to-sql-in-vs-code"></a>將語言模式設定為與程式碼中的 SQL

若要啟用`mssql`組語言模式命令和 T-SQL IntelliSense，設定為**SQL** Visual Studio 程式碼中。

1. 開啟 Visual Studio 程式碼，然後開啟 新的視窗。 

2. 按一下**純文字**右下角的 [狀態] 列中。

3. 在**選取的語言模式**下拉式選單，隨即開啟，請選取或輸入**SQL**，然後按下**ENTER**設為 SQL 的語言模式。 

## <a name="connect-to-the-ssis-catalog-database"></a>連接到 SSIS 目錄資料庫

您可以使用 Visual Studio 程式碼來連接到 SSIS 目錄。

> [!IMPORTANT]
> 在繼續之前，請確定您有您的伺服器、 資料庫和登入資訊就緒。 如果在您開始輸入連線設定檔資訊後，您可以變更從 Visual Studio 程式碼的焦點，您必須重新啟動 建立連線設定檔。

1. 在 VS Code 按**CTRL + SHIFT + P** (或**F1**) 若要開啟命令選擇區。

2. 型別**sqlcon**按**ENTER**。

3. 按**ENTER**選取**建立連線設定檔**。 這個步驟會建立您的 SQL Server 執行個體的連線設定檔。

4. 遵循提示來指定新的連線設定檔的連接屬性。 指定每個值之後, 按**ENTER**才能繼續。 

   | 設定       | 建議的值 | 其他資訊 |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器名稱** | 完整的伺服器名稱 | 如果您要連線至 Azure SQL Database 伺服器，則名稱是以下列格式： `<server_name>.database.windows.net`。 |
   | **資料庫名稱** | **SSISDB** | 要用來連接的資料庫名稱。 |
   | **驗證** | SQL 登入| 本快速入門使用 SQL 驗證。 |
   | **使用者名稱** | 伺服器系統管理員帳戶 | 這是您在建立伺服器時指定的帳戶。 |
   | **密碼 （SQL 登入）** | 伺服器系統管理員帳戶密碼 | 這是您在建立伺服器時指定的密碼。 |
   | **儲存密碼嗎？** | [是] 或 [否] | 如果您不想每次輸入的密碼，選取 [是]。 |
   | **輸入此設定檔的名稱** | 設定檔名稱，例如**mySSISServer** | 儲存的設定檔名稱會加速您的連線後續登入。 | 

5. 按**ESC**鍵來關閉資訊訊息，通知您已建立設定檔，並連接。

6. 請確認您在 [狀態] 列中的連線。

## <a name="run-the-t-sql-code"></a>執行 T-SQL 程式碼
執行下列 TRANSACT-SQL 程式碼執行 SSIS 封裝。

1. 在**編輯器**視窗中，輸入下列查詢在空白查詢視窗中。 (此程式碼是產生的程式碼**指令碼**選項**執行封裝**在 SSMS 中的對話方塊。)

2. 更新中的參數值`catalog.create_execution`預存程序，為您的系統。

3. 按**CTRL + SHIFT + E**執行程式碼，並執行封裝。

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx',
    @execution_id=@execution_id OUTPUT,
    @folder_name=N'Deployed Projects',
      @project_name=N'Integration Services Project1',
    @use32bitruntime=False,
      @reference_id=Null
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,
    @object_type=50,
      @parameter_name=N'LOGGING_LEVEL',
      @parameter_value=@var0
EXEC [SSISDB].[catalog].[start_execution] @execution_id
GO
```

## <a name="next-steps"></a>後續的步驟
- 考慮以其他方式來執行封裝。
    - [使用 SSMS 執行 SSIS 封裝](./ssis-quickstart-run-ssms.md)
    - [使用 TRANSACT-SQL (SSMS) 執行 SSIS 封裝](./ssis-quickstart-run-tsql-ssms.md)
    - [從命令提示字元中執行 SSIS 封裝](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 封裝](ssis-quickstart-run-powershell.md)
    - [使用 C# 中執行 SSIS 封裝](./ssis-quickstart-run-dotnet.md) 

