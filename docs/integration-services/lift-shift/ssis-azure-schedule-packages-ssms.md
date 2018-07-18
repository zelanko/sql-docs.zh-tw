---
title: 使用 SSMS 排程 Azure 中的 SSIS 套件 | Microsoft Docs
description: 描述如何使用 SQL Server Management Studio (SSMS) 中的排程命令，來排程部署到 Azure SQL Database 的 SSIS 套件。
ms.date: 05/09/2018
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
ms.openlocfilehash: d52568b59540ed5a3c4a1111ebf1759f5bdd77f8
ms.sourcegitcommit: 70882926439a63ab9d812809429c63040eb9a41b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36261973"
---
# <a name="schedule-the-execution-of-ssis-packages-deployed-in-azure-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 排程 Azure 中部署的 SSIS 套件執行

您可以使用 SQL Server Management Studio (SSMS) 對部署到 Azure SQL Database 的 SSIS 套件進行排程。 內部部署 SQL Server 和 SQL Database 受控執行個體 (預覽) 分別有作為首要 SSIS 工作排程器的 SQL Server Agent 和受控執行個體代理程式。 相反地，SQL Database 未內建首要 SSIS 工作排程器。 本文所述的 SSMS 功能提供類似於 SQL Server Agent 的熟悉使用者介面，來排程部署到 SQL Database 的套件。

如果您使用 SQL Database 裝載 SSIS 目錄 `SSISDB`，您可以使用此 SSMS 功能，產生排程 SSIS 套件所需的 Data Factory 管線、活動和觸發程序。 稍後，您可以選擇性地編輯並擴充 Data Factory 中的這些物件。

當您使用 SSMS 排程套件時，SSIS 會自動建立三個新的 Data Factory 物件，並根據所選套件的名稱及時間戳記來命名。 例如，如果 SSIS 套件的名稱是 **MyPackage**，SSMS 便會建立類似如下的新 Data Factory 物件：

| Object | [屬性] |
|---|---|
| 管線 | **Pipeline_MyPackage_2018-05-08T09_00_00Z** |
| 執行 SSIS 套件活動 | **Activity_MyPackage_2018-05-08T09_00_00Z** |
| 觸發程序 | **Trigger_MyPackage_2018-05-08T09_00_00Z** |
|||

## <a name="prerequisites"></a>Prerequisites

本文所述的功能需要 SQL Server Management Studio 17.7 版或更高版本。 若要取得最新版的 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)。

## <a name="schedule-a-package-in-ssms"></a>在 SSMS 中排程套件

1. 在 SSMS 的 [物件總管] 中，依序選取 SSISDB 資料庫、資料夾、專案和套件。 以滑鼠右鍵按一下套件，然後選取 [排程]。

    ![選取要排程的套件。](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image1-schedule.png)

2. [新增排程] 對話方塊會隨即開啟。 在 [新增排程] 對話方塊的 [一般] 頁面上，提供新排程工作的名稱和描述。

    ![[新增排程] 對話方塊的 [一般] 頁面](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image2-new-schedule.png)

3. 在 [新增排程] 對話方塊的 [套件] 頁面上，選取選擇性執行階段設定和執行階段環境。

    ![[新增排程] 對話方塊的 [套件] 頁面](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image3-new-schedule2.png)

4. 在 [新增排程] 對話方塊的 [排程] 頁面上，提供排程設定，例如頻率、一天當中的時間和持續時間。

    ![[新增排程] 對話方塊的 [排程] 頁面](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image4-new-schedule3.png)

5. 在 [新增排程] 對話方塊中完成建立工作之後，會出現確認，提醒您 SSMS 即將建立新的 Data Factory 物件。 如果您在確認對話方塊中選取 [是]，則會在 Azure 入口網站中開啟新的 Data Factory 管線，以供您檢閱和自訂。

    ![新排程確認](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image5-confirmation.png)

6. 若要自訂排程觸發程序，請從 [觸發程序] 功能表選取 [新增/編輯]。

    ![選擇性編輯新管線](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image6-edit.png)

    這會開啟 [編輯觸發程序] 刀鋒視窗，以供您自訂排程選項。

    ![編輯觸發程序](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image7-edit2.png)

## <a name="next-steps"></a>後續步驟

若要了解排程 SSIS 套件的其他方法，請參閱[排程 Azure 上的 SSIS 套件執行](ssis-azure-schedule-packages.md)。

若要深入了解 Azure Data Factory 管線、活動和觸發程序，請參閱下列文章：
-   [Azure Data Factory 中的管道及活動](https://docs.microsoft.com/azure/data-factory/concepts-pipelines-activities)
-   [Azure Data Factory 中的管道執行和觸發程序](https://docs.microsoft.com/azure/data-factory/concepts-pipeline-execution-triggers)
