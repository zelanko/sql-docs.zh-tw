---
title: "合併 assessment 報表 （SQL Server 資料移轉小幫手） |Microsoft 文件"
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, Assess
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d0dd690a34cf2e4bf5df2d758f65da9b1123506
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="consolidate-assessment-reports-data-migration-assistant"></a>合併的評估報告 （資料移轉小幫手）

您可以使用命令列執行移轉評估在自動模式中，資料移轉小幫手 v2.1 將分別為開頭。 這項功能可協助您執行大規模的評估。  JSON 或 CSV 檔案的形式評估結果。

您可以評估多個資料庫中的資料移轉小幫手的命令列公用程式的單一具現化並匯出到單一的 JSON 檔案中所有的評估結果。 或者，您可以隨時評估一個資料庫，稍後將這些多個 JSON 檔案的結果合併到 SQL 資料庫。

如需如何從命令列執行資料移轉小幫手資訊，請參閱[執行資料移轉小幫手從命令列](../dma/dma-commandline.md)。 


## <a name="import-assessment-results-into-a-sql-server-database"></a>匯入 SQL Server 資料庫的評估結果

使用 PowerShell 指令碼可在此[Github 儲存機制](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)從 JSON 檔案的評估結果匯入至 SQL Server 資料庫。

當您執行指令碼時，您需要提供下列資訊： 

- **serverName**: SQL Server 執行個體名稱，您要匯入評估會產生 JSON 檔案中。

- **databaseName**： 結果取得匯入的資料庫名稱。

- **jsonDirectory**： 評估結果，儲存在一個或多個 JSON 檔案中的資料夾。

- **processTo**: sql Server

上述值區段中，加入 「 執行函式 」，，如下所示。

```
dmaProcessor -serverName localhost \`\
-databaseName DMAReporting \`\
-jsonDirectory "C:\\temp\\DMACmd\\output\\" \`\
-processTo SQLServer
```

PowerShell 指令碼會在您指定的 SQL 執行個體中建立下列物件，如果這些物件原本不存在：

- **資料庫**– PowerShell 參數中提供的名稱

  - 主要的儲存機制

- **資料表**– ReportData

  - 報表的資料

- **資料表**-BreakingChangeWeighting

  - 參考資料表的所有重大變更。  您可以在這裡定義您自己的加權值，以影響更精確的百分比 （%） 升級成功排名。

- **檢視**– UpgradeSuccessRanking\_OnPrem

  - 顯示成功的因素是內部移轉的每個資料庫的檢視。

- **檢視**– UpgradeSuccessRanking\_Azure

  - 顯示成功的因素是內部移轉的每個資料庫的檢視。

- **預存程序**– JSONResults\_插入

  - 用來從 JSON 檔案匯入資料到 SQL Server。

- **預存程序**– AzureFeatureParityResults\_插入

  - 用來從 JSON 檔案的 Azure 功能同位檢查結果匯入至 SQL Server。

- **資料表類型**– JSONResults

  - 用來保存在內部部署評估的 JSON 結果，並將傳遞給 JSONResults\_插入預存程序

- **資料表類型**– AzureFeatureParityResults

  - 用來保存 Azure 的功能同位檢查 azure 的評估結果，並將傳遞給 AzureFeatureParityResults\_插入預存程序

PowerShell 指令碼會建立**處理**目錄內您提供要處理的 JSON 檔案所在的目錄。

在指令碼完成之後，結果會匯入資料表，ReportData。

### <a name="viewing-the-results-in-sql-server"></a>SQL Server 中檢視結果

在載入資料之後，連接到您的 SQL Server 執行個體。 您應該看到下列各項：

![SQL Server 資料庫中的彙總的報告](../dma/media/DMAReportingDatabase.png)

Dbo。ReportData 資料表包含以原始格式的 JSON 檔案的內容。

## <a name="on-premises-upgrade-success-ranking"></a>在內部部署升級成功排名

若要查看資料庫和百分比 （%） 成功陣序的清單，選取 [dbo]。UpgradeSuccessRanking_OnPrem 檢視：

![UpgradeSuccessRaning_OnPrem 檢視中的資料](../dma/media/UpgradeSuccessRankingView.png)

我們可以看到針對給定的資料庫為何不同相容性層級升級成功的機率。  因此，比方說，HR 資料庫已評估相容性層級 100、 110、 120 和 130。  這項評估可協助您以視覺化方式，請參閱投入多少時間時涉及從目前資料庫上目前的版本移轉至較新版的 SQL Server。

通常我們很重視的計量是給定的資料庫會有多少中斷變更。  在上述範例中，我們可以看到 HR 資料庫中的相容性層級 100、 110、 120 和 130 的 50%升級成功因素。

此標準受到改變 dbo 的加權值。BreakingChangeWeighting 資料表。

在下列範例中，修正語法問題 HR 資料庫中所涉及的工作被視為高因此 3 這個值會指派給**投入時間**。 值為 1，因為它不會花費的時間長修正語法問題，要指派給**FixTime**。 值為 2 會有一些成本參與進行變更，因為指派給**成本**。  這會混合的 Changerank 變更為 2。

> [!NOTE]
> 計分是 1-5 標尺上。  1 表示低和 5 變高。 此外，ChangeRank 是計算資料行。

![投入時間、 FixTime 和成本值的語法問題](../dma/media/SyntaxIssueEffort.png)

現在會在此範例，當您查詢 dbo。UpgradeSuccessRanking_OnPrem 檢視已經卸除 HR 資料庫中的重大變更的升級成功因素。

![升級成功因素的 HR 資料庫](../dma/media/UpgradeSuccessFactor_HR.png)

## <a name="azure-upgrade-success-ranking"></a>Azure 升級成功排名

若要查看資料庫移轉至 Azure SQL DB 和成功百分比排名的清單，選取 [dbo]。UpgradeSuccessRanking_Azure 檢視。

![UpgradeSuccessRanking_Azure 檢視中的資料](../dma/media/UpgradeSuccessRankingView_Azure.png)

這裡我們有興趣 MigrationBlocker 值。  賣出 100.00 表示將資料庫移到 Azure SQL Database v12 的 100%成功陣序規範。

與此檢視的差異是，沒有目前的覆寫來變更移轉封鎖規則的加權。

如需使用 Power BI 此資料的報告資訊，請參閱[報告與 PowerBI 合併評估](../dma/dma-powerbiassesreport.md)。


