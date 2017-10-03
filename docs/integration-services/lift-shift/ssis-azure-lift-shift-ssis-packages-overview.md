---
title: "拿起，然後移至雲端的 SQL Server Integration Services 工作負載 |Microsoft 文件"
ms.date: 09/28/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: e76675099ab290d29231d434eb74e92b613185b7
ms.openlocfilehash: a3693b84ed02583cd47921fbfda84c7df9559b68
ms.contentlocale: zh-tw
ms.lasthandoff: 09/29/2017

---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>拿起，然後移至雲端的 SQL Server Integration Services 工作負載
您現在可以將您的 SQL Server Integration Services (SSIS) 封裝和工作負載移至 Azure 雲端。
-   儲存並管理 SSIS 專案和 Azure SQL Database 的 SSIS 目錄資料庫 (SSISDB) 中的封裝。
-   Azure SSIS 整合執行階段，做為第 2 版的 Azure Data Factory 的一部分導入的執行個體中執行封裝。
-   使用熟悉的工具，例如 SQL Server Management Studio (SSMS) 這些一般工作。

## <a name="benefits"></a>優點
您在內部部署的 SSIS 工作負載移動到 Azure 有下列優點：
-   **降低營運成本**藉由減少內部部署基礎結構。
-   **增加高可用性**具有多個節點，每個叢集，以及 Azure 和 Azure SQL 資料庫的高可用性功能。
-   **提高延展性**指定多個核心每個節點 （向上延展） 和每個叢集 （向外延展） 的多個節點的能力。
-   **避免限制**的 Azure 虛擬機器上執行 SSIS。

## <a name="architecture-overview"></a>架構概觀
下表強調 SSIS 在內部部署與 Azure 上的 SSIS 之間的差異。 最顯著的差異在於分隔運算和儲存體。

| 儲存空間 | 執行階段 | 延展性 |
|---|---|---|
| 在內部部署 (SQL Server) | 由 SQL Server 的 SSIS 執行階段 | SSIS 向外 （在 SQL Server 2017 和更新版本）<br/><br/>自訂解決方案 （在舊版的 SQL Server） |
| 在 Azure (SQL Database) | Azure SSIS 整合執行階段，Azure Data Factory 第 2 版的元件 | SSIS IR 縮放選項 |
| | | |

Azure Data Factory 會裝載在 Azure 上的 SSIS 封裝的執行階段引擎。 在執行階段引擎會呼叫 Azure SSIS 整合執行階段 (SSIS IR)。

當您佈建 SSIS 紅外線遙控器時，您可以向上延展和向外延展藉由指定下列選項的值：
-   節點大小 （包括核心數目） 和叢集中的節點數目。
-   現有的執行個體來主控 SSIS 目錄資料庫 (SSISDB)，以及資料庫的服務層的 Azure SQL Database。
-   每個節點最大平行執行。

您只需要佈建 SSIS IR 一次。 之後，您可以使用熟悉的工具，例如 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 來部署、 設定、 執行、 監視、 排程及管理封裝。

Data Factory 也支援其他類型的整合執行階段。 若要了解有關 SSIS IR 和整合執行階段的其他類型的詳細資訊，請參閱[Azure Data Factory 中的整合執行階段](/azure/data-factory/concepts-integration-runtime.md)。

## <a name="prerequisites"></a>必要條件
本主題中所述的功能需要 SQL Server Data Tools (SSDT) 版本 17.2 或更新版本，但不是需要 SQL Server 2017 或 SQL Server 2016。 當您將封裝部署至 Azure 時，套件部署精靈 」 一律為最新的封裝格式升級的封裝。

如需在 Azure 中的必要條件的詳細資訊，請參閱[增益及 shift SQL Server Integration Services (SSIS) 封裝至 Azure](/azure/data-factory/quickstart-lift-shift-ssis-packages-powershell.md)。

## <a name="ssis-features-on-azure"></a>在 Azure 上的 SSIS 功能

當您佈建到主控 SSISDB 的 SQL Database 的執行個體時，會安裝 Azure Feature Pack，for SSIS，以及存取可轉散發套件。 這些元件提供連線至 Excel 和 Access 檔案和各種不同的 Azure 資料來源。 您無法安裝適用於 SSIS 的協力廠商元件，這一次。

主控 SSISDB 的 SQL 資料庫的名稱會變成您部署和管理封裝，SSDT 和 SSMS-從時所要使用的四部分名稱的第一個部分`<sql_database_name>.database.windows.net`。

您必須使用專案部署模型，而非封裝部署模型，您將部署到 Azure SQL Database 上的 SSISDB 的專案。

您繼續設計和建置封裝內部在 SSDT 中，或在 Visual Studio 中有了 SSDT 安裝。

如需如何從使用 Windows 驗證雲端至內部部署資料來源連接資訊，請參閱[連接到內部部署資料來源使用 Windows 驗證](ssis-azure-connect-with-windows-auth.md)。

## <a name="common-tasks"></a>一般工作

### <a name="provision"></a>佈建
您可以部署，並在 Azure 中執行 SSIS 封裝之前，您必須佈建 SSISDB 目錄資料庫和 Azure SSIS 整合執行階段。 後續的佈建這篇文章中的步驟：[增益及 shift SQL Server Integration Services (SSIS) 封裝至 Azure](/azure/data-factory/quickstart-lift-shift-ssis-packages-powershell.md)。

### <a name="deploy-and-run-packages"></a>部署和執行封裝
若要將專案部署和 SQL Database 上執行封裝，您可以使用數個熟悉的工具和指令碼選項的其中一個：
-   SQL Server Management Studio (SSMS)
-   Transact SQL （從 SSMS 中，Visual Studio 程式碼或其他工具）
-   命令列工具
-   PowerShell
-   C# 和 SSIS 管理物件模型

### <a name="monitor-packages"></a>監視封裝
若要監視執行中的封裝在 SSMS 中，您可以在 SSMS 中使用下列報告工具之一。
-   以滑鼠右鍵按一下**SSISDB**，然後選取**作用中的作業**開啟**作用中的作業** 對話方塊。
-   選取在 [物件總管] 中，以滑鼠右鍵按一下並選取封裝**報表**，然後**標準報表**，然後**所有執行**。

### <a name="schedule-packages"></a>排程封裝
若要排程執行的 SQL 資料庫中儲存的封裝，您可以使用下列工具：
-   SQL Server 代理程式在內部部署
-   資料處理站 SQL Server 預存程序活動

如需詳細資訊，請參閱[排程 SSIS 封裝在 Azure 上的執行](ssis-azure-schedule-packages.md)。

## <a name="next-steps"></a>後續的步驟
若要開始使用 Azure 上的 SSIS 工作負載，請參閱下列文章：
-   [拿起，然後移至 Azure 的 SQL Server Integration Services (SSIS) 封裝](/azure/data-factory/quickstart-lift-shift-ssis-packages-powershell.md)
-   [部署、 執行和監視 Azure 上的 SSIS 封裝](ssis-azure-deploy-run-monitor-tutorial.md)

