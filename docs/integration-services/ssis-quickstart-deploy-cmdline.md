---
title: "從命令提示字元中部署 SSIS 專案 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6c3e7f7e3fa870c7aa5b30a5a4a324f0cef7f6ba
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>從命令提示字元中使用 ISDeploymentWizard.exe 部署 SSIS 專案
本快速入門教學課程示範如何執行 Integration Servicess 部署精靈 `ISDeploymentWizard.exe`，從命令提示字元中部署 SSIS 專案。

如需 Integration Services 部署精靈的詳細資訊，請參閱 [Integration Services 部署精靈](packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard)。

## <a name="start-the-integration-services-deployment-wizard"></a>啟動 Integration Services 部署精靈
1. 開啟 [命令提示字元] 視窗。

2. 執行 `ISDeploymentWizard.exe`。 即會開啟 [Integration Services 部署精靈]。

    如果包含 `ISDeploymentWizard.exe` 的資料夾不在 `path` 環境變數中，您可能需要使用 `cd` 命令以切換到其目錄。 若是 SQL Server 2017，此資料夾通常位於 `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`。

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
    -   選擇性：按一下 [儲存報表...]，將結果儲存到 XML 檔案。
    -   按一下 [關閉] 結束精靈。

## <a name="next-steps"></a>後續的步驟
- 請考慮使用其他方式來部署套件。
    - [使用 SSMS 部署 SSIS 套件](./ssis-quickstart-deploy-ssms.md)
    - [使用 Transact-SQL 部署 SSIS 套件 (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [使用 Transact-SQL 部署 SSIS 套件 (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [使用 PowerShell 部署 SSIS 套件](ssis-quickstart-deploy-powershell.md)
    - [使用 C# 部署 SSIS 套件](./ssis-quickstart-deploy-dotnet.md) 
- 執行已部署的套件。 若要執行套件，您可以從數個工具和語言進行選擇。 如需詳細資訊，請參閱下列文章：
    - [使用 SSMS 執行 SSIS 套件](./ssis-quickstart-run-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 Transact-SQL 執行 SSIS 套件 (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元中執行 SSIS 套件](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 套件](ssis-quickstart-run-powershell.md)
    - [使用 C# 執行 SSIS 套件](./ssis-quickstart-run-dotnet.md) 
