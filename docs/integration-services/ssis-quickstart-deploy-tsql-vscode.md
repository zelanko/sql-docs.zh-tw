---
title: 使用 Transact-SQL 部署 SSIS 專案 (VS Code) | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: af19358906b70cad15103913eebf45507f449410
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921827"
---
# <a name="deploy-an-ssis-project-from-visual-studio-code-with-transact-sql"></a>使用 Transact-SQL 從 Visual Studio Code 部署 SSIS 專案

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


此快速入門示範如何使用 Visual Studio Code 連線至 SSIS 目錄資料庫，然後使用 Transact-SQL 陳述式將 SSIS 專案部署至 SSIS 目錄。

Visual Studio Code 是 Windows、macOS 和 Linux 中支援延伸模組的程式碼編輯器，包含連線至 Microsoft SQL Server、Azure SQL Database 或 Azure SQL Data Warehouse 的 `mssql` 延伸模組。 如需 VS Code 的詳細資訊，請參閱 [Visual Studio Code](https://code.visualstudio.com/)。

## <a name="prerequisites"></a>Prerequisites

開始之前，請確定您已安裝最新版 Visual Studio Code 並載入 `mssql` 延伸模組。 若要下載這些工具，請參閱下列頁面：
-   [下載 Visual Studio Code](https://code.visualstudio.com/Download)
-   [mssql 延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="supported-platforms"></a>支援的平台

您可以使用本快速入門中的資訊，將 SSIS 套件部署到下列平台：

-   Windows 上的 SQL Server。

您無法使用本快速入門中的資訊，將 SSIS 套件部署到 Azure SQL Database。 `catalog.deploy_project` 預存程序必須有本機 (內部部署) 檔案系統中 `.ispac` 檔案的路徑。 如需在 Azure 中部署和執行套件的詳細資訊，請參閱[將 SQL Server Integration Services 工作負載隨即轉移至雲端](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)。

您無法使用本快速入門中的資訊，將 SSIS 套件部署到 Linux 上的 SQL Server。 如需在 Linux 上執行套件的詳細資訊，請參閱[使用 SSIS 在 Linux 上擷取、轉換和載入資料](../linux/sql-server-linux-migrate-ssis.md)。

## <a name="set-language-mode-to-sql-in-vs-code"></a>在 VS Code 中將語言模式設定為 SQL

若要啟用 `mssql` 命令和 T-SQL IntelliSense，請在 Visual Studio Code 中將語言模式設定為 [SQL]  。

1. 開啟 Visual Studio Code，然後開啟新視窗。 

2. 按一下狀態列右下角的 [純文字]  。
 
3. 在開啟的 [選取語言模式]  下拉式功能表中，選取或輸入 **SQL**，然後按 **ENTER** 將語言模式設定為 SQL。 

## <a name="supported-authentication-method"></a>支援的驗證方法

請參閱[適用於部署的驗證方法](ssis-quickstart-deploy-ssms.md#authentication-methods-for-deployment)。

## <a name="connect-to-the-ssis-catalog-database"></a>連線至 SSIS 目錄資料庫

使用 Visual Studio Code，以建立與 SSIS 目錄的連線。

1. 在 VS Code 中，按 **CTRL+SHIFT+P** (或 **F1**) 開啟 [命令選擇區]。

2. 鍵入 **sqlcon**，並按 **ENTER**。

3. 按 **ENTER** 選取 [Create Connection Profile] (建立連線設定檔)  。 此步驟會建立您 SQL Server 執行個體的連線設定檔。

4. 遵循提示來指定新連線設定檔的連線屬性。 指定每個值之後，請按 **ENTER** 繼續。 

   | 設定       | 建議的值 | 其他資訊 |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器名稱** | 完整伺服器名稱 |  |
   | **資料庫名稱** | **SSISDB** | 要連線之資料庫的名稱。 |
   | **驗證** | SQL 登入 | |
   | **使用者名稱** | 伺服器系統管理員帳戶 | 這個帳戶是您在建立伺服器時指定的帳戶。 |
   | **密碼 (SQL 登入)** | 伺服器系統管理員帳戶的密碼 | 這個密碼是您在建立伺服器時指定的密碼。 |
   | **儲存密碼嗎？** | [是] 或 [否] | 如果您不想要每次都輸入密碼，請選取 [是]。 |
   | **輸入此設定檔的名稱** | 設定檔名稱，例如 **mySSISServer** | 儲存的設定檔名稱可在後續的登入中加速您的連線。 | 

5. 按 **ESC** 鍵關閉資訊訊息，通知您已建立並連線設定檔。

6. 在狀態列中確認您的連線。

## <a name="run-the-t-sql-code"></a>執行 T-SQL 程式碼
執行下列 Transact-SQL 程式碼來部署 SSIS 專案。

1. 在 [編輯器]  視窗中，於空白查詢視窗中輸入下列查詢

2. 更新 `catalog.deploy_project` 預存程序中您系統的參數值。

3. 按 **CTRL+SHIFT+E** 執行程式碼，並部署專案。

```sql
DECLARE @ProjectBinary AS varbinary(max)
DECLARE @operation_id AS bigint
SET @ProjectBinary = (SELECT * FROM OPENROWSET(BULK '<project_file_path>.ispac', SINGLE_BLOB) AS BinaryData)

EXEC catalog.deploy_project @folder_name = '<target_folder>',
    @project_name = '<project_name',
    @Project_Stream = @ProjectBinary,
    @operation_id = @operation_id out
```

## <a name="next-steps"></a>後續步驟
- 請考慮使用其他方式來部署套件。
    - [使用 SSMS 部署 SSIS 套件](./ssis-quickstart-deploy-ssms.md)
    - [使用 Transact-SQL 部署 SSIS 套件 (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [從命令提示字元中部署 SSIS 套件](./ssis-quickstart-deploy-cmdline.md)
    - [使用 PowerShell 部署 SSIS 套件](ssis-quickstart-deploy-powershell.md)
    - [使用 C# 部署 SSIS 套件](./ssis-quickstart-deploy-dotnet.md) 
- 執行已部署的套件。 若要執行套件，您可以從數個工具和語言進行選擇。 如需詳細資訊，請參閱下列文章：
    - [使用 SSMS 執行 SSIS 套件](./ssis-quickstart-run-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元執行 SSIS 套件](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 套件](ssis-quickstart-run-powershell.md)
    - [使用 C# 執行 SSIS 套件](./ssis-quickstart-run-dotnet.md) 
