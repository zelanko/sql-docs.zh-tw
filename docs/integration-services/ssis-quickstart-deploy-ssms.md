---
title: "使用 SSMS 部署 SSIS 專案 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: quick-start
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 151089d319a1106f81426beee4aa2989bc72b978
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="deploy-an-ssis-project-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 部署 SSIS 專案
本快速入門示範如何使用 SQL Server Management Studio (SSMS) 連線至 SSIS 目錄資料庫，然後執行 [Integration Services 部署精靈] 將 SSIS 專案部署至 SSIS 目錄。 

SQL Server Management Studio 是整合式環境，用於管理任何 SQL 基礎結構，從 SQL Sever 到 SQL Database 皆適用。 如需 SSMS 的詳細資訊，請參閱 [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)。

## <a name="prerequisites"></a>Prerequisites

開始之前，請確定您有最新版的 SQL Server Management Studio。 若要下載 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="connect-to-the-ssisdb-database"></a>連線至 SSISDB 資料庫

使用 SQL Server Management Studio，以建立與 SSIS 目錄的連線。 

> [!NOTE]
> Azure SQL Database 伺服器會接聽連接埠 1433。 如果您要嘗試透過公司防火牆連線至 Azure SQL Database 伺服器，則必須在公司防火牆中開啟此連接埠，讓您成功連線。

1. 開啟 SQL Server Management Studio。

2. 在 [連線至伺服器] 對話方塊中，輸入下列資訊：

   | 設定       | 建議值 | 其他資訊 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器類型** | 資料庫引擎 | 這是必要的值。 |
   | **伺服器名稱** | 完整伺服器名稱 | 如果您要連線至 Azure SQL Database 伺服器，則名稱的格式如下：`<server_name>.database.windows.net`。 |
   | **驗證** | SQL Server 驗證 | 本快速入門使用 SQL 驗證。 |
   | **登入** | 伺服器系統管理員帳戶 | 這是您在建立伺服器時指定的帳戶。 |
   | **密碼** | 伺服器系統管理員帳戶的密碼 | 這是您在建立伺服器時指定的密碼。 |

3. 按一下 **[連接]**。 [物件總管] 視窗會在 SSMS 中開啟。 

4. 在 [物件總管] 中，展開 [Integration Services 目錄]，然後展開 [SSISDB] 以檢視 SSIS 目錄資料庫中的物件。

## <a name="start-the-integration-services-deployment-wizard"></a>啟動 Integration Services 部署精靈
1. 在 [物件總管] 中，展開 [Integration Services 目錄] 節點和 [SSISDB] 之後，請展開專案資料夾。

2.  展開 [專案] 資料夾。

3.  以滑鼠右鍵按一下 [專案] 節點，然後選取 [部署專案]。 即會開啟 [Integration Services 部署精靈]。 您可以從目前的目錄或檔案系統部署專案。

## <a name="deploy-a-project-with-the-wizard"></a>使用精靈部署專案
1. 在精靈的 [簡介] 頁面上，檢閱簡介。 按一下 [下一步] 開啟 [選取來源] 頁面。

2. 在 [選取來源] 頁面上，選取要部署的現有 SSIS 專案。
    -   若要部署您建立的專案部署檔案，請選取 [專案部署檔案]  ，並輸入 .ispac 檔案的路徑。
    -   若要部署位於 SSIS 目錄中的專案，請選取 [Integration Services 目錄]，然後輸入伺服器名稱以及該專案在目錄中的路徑。
    按一下 [下一步]  ，以查看 [選取目的地]  頁面。
  
3.  在 [選取目的地] 頁面上，選取專案目的地。
    -   輸入完整伺服器名稱。 如果目標伺服器是 Azure SQL Database 伺服器，則名稱的格式如下：`<server_name>.database.windows.net`。
    -   然後按一下 [瀏覽] 在 SSISDB 中選取目標資料夾。
    按一下 [下一步] 開啟 [檢閱] 頁面。  
  
4.  在 [檢閱] 頁面上，檢閱您選取的設定。
    -   您可以按一下 **[上一步]**，或按一下左窗格中的任何步驟來變更您的選取項目。
    -   按一下 [部署]  開始部署程序。
  
5.  完成部署程序之後，會開啟 [結果] 頁面。 此頁面會顯示每個動作執行成功或失敗。
    -   如果動作失敗，請按一下 [結果] 資料行中的 [失敗] 以顯示錯誤的說明。
    -   選擇性地按一下 [儲存報表]，將結果儲存至 XML 檔案。
    -   按一下 [關閉] 結束精靈。

## <a name="next-steps"></a>後續步驟
- 請考慮使用其他方式來部署套件。
    - [使用 Transact-SQL 部署 SSIS 套件 (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [使用 Transact-SQL 部署 SSIS 套件 (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [從命令提示字元中部署 SSIS 套件](./ssis-quickstart-deploy-cmdline.md)
    - [使用 PowerShell 部署 SSIS 套件](ssis-quickstart-deploy-powershell.md)
    - [使用 C# 部署 SSIS 套件](./ssis-quickstart-deploy-dotnet.md) 
- 執行已部署的套件。 若要執行套件，您可以從數個工具和語言進行選擇。 如需詳細資訊，請參閱下列文章：
    - [使用 SSMS 執行 SSIS 套件](./ssis-quickstart-run-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元中執行 SSIS 套件](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 套件](ssis-quickstart-run-powershell.md)
    - [使用 C# 執行 SSIS 套件](./ssis-quickstart-run-dotnet.md) 
