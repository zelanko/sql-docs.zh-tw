---
title: 匯入和合併資料移轉小幫手評定報告 (SQL Server) |Microsoft Docs
description: 了解如何從 Data Migration Assistant 將評定報表匯入到 SQL Server 資料庫，以及合併多個報表
ms.custom: ''
ms.date: 04/16/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: be9fc224093f0d5ae14372d4674a52589a2d4801
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37781769"
---
# <a name="import-and-consolidate-data-migration-assistant-assessment-reports"></a>匯入和合併資料移轉小幫手評定報告

若要開始使用 Data Migration Assistant v2.1 將分別在自動模式中，執行移轉評估，您可以使用命令列。 這項功能可協助您執行大規模的評量。 評估結果的 JSON 或 CSV 檔案形式。

您可以評估資料移轉小幫手的命令列公用程式的單一具現化中的多個資料庫，並將所有的評估結果匯出到單一 JSON 檔案。 或者，您可以隨時評估一個資料庫，並稍後將這些多個 JSON 檔案的結果合併到 SQL database。

如需如何從命令列執行 Data Migration Assistant 的詳細資訊，請參閱[執行 Data Migration Assistant 從命令列](../dma/dma-commandline.md)。 

## <a name="import-assessment-results-into-a-sql-server-database"></a>評估結果匯入至 SQL Server 資料庫

使用此 PowerShell 指令碼[Github 存放庫](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)JSON 檔案中的評估結果匯入至 SQL Server 資料庫。

> [!NOTE]
> PowerShell v5 或更高的需要。

當您執行指令碼時，您需要提供下列資訊： 

- **serverName**： 從 JSON 檔案會產生您想要匯入評估 SQL Server 執行個體名稱。

- **databaseName**： 若要匯入結果的資料庫名稱。

- **jsonDirectory**： 評估結果，儲存在一或多個 JSON 檔案的資料夾。

- **processTo**: SQLServer

將先前的值，如下所示新增 「 執行函式 」 一節中。

```
dmaProcessor -serverName localhost \`\
-databaseName DMAReporting \`\
-jsonDirectory "C:\\temp\\DMACmd\\output\\" \`\
-processTo SQLServer
```

PowerShell 指令碼在您指定的 SQL 執行個體中建立下列物件，如果這些物件原本不存在：

- **資料庫**– PowerShell 參數中提供的名稱

  - 主要存放庫

- **資料表**– ReportData

  - 報表的資料

- **資料表**-BreakingChangeWeighting

  - 如需所有的重大變更的參考資料表。 您可以在這裡定義您自己的加權值，以影響更精確的百分比 （%） 升級成功排名。

- **檢視**– UpgradeSuccessRanking\_OnPrem

  - 顯示成功的因素，針對要移轉內部部署的每個資料庫的檢視。

- **檢視**– UpgradeSuccessRanking\_Azure

  - 顯示成功的因素，針對要移轉內部部署的每個資料庫的檢視。

- **預存程序**– JSONResults\_插入

  - 用來從 JSON 檔案匯入資料到 SQL Server。

- **預存程序**– AzureFeatureParityResults\_插入

  - 用來從 JSON 檔案的 Azure 功能同位檢查結果匯入至 SQL Server。

- **資料表類型**– JSONResults

  - 用來保存 JSON 結果，如在內部評估並將傳遞給 JSONResults\_插入預存程序

- **資料表類型**– AzureFeatureParityResults

  - 用來保存 Azure 功能的 azure 評量的同位檢查結果，並將傳遞給 AzureFeatureParityResults\_插入預存程序

PowerShell 指令碼會建立**處理**目錄內您所提供，其中包含所要處理的 JSON 檔案的目錄。

指令碼完成之後，結果會匯入至資料表，ReportData。

### <a name="viewing-the-results-in-sql-server"></a>SQL Server 中檢視結果

在載入資料之後，連線到您的 SQL Server 執行個體。 您的畫面應該會出現，如下圖所示：

![SQL Server 資料庫中的彙總的報表](../dma/media/DMAReportingDatabase.png)

Dbo。ReportData 資料表會包含 JSON 檔案，以其原始格式的內容。

## <a name="on-premises-upgrade-success-ranking"></a>在內部部署升級成功排名

若要查看的資料庫和其百分比 （%） 成功排名清單，選取 [dbo]。UpgradeSuccessRanking_OnPrem 檢視：

![UpgradeSuccessRaning_OnPrem 檢視中的資料](../dma/media/UpgradeSuccessRankingView.png)

這裡您可以看到對於給定的資料庫為何不同的相容性層級的升級成功機會。 因此，比方說，HR 資料庫已通過相容性層級 100、 110、 120 和 130。 這項評估可協助您以視覺化方式，請參閱投入參與從目前資料庫位於目前的版本移轉至新版的 SQL Server。

通常您關心的計量是有幾個重大變更會針對給定的資料庫。 在上述範例中，您可以看到 HR 資料庫的相容性層級 100、 110、 120 和 130 的 50%升級成功因素。

此計量可以受到改變 dbo 的加權值。BreakingChangeWeighting 資料表。

在下列範例中，在 HR 資料庫中修正的語法問題所涉及的工作會被視為高因此 3 這個值會指派給**努力**。 值為 1，因為它不需要很長，若要修正語法問題，要指派給**FixTime**。 值為 2，因為會有一些成本參與進行變更，要指派給**成本**。 使用此值變更為 2 的混合的 Changerank。

> [!NOTE]
> 計分是範圍為 1 到 5。  1 個低，而 5 是高。 此外，ChangeRank 是計算資料行。

![投入時間、 FixTime 和成本值的語法問題](../dma/media/SyntaxIssueEffort.png)

現在在此範例，當您查詢 dbo。UpgradeSuccessRanking_OnPrem 檢視中，已卸除 HR 資料庫中的重大變更的升級成功因素。

![HR 資料庫升級成功的因素](../dma/media/UpgradeSuccessFactor_HR.png)

## <a name="azure-upgrade-success-ranking"></a>Azure 的升級成功排名

若要查看的資料庫移轉至 Azure SQL DB 和成功百分比排名清單，選取 dbo。UpgradeSuccessRanking_Azure 檢視中。

![UpgradeSuccessRanking_Azure 檢視中的資料](../dma/media/UpgradeSuccessRankingView_Azure.png)

這裡您感興趣的 MigrationBlocker 值。 100.00 表示會將資料庫移至 Azure SQL Database v12 的 100%成功陣序規範。

與此檢視的差異是，目前沒有變更的加權都會移轉封鎖程式 」 規則的覆寫。

如需使用 Power BI 的這個資料的報告資訊，請參閱[power Bi 與您合併評定報告](../dma/dma-powerbiassesreport.md)。
