---
title: 使用 Transact-SQL 執行 SSIS 套件 (SSMS) | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 56e3cb535570c768b1a7db6b55c439e1fb3be74e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654356"
---
# <a name="run-an-ssis-package-from-ssms-with-transact-sql"></a>使用 Transact-SQL 從 SSMS 執行 SSIS 套件
本快速入門示範如何使用 SQL Server Management Studio (SSMS) 連線到 SSIS 目錄資料庫，然後使用 Transact-SQL 陳述式來執行儲存在 SSIS 目錄的 SSIS 套件。

SQL Server Management Studio 是整合式環境，用於管理任何 SQL 基礎結構，從 SQL Sever 到 SQL Database 皆適用。 如需 SSMS 的詳細資訊，請參閱 [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)。

## <a name="prerequisites"></a>Prerequisites

開始之前，請確定您有最新版的 SQL Server Management Studio (SSMS)。 若要下載 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

Azure SQL Database 伺服器會接聽連接埠 1433。 如果您要嘗試透過公司防火牆連線至 Azure SQL Database 伺服器，則必須在公司防火牆中開啟此連接埠，讓您成功連線。

## <a name="supported-platforms"></a>支援的平台

您可以使用本快速入門中的資訊，在下列平台上執行 SSIS 套件：

-   Windows 上的 SQL Server。

-   Azure SQL Database。 如需在 Azure 部署和執行套件的詳細資訊，請參閱[將 SQL Server Integration Services 工作負載隨即轉移至雲端](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)。

您不能使用本快速入門中的資訊在 Linux 上執行 SSIS 套件。 如需在 Linux 上執行套件的詳細資訊，請參閱[使用 SSIS 在 Linux 上擷取、轉換和載入資料](../linux/sql-server-linux-migrate-ssis.md)。

## <a name="for-azure-sql-database-get-the-connection-info"></a>針對 Azure SQL Database，請取得連線資訊

若要在 Azure SQL Database 上執行套件，請取得連線至 SSIS 目錄資料庫 (SSISDB) 所需的連線資訊。 在下列程序中，您需要完整伺服器名稱和登入資訊。

1. 登入 [Azure 入口網站](https://portal.azure.com/)。
2. 從左側功能表中選取 [SQL 資料庫]，然後選取 [SQL 資料庫] 頁面上的 SSISDB 資料庫。 
3. 在您資料庫的 [概觀] 頁面上，檢閱完整伺服器名稱。 若要顯示 [按一下以複製] 選項，請將滑鼠指標暫留在伺服器名稱上。 
4. 如果您忘記 Azure SQL Database 伺服器登入資訊，請巡覽至 [SQL Database 伺服器] 頁面來檢視伺服器管理員名稱。 如有需要，您可以重設密碼。

## <a name="connect-to-the-ssisdb-database"></a>連線至 SSISDB 資料庫

使用 SQL Server Management Studio，以建立與 Azure SQL Database 伺服器之 SSIS 目錄的連線。 

1. 開啟 SQL Server Management Studio。

2. 在 [連線至伺服器] 對話方塊中，輸入下列資訊：

   | 設定       | 建議值 | 其他資訊 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器類型** | 資料庫引擎 | 這是必要的值。 |
   | **伺服器名稱** | 完整伺服器名稱 | 如果您要連線至 Azure SQL Database 伺服器，則名稱的格式如下：`<server_name>.database.windows.net`。 |
   | **驗證** | SQL Server 驗證 | 使用 SQL Server 驗證時，您可以連線到 SQL Server 或 Azure SQL Database。 如果要連線至 Azure SQL Database 伺服器，您無法使用 Windows 驗證。 |
   | **登入** | 伺服器系統管理員帳戶 | 這個帳戶是您在建立伺服器時指定的帳戶。 |
   | **密碼** | 伺服器系統管理員帳戶的密碼 | 這個密碼是您在建立伺服器時指定的密碼。 |

3.  按一下 **[連接]**。 [物件總管] 視窗會在 SSMS 中開啟。

4. 在 [物件總管] 中，展開 [Integration Services 目錄]，然後展開 [SSISDB] 以檢視 SSIS 目錄資料庫中的物件。

## <a name="run-a-package"></a>執行套件
執行下列 Transact-SQL 程式碼來執行 SSIS 套件。

1.  在 SSMS 中，開啟新的查詢視窗，並貼入下列程式碼。 (此程式碼是 SSMS 中 [執行套件] 對話方塊的 [指令碼] 選項所產生的程式碼。)

2.  更新 `catalog.create_execution` 預存程序中您系統的參數值。

3.  確定 SSISDB 是目前的資料庫。

4.  執行指令碼。

5. 在 [物件總管] 中，於必要時更新 **SSISDB** 的內容，然後檢查是否有您所部署的專案。

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
    - [使用 Transact-SQL 執行 SSIS 套件 (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元中執行 SSIS 套件](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 套件](ssis-quickstart-run-powershell.md)
    - [使用 C# 執行 SSIS 套件](./ssis-quickstart-run-dotnet.md) 
