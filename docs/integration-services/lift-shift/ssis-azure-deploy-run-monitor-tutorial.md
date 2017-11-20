---
title: "部署、 執行和監視 Azure 上的 SSIS 封裝 |Microsoft 文件"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: 2e16666c412870cc55024e7156752f43ddbc1800
ms.contentlocale: zh-tw
ms.lasthandoff: 10/13/2017

---
# <a name="deploy-run-and-monitor-an-ssis-package-on-azure"></a>部署、 執行和監視 Azure 上的 SSIS 封裝
本教學課程會示範如何將 SQL Server Integration Services 專案部署至 SSISDB 目錄資料庫，在 Azure SQL Database、 Azure SSIS 整合執行階段中執行封裝及監視正在執行的封裝。

## <a name="prerequisites"></a>必要條件

開始之前，請確定您有 17.2 或更新版本的 SQL Server Management Studio 的版本。 若要下載最新版本的 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

也請確定您已將 SSISDB 資料庫設定和佈建 Azure SSIS 整合執行階段。 如需如何在 Azure 上的 SSIS 佈建資訊，請參閱[增益及 shift SQL Server Integration Services (SSIS) 封裝至 Azure](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure)。

## <a name="connect-to-the-ssisdb-database"></a>連接到 SSISDB 資料庫

使用 SQL Server Management Studio 連接到 Azure SQL Database 伺服器上的 SSIS 目錄。 如需詳細資訊，請參閱[連接到 Azure 上的 SSISDB 目錄資料庫](ssis-azure-connect-to-catalog-database.md)。

> [!IMPORTANT]
> Azure SQL Database 伺服器通訊埠 1433年上接聽。 如果您嘗試連接到 Azure SQL Database 伺服器從公司防火牆內，此連接埠必須開啟在公司防火牆中針對您已成功連接。

1. 開啟 SQL Server Management Studio。

2. **連接到伺服器**。 在**連接到伺服器**對話方塊方塊中，輸入下列資訊：

   | 設定       | 建議的值 | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器類型** | Database Engine | 這是必要的值。 |
   | **伺服器名稱** | 完整的伺服器名稱 | 名稱應該採用下列格式： **mysqldbserver.database.windows.net**。 如果您需要的伺服器名稱，請參閱[連接到 Azure 上的 SSISDB 目錄資料庫](ssis-azure-connect-to-catalog-database.md)。 |
   | **驗證** | SQL Server 驗證 | 本快速入門使用 SQL 驗證。 |
   | **登入** | 伺服器系統管理員帳戶 | 這是您在建立伺服器時指定的帳戶。 |
   | **密碼** | 伺服器系統管理員帳戶密碼 | 這是您在建立伺服器時指定的密碼。 |

3. **連接到 SSISDB 資料庫**。 選取**選項**展開**連接到伺服器** 對話方塊。 在展開**連接到伺服器**對話方塊中，選取**連接屬性** 索引標籤。在**連接至資料庫**欄位中，選取或輸入`SSISDB`。

4. 然後選取**連接**。 在 SSMS 中，開啟 [物件總管] 視窗。 

5. 在 物件總管 中，展開**Integration Services 目錄**，然後展開  **SSISDB** SSIS 目錄資料庫中檢視的物件。

## <a name="deploy-a-project"></a>部署專案

### <a name="start-the-integration-services-deployment-wizard"></a>啟動 Integration Services 部署精靈
1. 在 物件總管，在 SSMS 中，與**Integration Services 目錄**節點和**SSISDB**節點展開，展開 專案資料夾。

2.  選取**專案**節點。

3.  以滑鼠右鍵按一下**專案**節點，然後選取**部署專案**。 Integration Services 部署精靈 隨即開啟。 您可以部署專案，從 SSIS 目錄資料庫或檔案系統。

### <a name="deploy-a-project-with-the-deployment-wizard"></a>部署具有 [部署精靈] 的專案
1. 在**簡介**頁面的 部署精靈 中，檢閱 簡介。 選取**下一步**開啟**選取來源**頁面。

2. 在**選取來源**頁面上，選取要部署現有的 SSIS 專案。
    -   若要部署您建立的專案部署檔案，請選取 [專案部署檔案]  ，並輸入 .ispac 檔案的路徑。
    -   若要部署的專案位於 SSIS 目錄中，選取**Integration Services 目錄**，然後輸入類別目錄中的專案的 伺服器名稱和路徑。
    -   選取**下一步**查看**選取目的地**頁面。
  
3.  在**選取目的地**頁面上，選取專案目的地。
    -   輸入完整的伺服器名稱格式`<server_name>.database.windows.net`。
    -   然後選取**瀏覽**在 SSISDB 中選取目標資料夾。
    -   選取**下一步**開啟**檢閱**頁面。  
  
4.  在**檢閱**頁面上，檢閱您選取的設定。
    -   您可以選取來變更您的選擇**上一步**，或在左窗格中選取的任何步驟。
    -   選取**部署**啟動部署程序。
  
5.  部署程序完成之後，**結果**頁面隨即開啟。 此頁面會顯示每個動作執行成功或失敗。
    -   如果動作失敗、 選取**失敗**中**結果**資料行，以顯示錯誤的說明。
    -   （選擇性） 選取**儲存報表...**將結果儲存至 XML 檔案。
    -   選取**關閉**結束精靈。

## <a name="run-a-package"></a>執行封裝

1. 在 物件總管，在 SSMS 中，選取您想要執行的封裝。

2. 以滑鼠右鍵按一下並選取**Execute**開啟**執行封裝** 對話方塊。

3.  在**執行封裝**對話方塊方塊中，設定封裝執行所使用的設定**參數**，**連接管理員**，和**進階**索引標籤。

4.  選取**確定**執行封裝。

## <a name="monitor-the-running-package-in-ssms"></a>監視在 SSMS 中執行的封裝

若要檢視目前執行中的 Integration Services 伺服器上，例如部署、 驗證及封裝執行的 Integration Services 作業的狀態使用**作用中的作業**在 SSMS 中的對話方塊。 若要開啟**作用中的作業**對話方塊中，以滑鼠右鍵按一下**SSISDB**，然後選取**作用中的作業**。

您也可以選取在 [物件總管] 中，以滑鼠右鍵按一下並選取封裝**報表**，然後**標準報表**，然後**所有執行**。

如需如何監視在 SSMS 中的執行中封裝的詳細資訊，請參閱[監視執行中封裝和其他作業](https://docs.microsoft.com/en-us/sql/integration-services/performance/monitor-running-packages-and-other-operations)。

## <a name="monitor-the-azure-ssis-integration-runtime"></a>監視 Azure SSIS 整合執行階段

若要取得 Azure SSIS 整合執行階段執行封裝的狀態資訊，請使用下列 PowerShell 命令： 為每個命令，提供 Data Factory 及 Azure SSIS 紅外線遙控器，資源群組的名稱。

### <a name="get-metadata-about-the-azure-ssis-integration-runtime"></a>取得有關 Azure SSIS 整合執行階段中繼資料

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

### <a name="get-the-status-of-the-azure-ssis-integration-runtime"></a>取得 Azure SSIS 整合執行階段的狀態

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -Status -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

## <a name="next-steps"></a>後續的步驟
- 了解如何排程封裝執行。 如需詳細資訊，請參閱[排程 SSIS 封裝在 Azure 上的執行](ssis-azure-schedule-packages.md)

