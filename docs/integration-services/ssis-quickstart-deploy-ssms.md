---
title: "SSIS 專案部署使用 SSMS |Microsoft 文件"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: b9729343ab14563ee6264795d6f098f3c22e91bf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-with-sql-server-management-studio-ssms"></a>SSIS 專案部署與 SQL Server Management Studio (SSMS)
本快速入門示範如何使用 SQL Server Management Studio (SSMS) 連接到 SSIS 目錄資料庫，然後執行 Integration Services 部署精靈，將 SSIS 專案部署至 SSIS 目錄。 

SQL Server Management Studio 是管理任何 SQL 基礎結構，從 SQL 資料庫的 SQL Server 的整合式的環境。 如需 SSMS 的詳細資訊，請參閱[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)。

## <a name="prerequisites"></a>必要條件

開始之前，請確定您有最新版本的 SQL Server Management Studio。 若要下載 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

## <a name="connect-to-the-ssisdb-database"></a>連接到 SSISDB 資料庫

您可以使用 SQL Server Management Studio 來連接到 SSIS 目錄。 

> [!NOTE]
> Azure SQL Database 伺服器通訊埠 1433年上接聽。 如果您嘗試連接到 Azure SQL Database 伺服器從公司防火牆內，此連接埠必須開啟在公司防火牆中針對您已成功連接。

1. 開啟 SQL Server Management Studio。

2. 在**連接到伺服器**對話方塊方塊中，輸入下列資訊：

   | 設定       | 建議的值 | 其他資訊 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器類型** | 資料庫引擎 | 這是必要的值。 |
   | **伺服器名稱** | 完整的伺服器名稱 | 如果您要連線至 Azure SQL Database 伺服器，則名稱是以下列格式： `<server_name>.database.windows.net`。 |
   | **驗證** | SQL Server 驗證 | 本快速入門使用 SQL 驗證。 |
   | **登入** | 伺服器系統管理員帳戶 | 這是您在建立伺服器時指定的帳戶。 |
   | **密碼** | 伺服器系統管理員帳戶密碼 | 這是您在建立伺服器時指定的密碼。 |

3. 按一下 **[連接]**。 在 SSMS 中，開啟 [物件總管] 視窗。 

4. 在 物件總管 中，展開**Integration Services 目錄**，然後展開  **SSISDB** SSIS 目錄資料庫中檢視的物件。

## <a name="start-the-integration-services-deployment-wizard"></a>啟動 Integration Services 部署精靈
1. 在 物件總管 中，與**Integration Services 目錄**節點和**SSISDB**展開，展開 專案資料夾。

2.  選取**專案**節點。

3.  以滑鼠右鍵按一下**專案**節點，然後選取**部署專案**。 Integration Services 部署精靈 隨即開啟。 您可以部署專案，從目前的目錄或檔案系統。

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
    - [部署 SSIS 封裝使用 TRANSACT-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [部署 SSIS 封裝使用 TRANSACT-SQL (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [部署 SSIS 封裝從命令提示字元](./ssis-quickstart-deploy-cmdline.md)
    - [部署 SSIS 封裝使用 PowerShell](ssis-quickstart-deploy-powershell.md)
    - [部署使用 C# 的 SSIS 封裝](./ssis-quickstart-deploy-dotnet.md) 
- 執行部署的封裝。 若要執行封裝，您可以選擇從數個工具和語言。 如需詳細資訊，請參閱下列文章：
    - [使用 SSMS 執行 SSIS 封裝](./ssis-quickstart-run-ssms.md)
    - [使用 TRANSACT-SQL (SSMS) 執行 SSIS 封裝](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 TRANSACT-SQL (VS Code) 中執行 SSIS 封裝](ssis-quickstart-run-tsql-vscode.md)
    - [從命令提示字元中執行 SSIS 封裝](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 執行 SSIS 封裝](ssis-quickstart-run-powershell.md)
    - [使用 C# 中執行 SSIS 封裝](./ssis-quickstart-run-dotnet.md) 

