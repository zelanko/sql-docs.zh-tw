---
title: 在 Azure 中部署和執行 SSIS 套件 | Microsoft Docs
description: 了解您如何將 SQL Server Integration Services (SSIS) 專案、套件和工作負載移至 Microsoft Azure 雲端。
ms.date: 07/01/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.suite: sql
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 3864a5ac0f4bb1ebd87ab54a0b949ec80b636bc6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304388"
---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>將 SQL Server Integration Services 工作負載隨即轉移至雲端
您現在可以將 SQL Server Integration Services (SSIS) 專案、套件和工作負載移至 Azure 雲端。 使用熟悉的工具 (例如 SQL Server Management Studio，SSMS)，在 Azure SQL Database 或 SQL Database 受控執行個體 (預覽) 的 SSIS 目錄 (SSISDB) 中，部署、執行及管理 SSIS 專案和套件。

## <a name="benefits"></a>優點
將內部部署 SSIS 工作負載移至 Azure 有下列優點：
-   **降低營運成本**，並降低您在內部部署環境或 Azure 虛擬機器上執行 SSIS 時所擁有的管理基礎結構負擔。
-   **提高高可用性** 而且可以指定每個叢集有多個節點，以及 Azure 和 Azure SQL Database 的高可用性功能。
-   **提高延展性**以及指定每個節點的多個核心 (相應增加) 和每個叢集的多個節點 (相應放大) 的能力。

## <a name="architecture-of-ssis-on-azure"></a>Azure 上的 SSIS 架構
下表強調顯示內部部署環境上的 SSIS 與 Azure 上的 SSIS 之間的差異。

最明顯的差異在於區隔儲存與執行階段。 Azure Data Factory 會裝載 Azure 上 SSIS 套件的執行階段引擎。 執行階段引擎稱為 Azure SSIS Integration Runtime (Azure SSIS IR)。 如需詳細資訊，請參閱 [Azure SSIS Integration Runtime](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime)。

| 位置 | 儲存體 | 執行階段 | 延展性 |
|---|---|---|---|
| 內部部署 | SQL Server | SQL Server 所裝載的 SSIS 執行階段 | SSIS Scale Out (在 SQL Server 2017 和更新版本中)<br/><br/>自訂解決方案 (在舊版 SQL Server 中) |
| 在 Azure 上 | SQL Database 或 SQL Database 受控執行個體 (預覽) | Azure SSIS Integration Runtime，Azure Data Factory 的元件 | Azure SSIS Integration Runtime 的擴充選項 |
| | | | |

## <a name="provision-ssis-on-azure"></a>在 Azure 上佈建 SSIS

**佈建**。 您必須先佈建 SSIS 目錄 (SSISDB) 與 Azure-SSIS Integration Runtime，才能在 Azure 中部署和執行 SSIS 套件。

-   若要在 Azure 入口網站中將 SSIS 佈建在 Azure 上，請遵循本文中的佈建步驟：[在 Azure Data Factory 中佈建 Azure-SSIS 整合執行階段](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)。 

-   若要使用 PowerShell 將 SSIS 佈建在 Azure 上，請遵循本文中的佈建步驟：[使用 PowerShell 在 Azure Data Factory 中佈建 Azure-SSIS 整合執行階段](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure-powershell)。

您只需要佈建 Azure SSIS IR 一次。 之後，您可以使用熟悉的工具 (例如 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS)) 來部署、設定、執行、監視、排程及管理套件。

