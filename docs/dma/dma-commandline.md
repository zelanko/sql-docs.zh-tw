---
title: 執行 Data Migration Assistant，從命令列 (SQL Server) |Microsoft Docs
description: 了解如何從命令列來評估要移轉的 SQL Server 資料庫執行 Data Migration Assistant
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Command Line
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: ec274af1b3674cb821f0f5a477d1f798c404000e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63154672"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>從命令列執行 Data Migration Assistant
2.1 版和更新版本，當您安裝 Data Migration Assistant，它也會安裝在 dmacmd.exe *%programfiles%\\Microsoft Data Migration Assistant\\*。 使用 dmacmd.exe 來評估您的資料庫，以自動模式，並輸出結果以 JSON 或 CSV 檔案。 評估多個資料庫或大量資料庫時，這個方法會特別有用。 

> [!NOTE]
> Dmacmd.exe 支援只執行評量。 在此階段不支援移轉。


## <a name="assessments-using-the-command-line-interface-cli"></a>使用命令列介面 (CLI) 的評量

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|引數  |描述  | 必要 （是/否）
|---------|---------|---------------|
| `/help or /?`     | 如何使用 dmacmd.exe 說明文字        | N
|`/AssessmentName`     |   評估專案的名稱   | Y
|`/AssessmentDatabases`     | 連接字串的以逗號分隔清單。 資料庫名稱 （初始類別目錄） 會區分大小寫。 | Y
|`/AssessmentSourcePlatform`     | 評定的原始碼平台： <br>評估為支援的值：SqlOnPrem，RdsSqlServer （預設值） <br>支援目標整備性評估的值：SqlOnPrem RdsSqlServer （預設）、 Cassandra （預覽版）   | N
|`/AssessmentTargetPlatform`     | 評估的目標平台：  <br> 評估為支援的值：AzureSqlDatabase、 ManagedSqlServer、 SqlServer2012、 SqlServer2014、 SqlServer2016、 SqlServerLinux2017 和 SqlServerWindows2017 （預設值）  <br> 支援目標整備性評估的值：ManagedSqlServer （預設）、 CosmosDB （預覽）   | N
|`/AssessmentEvaluateFeatureParity`  | 執行功能同位規則。 如果 RdsSqlServer 原始碼平台，功能同位檢查評估不支援目標平台 AzureSqlDatabase  | N
|`/AssessmentEvaluateCompatibilityIssues`     | 執行相容性規則  | Y <br> （AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendations 是必要）。
|`/AssessmentEvaluateRecommendations`     | 執行功能建議        | Y <br> （AssessmentEvaluateCompatibilityIssues 或所需的 AssessmentEvaluateRecommendationsis）
|`/AssessmentOverwriteResult`     | 覆寫結果檔案    | N
|`/AssessmentResultJson`     | JSON 結果檔案的完整路徑     | Y <br> （AssessmentResultJson 或 AssessmentResultCsv 是必要的）
|`/AssessmentResultCsv`    | CSV 結果檔案的完整路徑   | Y <br>（AssessmentResultJson 或 AssessmentResultCsv 是必要的）
|`/Action`    | 若要取得 SKU 的建議，請使用 AssessTargetReadiness 執行目標整備性評估使用 SkuRecommendation。   | N
|`/SourceConnections`    | 以空格分隔的連接字串的清單。 資料庫名稱 (Initial Catalog) 是選擇性的。 如果沒有提供資料庫名稱時，會評估來源上的所有資料庫。   | Y <br>（必要動作是否 'AssessTargetReadiness'）
|`/TargetReadinessConfiguration`    | 描述名稱、 來源連接和結果檔案的 XML 檔案的完整路徑。   | Y <br>（TargetReadinessConfiguration 或 SourceConnections 是必要的）
|`/FeatureDiscoveryReportJson`    | 功能探索 JSON 報表路徑。 如果產生此檔案，它可以用來重新執行目標整備性評估，而不需要連線到來源。   | N
|`/ImportFeatureDiscoveryReportJson`    | 功能探索 JSON 報告稍早建立的路徑。 而不是來源連接，就會使用這個檔案。   | N

## <a name="examples-of-assessments-using-the-cli"></a>使用 CLI 的評量的範例

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**使用 Windows 驗證和執行相容性規則的單一資料庫評估**


```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**使用 SQL Server 驗證 」 和 「 執行功能的建議事項的單一資料庫評估**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;User Id=myUsername;Password=myPassword;"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**單一資料庫評估目標平台 SQL Server 2012 中，將結果儲存至.json 和.csv 檔案**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2012"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**單一資料庫評估目標平台 SQL Azure 資料庫中，將結果儲存至.json 和.csv 檔案**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="AzureSqlDatabaseV12"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"
```

**多個資料庫評估**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```

**使用 Windows 驗證的單一資料庫目標整備性評估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"
```

**使用 SQL Server 驗證的單一資料庫目標整備性評估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;User Id=myUsername;Password=myPassword;" /AssessmentEvaluateRecommendations 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json" 

```

**單一資料庫評估目標平台 SQL Azure 資料庫中，將結果儲存至.json 和.csv 檔案**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentSourcePlatform="SqlOnPrem"
/AssessmentTargetPlatform="AzureSqlDatabase"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"

```

**多個資料庫目標整備性評估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/AssessmentSourcePlatform=SourcePlatform
/AssessmentTargetPlatform=TargetPlatform
/SourceConnections="Server=SQLServerInstanceName1;Initial Catalog=DatabaseName1;Integrated Security=true" "Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated Security=true" "Server=SQLServerInstanceName2;Initial Catalog=DatabaseName3;Integrated Security=true" 
/AssessmentOverwriteResult  
/AssessmentResultJson="C:\Results\test2016.json"

