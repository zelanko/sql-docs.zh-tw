---
title: 將 SQL Server Integration Services 工作負載隨即轉移至雲端 | Microsoft Docs
ms.date: 04/13/2018
ms.topic: article
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10870216c2abc826a72bb16715701a794e651610
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>將 SQL Server Integration Services 工作負載隨即轉移至雲端
您現在可以將 SQL Server Integration Services (SSIS) 套件和工作負載移至 Azure 雲端。
-   在 Azure SQL Database 或 SQL Database 受控執行個體 (預覽) 的 SSIS 目錄資料庫 (SSISDB) 中，儲存並管理 SSIS 專案和套件。
-   在 Azure SSIS Integration Runtime (引進為 Azure Data Factory 第 2 版的一部分) 執行個體中執行套件。
-   使用熟悉的工具 (例如 SQL Server Management Studio (SSMS)) 進行這些一般工作。

## <a name="benefits"></a>優點
將內部部署 SSIS 工作負載移至 Azure 有下列優點：
-   **降低營運成本**，並降低您在內部部署環境或 Azure 虛擬機器上執行 SSIS 時所擁有的管理基礎結構負擔。
-   **提高高可用性** 而且可以指定每個叢集有多個節點，以及 Azure 和 Azure SQL Database 的高可用性功能。
-   **提高延展性**以及指定每個節點的多個核心 (相應增加) 和每個叢集的多個節點 (相應放大) 的能力。

## <a name="architecture-overview"></a>架構概觀
下表強調顯示內部部署環境上的 SSIS 與 Azure 上的 SSIS 之間的差異。 最明顯的差異在於區隔儲存與運算。

| Storage | 執行階段 | 延展性 |
|---|---|---|
| 內部部署 (SQL Server) | SQL Server 所裝載的 SSIS 執行階段 | SSIS Scale Out (在 SQL Server 2017 和更新版本中)<br/><br/>自訂解決方案 (在舊版 SQL Server 中) |
| 在 Azure 上 (SQL Database 或 SQL Database 受控執行個體 (預覽)) | Azure SSIS Integration Runtime，即 Azure Data Factory 第 2 版的元件 | SSIS IR 的縮放選項 |
| | | |

Azure Data Factory 會裝載 Azure 上 SSIS 套件的執行階段引擎。 執行階段引擎稱為 Azure SSIS Integration Runtime (SSIS IR)。

當您佈建 SSIS IR 時，可以指定下列選項的值來相應增加和相應放大：
-   節點大小 (包含核心數目) 以及叢集中的節點數目。
-   裝載 SSIS 目錄資料庫 (SSISDB) 的現有 Azure SQL Database 執行個體，以及資料庫的服務層。
-   每個節點的最大平行執行。

您只需要佈建 SSIS IR 一次。 之後，您可以使用熟悉的工具 (例如 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS)) 來部署、設定、執行、監視、排程以及管理套件。

