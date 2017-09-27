---
title: "SSIS 專案部署從命令提示字元 |Microsoft 文件"
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
ms.openlocfilehash: a1df574e0436a9fa81e714dfdc21bcbd43c0bda8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>SSIS 專案部署從 ISDeploymentWizard.exe 在命令提示字元
本快速入門教學課程示範如何執行 Integration Services 部署精靈，以部署的 SSIS 專案，從命令提示字元`ISDeploymentWizard.exe`。

如需 Integration Services 部署精靈的詳細資訊，請參閱[Integration Services 部署精靈](/sql/integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard)。

## <a name="start-the-integration-services-deployment-wizard"></a>啟動 Integration Services 部署精靈
1. 開啟 [命令提示字元] 視窗。

2. 執行 `ISDeploymentWizard.exe`。 Integration Services 部署精靈 隨即開啟。

    如果資料夾包含`ISDeploymentWizard.exe`不在您`path`可能要使用的環境變數`cd`命令來變更為它的目錄。 若是 SQL Server 2017，此資料夾通常位於`C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`。

## <a name="deploy-a-project-with-the-wizard"></a>部署專案精靈
1. 在**簡介**頁面在精靈的檢閱 簡介。 按一下**下一步**開啟**選取來源**頁面。

2. 在**選取來源**頁面上，選取要部署現有的 SSIS 專案。
    -   若要部署您建立的專案部署檔案，請選取 [專案部署檔案]  ，並輸入 .ispac 檔案的路徑。
    -   若要部署的專案位於 SSIS 目錄中，選取**Integration Services 目錄**，然後輸入類別目錄中的專案的 伺服器名稱和路徑。
    按一下 [下一步]  ，以查看 [選取目的地]  頁面。
  
3.  在**選取目的地**頁面上，選取專案目的地。
    -   輸入完整的伺服器名稱。 如果目標伺服器是 Azure SQL Database 伺服器，則名稱是以下列格式： `<server_name>.database.windows.net`。
    -   然後按一下 **瀏覽**在 SSISDB 中選取目標資料夾。
    按一下**下一步**開啟**檢閱**頁面。  
  
4.  在**檢閱**頁面上，檢閱您選取的設定。
    -   您可以按一下 **[上一步]**，或按一下左窗格中的任何步驟來變更您的選取項目。
    -   按一下 [部署]  開始部署程序。
  
5.  部署程序完成之後，**結果**頁面隨即開啟。 此頁面會顯示每個動作執行成功或失敗。
    -   如果動作失敗、 按一下**失敗**中**結果**資料行，以顯示錯誤的說明。
    -   （選擇性） 按一下**儲存報表...**將結果儲存至 XML 檔案。
    -   按一下**關閉**結束精靈。

## <a name="next-steps"></a>後續的步驟
- 考慮以其他方式來部署封裝。
    - [部署 SSIS 封裝使用 SSMS](./ssis-quickstart-deploy-ssms.md)
    - [部署 SSIS 封裝使用 TRANSACT-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [部署 SSIS 封裝使用 TRANSACT-SQL (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [部署 SSIS 封裝使用 PowerShell](ssis-quickstart-deploy-powershell.md)
    - [部署使用 C# 的 SSIS 封裝](./ssis-quickstart-deploy-dotnet.md) 
- 執行部署的封裝。 若要執行封裝，您可以選擇從數個工具和語言。 如需詳細資訊，請參閱下列文章：
    - [使用 SSMS 執行 SSIS 封裝](./ssis-quickstart-run-ssms.md)
    - [使用 TRANSACT-SQL (SSMS) 執行 SSIS 封裝](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 TRANSACT-SQL (VS Code) 中執行 SSIS 封裝](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元中執行 SSIS 封裝](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 封裝](ssis-quickstart-run-powershell.md)
    - [使用 C# 中執行 SSIS 封裝](./ssis-quickstart-run-dotnet.md) 