> [!NOTE]
> 所有 Azure 區域都還無法使用 Azure-SSIS Integration Runtime。 如需所支援區域的資訊，請參閱[不同區域的產品 - Microsoft Azure](https://azure.microsoft.com/regions/services/)。

**相應增加和相應放大**。當您佈建 Azure SSIS IR 時，可以指定下列選項的值來相應增加和相應放大：
-   節點大小 (包含核心數目) 以及叢集中的節點數目。
-   裝載 SSIS 目錄資料庫 (SSISDB) 的現有 Azure SQL Database 執行個體，以及資料庫的服務層。
-   每個節點的最大平行執行。

**改善效能**。 如需詳細資訊，請參閱[設定 Azure SSIS Integration Runtime 以獲得高效能](https://docs.microsoft.com/azure/data-factory/configure-azure-ssis-integration-runtime-performance)。

**降低成本**。 為了降低成本，請只在需要時才執行 Azure-SSIS IR。 如需詳細資訊，請參閱[如何排程 Azure SSIS 整合執行階段的啟動和停止](https://docs.microsoft.com/azure/data-factory/how-to-schedule-azure-ssis-integration-runtime)。

## <a name="design-packages"></a>設計套件

您會在 SSDT 的內部部署環境或已安裝 SSDT 的 Visual Studio 中繼續**設計和建置套件**。

### <a name="connect-to-data-sources"></a>連線到資料來源

若要使用 **Windows 驗證**從雲端連線至內部部署資料來源，請參閱[在 Azure 中從 SSIS 套件使用 Windows 驗證來連線至資料來源和檔案共用](ssis-azure-connect-with-windows-auth.md)。

若要連線至檔案和檔案共用，請參閱[在 SSIS 套件部署於 Azure 的情況下，於內部部署與 Azure 中開啟和儲存檔案](ssis-azure-files-file-shares.md)。

### <a name="available-ssis-components"></a>可用的 SSIS 元件

當您佈建 SQL Database 執行個體來裝載 SSISDB 時，也會安裝 Azure Feature Pack for SSIS 以及 Access 可轉散發套件。 除了內建元件所支援的資料來源之外，這些元件還會提供與各種 **Azure** 資料來源及 **Excel 和 Access** 檔案的連線。

您也可以安裝其他元件。例如，您可以安裝預設不會安裝的驅動程式。 如需詳細資訊，請參閱[自訂 Azure-SSIS 整合執行階段的安裝](/azure/articles/data-factory/how-to-configure-azure-ssis-ir-custom-setup)。

如果您有 Enterprise Edition 授權，將會提供其他元件。 如需詳細資訊，請參閱[佈建 Azure-SSIS 整合執行階段的企業版](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-enterprise-edition)。

如果您是 ISV，可以更新授權元件的安裝，使其可在 Azure 上使用。 如需詳細資訊，請參閱[安裝 Azure-SSIS 整合執行階段的付費或授權自訂元件](https://docs.microsoft.com/azure/data-factory/how-to-develop-azure-ssis-ir-licensed-components)。

### <a name="transaction-support"></a>交易支援

對於 SQL Server 內部部署和 Azure 虛擬機器，您可以使用 Microsoft Distributed Transaction Coordinator (MSDTC) 交易。 若要在 Azure SSIS IR 的每個節點上設定 MSDTC，請使用自訂安裝程式功能。 如需詳細資訊，請參閱[自訂 Azure-SSIS 整合執行階段的安裝程式](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup)。

使用 Azure SQL Database，您只能使用彈性交易。 如需詳細資訊，請參閱[跨雲端資料庫的分散式交易](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-transactions-overview)。

## <a name="deploy-and-run-packages"></a>部署和執行套件

若要開始使用，請參閱[教學課程：在 Azure 中部署和執行 SQL Server Integration Services (SSIS) 套件](ssis-azure-deploy-run-monitor-tutorial.md)。

### <a name="prerequisites"></a>先決條件

若要將 SSIS 套件部署至 Azure，您必須擁有下列其中一個版本的 SQL Server Data Tools (SSDT)：
-   針對 Visual Studio 2017 15.3 版或更新版本。
-   針對 Visual Studio 2015 17.2 版或更新版本。

### <a name="connect-to-ssisdb"></a>連線至 SSISDB

裝載 SSISDB 的 **SQL Database 名稱**會變成要在部署及執行 SSDT 和 SSMS 中的套件時使用之名稱 (共由四個部分組成) 的第一個部分，格式如下 - `<sql_database_name>.database.windows.net`。 如需如何在 Azure 中連線至 SSIS 目錄資料庫的詳細資訊，請參閱[連線至 Azure 中的 SSIS 目錄 (SSISDB)](ssis-azure-connect-to-catalog-database.md)。

### <a name="deploy-projects-and-packages"></a>部署專案和套件

當您將您專案部署至 Azure 上的 SSISDB 時，必須使用**專案部署模型**，而非套件部署模型。

若要在 Azure 上部署專案，您可以使用數個熟悉的工具與指令碼選項中的其中一個：
-   SQL Server Management Studio (SSMS)
-   Transact-SQL (從 SSMS、Visual Studio Code 或另一個工具)
-   命令列工具
-   PowerShell 或 C# 和 SSIS 管理物件模型

部署程序會驗證套件，以確認這些套件可在 Azure-SSIS Integration Runtime 上執行。 如需詳細資訊，請參閱[驗證部署到 Azure 的 SQL Server Integration Services (SSIS) 套件](ssis-azure-validate-packages.md)。

如需使用 SSMS 和 [Integration Services 部署精靈] 的部署範例，請參閱[教學課程：在 Azure 中部署和執行 SQL Server Integration Services (SSIS) 套件](ssis-azure-deploy-run-monitor-tutorial.md)。

### <a name="version-support"></a>版本支援

您可以將任何版本的 SSIS 所建立之套件，部署至 Azure。 當您將套件部署至 Azure 時，如果沒有任何驗證錯誤，則該套件會自動升級為最新的套件格式。 換句話說，其一律會升級到最新版本的 SSIS。

### <a name="run-packages"></a>執行套件

若要執行 Azure 中部署的 SSIS 套件，您可以使用各種方法。 如需詳細資訊，請參閱[執行部署於 Azure 中的 SQL Server Integration Services (SSIS) 套件](ssis-azure-run-packages.md)。

### <a name="run-packages-in-an-azure-data-factory-pipeline"></a>在 Azure Data Factory 管線中執行套件

若要在 Azure Data Factory 管線中執行 SSIS 套件，請使用「執行 SSIS 套件活動」。 如需詳細資訊，請參閱[在 Azure Data Factory 中使用執行 SSIS 套件活動執行 SSIS 套件](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)。

當您使用「執行 SSIS 套件活動」在 Data Factory 管線中執行套件時，可在執行階段將值傳遞至套件。 若要傳遞一或多個執行階段值，請使用 SQL Server Management Studio (SSMS) 在 SSISDB 中建立 SSIS 執行環境。 在每個環境中，建立變數並指派與專案或套件參數相對應的值。 請在 SSMS 中設定您的 SSIS 套件，將這些環境變數與專案或套件參數建立關聯。 當您在管線中執行套件時，藉由在「執行 SSIS 套件」活動 UI 的 [設定] 索引標籤上指定不同的環境路徑，即可在環境之間進行切換。 如需 SSIS 環境的詳細資訊，請參閱[建立和對應伺服器環境](../packages/deploy-integration-services-ssis-projects-and-packages.md#create-and-map-a-server-environment)。

## <a name="monitor-packages"></a>監視套件

若要監視執行中套件，請在 SSMS 中使用下列報告選項。
-   以滑鼠右鍵按一下 [SSISDB]，然後選取 [作用中的作業] 以開啟 [作用中的作業] 對話方塊。
-   在 [物件總管] 中選取套件，並按一下滑鼠右鍵，然後依序選取 [報表]、[標準報表] 和 [所有執行]。

若要監視 Azure SSIS Integration Runtime，請參閱[監視 Azure SSIS Integration Runtime](https://docs.microsoft.com/azure/data-factory/monitor-integration-runtime#azure-ssis-integration-runtime)。

## <a name="schedule-packages"></a>排程套件
您可以使用各種工具來排程執行部署在 Azure 中的套件。 如需詳細資訊，請參閱[排程部署於 Azure 中的 SQL Server Integration Services (SSIS) 套件執行](ssis-azure-schedule-packages.md)。

## <a name="next-steps"></a>後續步驟
若要在 Azure 上開始使用 SSIS 工作負載，請參閱下列文章：
-   [教學課程：在 Azure 中部署和執行 SQL Server Integration Services (SSIS) 套件](ssis-azure-deploy-run-monitor-tutorial.md)
-   [在 Azure Data Factory 中佈建 Azure-SSIS 整合執行階段](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)