> [!NOTE]
> 在此公開預覽期間，所有區域都還無法使用 Azure SSIS Integration Runtime。 如需所支援區域的資訊，請參閱[區域可用的產品 - Microsoft Azure](https://azure.microsoft.com/regions/services/)。

Data Factory 也支援其他類型的 Integration Runtime。 若要深入了解 SSIS IR 和其他類型的整合執行階段，請參閱 [Azure Data Factory 中的整合執行階段](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime)。

## <a name="version-info"></a>版本資訊

您可以將任何版本的 SSIS 所建立之套件，部署至 Azure。 當您將套件部署至 Azure 時，如果沒有任何驗證錯誤，則該套件會自動升級為最新的套件格式。 換句話說，其一律會升級到最新版本的 SSIS。

部署程序會驗證套件，以確認這些套件可在 Azure-SSIS Integration Runtime 上執行。 如需詳細資訊，請參閱[驗證部署到 Azure 的 SSIS 套件](ssis-azure-validate-packages.md)。

## <a name="prerequisites"></a>Prerequisites

本文中所述的功能，需要下列版本的 SQL Server Data Tools (SSDT)：
-   針對 Visual Studio 2017 15.3 版 (Preview) 或更新版本。
-   針對 Visual Studio 2015 17.2 版或更新版本。

如需 Azure 中的必要條件詳細資訊，請參閱[將 SSIS 套件部署到 Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal)。

## <a name="provision-ssis-on-azure"></a>在 Azure 上佈建 SSIS
您必須先佈建 SSIS 目錄資料庫 (SSISDB) 與 Azure-SSIS Integration Runtime，才可在 Azure 中部署及執行 SSIS 套件。 請遵循此文章中的佈建步驟：[將 SSIS 套件部署到 Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal)。

裝載 SSISDB 的「SQL Database 名稱」會變成要在部署和管理 SSDT 和 SSMS 中的套件時使用之名稱 (共由四個部分組成) 的第一個部分 - `<sql_database_name>.database.windows.net`。

如需如何連線至 SSIS 目錄資料庫的相關資訊，請參閱[連線至 Azure 上的 SSISDB 目錄資料庫](ssis-azure-connect-to-catalog-database.md)。

## <a name="design-packages"></a>設計套件
您會在 SSDT 的內部部署環境或已安裝 SSDT 的 Visual Studio 中繼續**設計和建置套件**。

如需如何使用 **Windows 驗證**從雲端連線至內部部署資料來源的相關資訊，請參閱[使用 Windows 驗證連線至內部部署資料來源與 Azure 檔案共用](ssis-azure-connect-with-windows-auth.md)。

如需如何連線至檔案與檔案共用的相關資訊，請參閱[使用 SSIS 儲存及擷取內部部署和 Azure 中檔案共用上的檔案](ssis-azure-files-file-shares.md)。

當您佈建 SQL Database 執行個體來裝載 SSISDB 時，也會安裝 Azure Feature Pack for SSIS 以及 Access 可轉散發套件。 除了內建元件所支援的資料來源之外，這些元件還會提供與各種 **Azure** 資料來源及 **Excel 和 Access** 檔案的連線。

您也可以安裝其他元件。 如需詳細資訊，請參閱[自訂 Azure-SSIS 整合執行階段的安裝程式](/azure/articles/data-factory/how-to-configure-azure-ssis-ir-custom-setup.md)。

## <a name="deploy-and-run-packages"></a>部署和執行套件
當您將您專案部署至 Azure 上的 SSISDB 時，必須使用**專案部署模型**，而非套件部署模型。

若要在 Azure 上部署專案及執行套件，您可以使用數個熟悉的工具與指令碼選項中的其中一個：
-   SQL Server Management Studio (SSMS)
-   Transact-SQL (從 SSMS、Visual Studio Code 或另一個工具)
-   命令列工具
-   PowerShell
-   C# 和 SSIS 管理物件模型

若要開始使用，請參閱[在 Azure 上部署、執行及監視 SSIS 套件](ssis-azure-deploy-run-monitor-tutorial.md)。

## <a name="monitor-packages"></a>監視套件
若要監視 SSMS 中的執行中套件，您可以在 SSMS 中使用下列其中一個報告工具。
-   以滑鼠右鍵按一下 [SSISDB]，然後選取 [作用中的作業] 以開啟 [作用中的作業] 對話方塊。
-   在 [物件總管] 中選取套件，並按一下滑鼠右鍵，然後依序選取 [報表]、[標準報表] 和 [所有執行]。

## <a name="schedule-packages"></a>排程套件
若要排程執行 SQL Database 中所儲存的套件，您可以使用下列工具：
-   SQL Server Agent 內部部署
-   Data Factory SQL Server 預存程序活動

如需詳細資訊，請參閱[排程 Azure 上的 SSIS 套件執行](ssis-azure-schedule-packages.md)。

## <a name="next-steps"></a>後續步驟
若要在 Azure 上開始使用 SSIS 工作負載，請參閱下列文章：
-   [將 SSIS 套件部署到 Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal)
-   [部署、執行和監視 Azure 上的 SSIS 套件](ssis-azure-deploy-run-monitor-tutorial.md)