(/AssessmentSourcePlatform and /AssessmentTargetPlatform are optional.)
```

**使用 Windows 驗證的伺服器上的所有資料庫的目標整備性評估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**藉由匯入稍早建立的功能探索報告的目標整備性評估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/ImportFeatureDiscoveryReportJson="c:\temp\feature_report.json" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**藉由提供組態檔的目標整備性評估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/TargetReadinessConfiguration=.\Config.xml

```
使用時，組態檔內容來源連接：
```
<?xml version="1.0" encoding="utf-8" ?>
<TargetReadinessConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <SourcePlatform>Source Platform</SourcePlatform> <!-- Optional. The default is SqlOnPrem -->
  <TargetPlatform>TargetPlatform</TargetPlatform> <!-- Optional. The default is ManagedSqlServer -->
  <SourceConnections>
    <SourceConnection>connection string 1</SourceConnection>
    <SourceConnection>connection string 2</SourceConnection>
    <!-- ... -->
    <SourceConnection>connection string n</SourceConnection>
  </SourceConnections>
  <AssessmentResultJson>path\to\file.json</AssessmentResultJson>
  <FeatureDiscoveryReportJson>path\to\featurediscoveryreport.json</FeatureDiscoveryReportJson>
  <OverwriteResult>true</OverwriteResult> <!-- or false -->
</TargetReadinessConfiguration>
```

組態檔案內容匯入功能探索報告時：
```
<TargetReadinessConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```

## <a name="azure-sql-database-sku-recommendations-using-the-cli"></a>使用 CLI 的 azure SQL 資料庫 SKU 建議

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true 
```

|引數  |描述  | 必要 （是/否）
|---------|---------|---------------|
|`/Action=SkuRecommendation` | 執行使用 DMA 命令列的 SKU 評量 | Y
|`/SkuRecommendationInputDataFilePath`  | 從主控資料庫的電腦收集的效能計數器檔案完整路徑 |    Y
|`/SkuRecommendationTsvOutputResultsFilePath`   | TSV 結果檔案的完整路徑 |    Y <br>（TSV 或 JSON 或 HTML 檔案的路徑是必要的）
|`/SkuRecommendationJsonOutputResultsFilePath`  | JSON 結果檔案的完整路徑 |   Y <br>（TSV 或 JSON 或 HTML 檔案的路徑是必要的）
|`/SkuRecommendationHtmlResultsFilePath` |  HTML 結果檔案的完整路徑 | Y <br>（TSV 或 JSON 或 HTML 檔案的路徑是必要的）
|`/SkuRecommendationPreventPriceRefresh` |  價格重新整理可防止發生。 如果在離線模式中執行，請使用。 |    Y <br>（這個引數選取靜態價格或下列所有引數，就必須選取來取得最新價格）
|`/SkuRecommendationCurrencyCode` | 要顯示的價格 （例如貨幣「 USD") | Y <br>（如果您想要取得最新的價格）
|`/SkuRecommendationOfferName` |    供應項目名稱 （例如："MS-AZR-0003 P")。 如需詳細資訊，請參閱 < [Microsoft Azure 優惠詳細資料](https://azure.microsoft.com/support/legal/offer-details/)頁面。 |   Y <br>（如果您想要取得最新的價格）
|`/SkuRecommendationRegionName` |   區域名稱 （例如：「 美國西部 」） |   Y <br>（如果您想要取得最新的價格）
|`/SkuRecommendationSubscriptionId` | 訂閱識別碼。 |    Y <br>（如果您想要取得最新的價格）
|`/AzureAuthenticationTenantId` | 驗證租用戶中。 |  Y <br>（如果您想要取得最新的價格）
|`/AzureAuthenticationClientId` | 用於驗證的 AAD 應用程式的用戶端識別碼。 | Y <br>（如果您想要取得最新的價格）
|`/AzureAuthenticationInteractiveAuthentication`    | 設定為 true，快顯視窗。 |   Y <br>（如果您想要取得最新的價格） <br>（選擇其中一個 3 個驗證選項-選項 1）
|`/AzureAuthenticationCertificateStoreLocation` | 設定憑證存放區位置 （例如：「 CurrentUser")。 | Y <br>（如果您想要取得最新的價格） <br>（選擇其中一個 3 個驗證選項-選項 2）
|`/AzureAuthenticationCertificateThumbprint`    | 設定憑證指紋。 | Y <br>（如果您想要取得最新的價格） <br>（選擇其中一個 3 個驗證選項-選項 2）
|`/AzureAuthenticationToken` |  設定憑證的語彙基元。 | Y <br>（如果您想要取得最新的價格） <br>（選擇其中一個 3 個驗證選項-選項 3）

## <a name="examples-of-sku-assessments-using-the-cli"></a>使用 CLI 的 SKU 評量的範例

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Azure SQL DB SKU 建議價格重新整理 （取得最新的價格）-使用互動式驗證** 
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationInteractiveAuthentication=true 
```

**Azure SQL DB SKU 建議價格更新 （取得最新的價格）-憑證驗證**
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationCertificateStoreLocation=<Your Certificate Store Location>
/AzureAuthenticationCertificateThumbprint=<Your Certificate Thumbprint>  
```

**Azure SQL DB SKU 建議價格更新 （取得最新的價格）-k 驗證**  
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationToken=<Your Authentication Token> 
```

**Azure SQL DB SKU 建議，而不需要價格重新整理 （使用靜態的價格）** 
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true  
```

## <a name="see-also"></a>另請參閱
- [Data Migration Assistant](https://aka.ms/get-dma)下載。
- 發行項[找出您的內部部署資料庫正確的 Azure SQL 資料庫 SKU](https://aka.ms/dma-sku-recommend-sqldb)。
