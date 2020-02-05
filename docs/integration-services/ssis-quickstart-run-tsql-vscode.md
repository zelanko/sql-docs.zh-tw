---
title: 使用 Transact-SQL 執行 SSIS 套件 (VS Code) | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cdd1dc130efb795b957911c51d5d8c2243522d38
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71281613"
---
# <a name="run-an-ssis-package-from-visual-studio-code-with-transact-sql"></a>使用 Transact-SQL 從 Visual Studio Code 執行 SSIS 套件

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


此快速入門示範如何使用 Visual Studio Code 連線到 SSIS 目錄資料庫，然後使用 Transact-SQL 陳述式執行 SSIS 目錄中所儲存的 SSIS 套件。

Visual Studio Code 是 Windows、macOS 和 Linux 中支援延伸模組的程式碼編輯器，包含連線至 Microsoft SQL Server、Azure SQL Database 或 Azure SQL Data Warehouse 的 `mssql` 延伸模組。 如需 VS Code 的詳細資訊，請參閱 [Visual Studio Code](https://code.visualstudio.com/)。

## <a name="prerequisites"></a>Prerequisites

開始之前，請確定您已安裝最新版 Visual Studio Code 並載入 `mssql` 延伸模組。 若要下載這些工具，請參閱下列頁面：
-   [下載 Visual Studio Code](https://code.visualstudio.com/Download)
-   [mssql 延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="supported-platforms"></a>支援的平台

您可以使用本快速入門中的資訊，在下列平台上執行 SSIS 套件：

-   Windows 上的 SQL Server。

-   Azure SQL Database。 如需在 Azure 中部署和執行套件的詳細資訊，請參閱[將 SQL Server Integration Services 工作負載隨即轉移至雲端](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)。

您不能使用本快速入門中的資訊在 Linux 上執行 SSIS 套件。 如需在 Linux 上執行套件的詳細資訊，請參閱[使用 SSIS 在 Linux 上擷取、轉換和載入資料](../linux/sql-server-linux-migrate-ssis.md)。

## <a name="set-language-mode-to-sql-in-vs-code"></a>在 VS Code 中將語言模式設定為 SQL

若要啟用 `mssql` 命令和 T-SQL IntelliSense，請在 Visual Studio Code 中將語言模式設定為 [SQL]  。

1. 開啟 Visual Studio Code，然後開啟新視窗。 

2. 按一下狀態列右下角的 [純文字]  。

3. 在開啟的 [選取語言模式]  下拉式功能表中，選取或輸入 **SQL**，然後按 **ENTER** 將語言模式設定為 SQL。 

## <a name="for-azure-sql-database-get-the-connection-info"></a>針對 Azure SQL Database，請取得連線資訊

若要在 Azure SQL Database 上執行套件，請取得連線至 SSIS 目錄資料庫 (SSISDB) 所需的連線資訊。 在下列程序中，您需要完整伺服器名稱和登入資訊。

1. 登入 [Azure 入口網站](https://portal.azure.com/)。
2. 從左側功能表中選取 [SQL 資料庫]  ，然後選取 [SQL 資料庫]  頁面上的 SSISDB 資料庫。 
3. 在您資料庫的 [概觀]  頁面上，檢閱完整伺服器名稱。 若要顯示 [按一下以複製]  選項，請將滑鼠指標暫留在伺服器名稱上。 
4. 如果您忘記 Azure SQL Database 伺服器登入資訊，請巡覽至 [SQL Database 伺服器] 頁面來檢視伺服器管理員名稱。 如有需要，您可以重設密碼。

## <a name="connect-to-the-ssis-catalog-database"></a>連線至 SSIS 目錄資料庫

使用 Visual Studio Code，以建立與 SSIS 目錄的連線。

> [!IMPORTANT]
> 繼續之前，請確定您已準備好伺服器、資料庫和登入資訊。 如果您在開始輸入連線設定檔資訊之後變更 Visual Studio Code 的焦點，則必須重新開始建立連線設定檔。

1. 在 VS Code 中，按 **CTRL+SHIFT+P** (或 **F1**) 開啟 [命令選擇區]。

2. 鍵入 **sqlcon**，並按 **ENTER**。

3. 按 **ENTER** 選取 [Create Connection Profile] (建立連線設定檔)  。 此步驟會建立您 SQL Server 執行個體的連線設定檔。

4. 遵循提示來指定新連線設定檔的連線屬性。 指定每個值之後，請按 **ENTER** 繼續。 

   | 設定       | 建議的值 | 其他資訊 |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器名稱** | 完整伺服器名稱 | 如果您要連線至 Azure SQL Database 伺服器，則名稱的格式如下：`<server_name>.database.windows.net`。 |
   | **資料庫名稱** | **SSISDB** | 要連線之資料庫的名稱。 |
   | **驗證** | SQL 登入 | 使用 SQL Server 驗證時，您可以連線到 SQL Server 或 Azure SQL Database。 如果要連線至 Azure SQL Database 伺服器，您無法使用 Windows 驗證。 |
   | **使用者名稱** | 伺服器系統管理員帳戶 | 這個帳戶是您在建立伺服器時指定的帳戶。 |
   | **密碼 (SQL 登入)** | 伺服器系統管理員帳戶的密碼 | 這個密碼是您在建立伺服器時指定的密碼。 |
   | **儲存密碼嗎？** | [是] 或 [否] | 如果您不想要每次都輸入密碼，請選取 [是]。 |
   | **輸入此設定檔的名稱** | 設定檔名稱，例如 **mySSISServer** | 儲存的設定檔名稱可在後續的登入中加速您的連線。 | 

5. 按 **ESC** 鍵關閉資訊訊息，通知您已建立並連線設定檔。

6. 在狀態列中確認您的連線。

## <a name="run-the-t-sql-code"></a>執行 T-SQL 程式碼
執行下列 Transact-SQL 程式碼來執行 SSIS 套件。

1. 在 [編輯器]  視窗中，於空白查詢視窗中輸入下列查詢 (此程式碼是 SSMS 中 [執行套件]  對話方塊的 [指令碼]  選項所產生的程式碼。)

2. 更新 `catalog.create_execution` 預存程序中您系統的參數值。

3. 按 **CTRL+SHIFT+E** 執行程式碼，並執行套件。

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

## <a name="next-steps"></a>後續步驟
- 請考慮使用其他方式來執行套件。
    - [使用 SSMS 執行 SSIS 套件](./ssis-quickstart-run-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [從命令提示字元執行 SSIS 套件](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 套件](ssis-quickstart-run-powershell.md)
    - [使用 C# 執行 SSIS 套件](./ssis-quickstart-run-dotnet.md) 
