---
description: 使用 SQL Server Management Studio (SSMS) 執行 SSIS 套件
title: 使用 SSMS 執行 SSIS 套件 | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: beb9a1e1dcb25f42e2d9a49c1e0e5c1a77a3f0ea
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193058"
---
# <a name="run-an-ssis-package-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 執行 SSIS 套件

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


本快速入門示範如何使用 SQL Server Management Studio (SSMS) 連線至 SSIS 目錄資料庫，然後從 SSMS 的 [物件總管] 中執行儲存在 SSIS 目錄中的 SSIS 套件。

SQL Server Management Studio 是整合式環境，用於管理任何 SQL 基礎結構，從 SQL Sever 到 SQL Database 皆適用。 如需 SSMS 的詳細資訊，請參閱 [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)。

## <a name="prerequisites"></a>必要條件

開始之前，請確定您有最新版的 SQL Server Management Studio (SSMS)。 若要下載 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)。

Azure SQL Database 伺服器會接聽連接埠 1433。 如果您要嘗試透過公司防火牆連線至 Azure SQL Database 伺服器，則必須在公司防火牆中開啟此連接埠，讓您成功連線。

## <a name="supported-platforms"></a>支援的平台

您可以使用本快速入門中的資訊，在下列平台上執行 SSIS 套件：

-   Windows 上的 SQL Server。

-   Azure SQL Database。 如需在 Azure 中部署和執行套件的詳細資訊，請參閱[將 SQL Server Integration Services 工作負載隨即轉移至雲端](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)。

您不能使用本快速入門中的資訊在 Linux 上執行 SSIS 套件。 如需在 Linux 上執行套件的詳細資訊，請參閱[使用 SSIS 在 Linux 上擷取、轉換和載入資料](../linux/sql-server-linux-migrate-ssis.md)。

## <a name="for-azure-sql-database-get-the-connection-info"></a>針對 Azure SQL Database，請取得連線資訊

若要在 Azure SQL Database 上執行套件，請取得連線至 SSIS 目錄資料庫 (SSISDB) 所需的連線資訊。 在下列程序中，您需要完整伺服器名稱和登入資訊。

1. 登入 [Azure 入口網站](https://portal.azure.com/)。
2. 從左側功能表中選取 [SQL 資料庫]****，然後選取 [SQL 資料庫]**** 頁面上的 SSISDB 資料庫。 
3. 在您資料庫的 [概觀]**** 頁面上，檢閱完整伺服器名稱。 若要顯示 [按一下以複製]**** 選項，請將滑鼠指標暫留在伺服器名稱上。 
4. 如果您忘記 Azure SQL Database 伺服器登入資訊，請巡覽至 [SQL Database 伺服器] 頁面來檢視伺服器管理員名稱。 如有需要，您可以重設密碼。

## <a name="connect-to-the-ssisdb-database"></a>連線至 SSISDB 資料庫

使用 SQL Server Management Studio，以建立與 SSIS 目錄的連線。 

1. 開啟 SQL Server Management Studio。

2. 在 [連線至伺服器]  對話方塊中，輸入下列資訊：

   | 設定       | 建議的值 | 其他資訊 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器類型** | 資料庫引擎 | 這是必要的值。 |
   | **伺服器名稱** | 完整伺服器名稱 | 如果您要連線至 Azure SQL Database 伺服器，則名稱的格式如下：`<server_name>.database.windows.net`。 |
   | **驗證** | SQL Server 驗證 | 使用 SQL Server 驗證時，您可以連線到 SQL Server 或 Azure SQL Database。 如果要連線至 Azure SQL Database 伺服器，您無法使用 Windows 驗證。 |
   | **登入** | 伺服器系統管理員帳戶 | 這個帳戶是您在建立伺服器時指定的帳戶。 |
   | **密碼** | 伺服器系統管理員帳戶的密碼 | 這個密碼是您在建立伺服器時指定的密碼。 |

3. 按一下 [ **連接**]。 [物件總管] 視窗會在 SSMS 中開啟。 

4. 在 [物件總管] 中，展開 [Integration Services 目錄]  ，然後展開 [SSISDB]  以檢視 SSIS 目錄資料庫中的物件。

## <a name="run-a-package"></a>執行套件

1. 在 [物件總管] 中，選取您要執行的套件。

2. 按一下滑鼠右鍵，然後選取 [執行]****。 即會開啟 [執行套件]**** 對話方塊。

3.  使用 **[執行封裝]** 對話方塊中， **[參數]** 、 **[連線管理員]** 和 [進階] 標籤上的設定，設定封裝執行。

4.  按一下 [確定] 以執行套件。

## <a name="next-steps"></a>後續步驟
- 請考慮使用其他方式來執行套件。
    - [使用 Transact-SQL 執行 SSIS 套件 (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元執行 SSIS 套件](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 套件](ssis-quickstart-run-powershell.md)
    - [使用 C# 執行 SSIS 套件](./ssis-quickstart-run-dotnet.md)