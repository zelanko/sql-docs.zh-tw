---
title: 從命令列執行 Data Migration Assistant
description: 瞭解如何從命令列執行 Data Migration Assistant，以評估 SQL Server 資料庫以進行遷移
ms.custom: seo-lt-2019
ms.date: 05/06/2019
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
ms.openlocfilehash: 3fbf2429a384ad64b1b416e3920a193d92a6c387
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74056620"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>從命令列執行 Data Migration Assistant

在2.1 版和更新版本中，當您安裝 Data Migration Assistant 時，它也會在 *% ProgramFiles%\\Microsoft Data Migration Assistant\\*中安裝 dmacmd。 使用 dmacmd 以自動模式評估您的資料庫，並將結果輸出至 JSON 或 CSV 檔案。 當評估數個資料庫或大型資料庫時，這個方法特別有用。 

> [!NOTE]
> Dmacmd 只支援執行評量。 目前不支援遷移。

## <a name="assessments-using-the-command-line-interface-cli"></a>使用命令列介面（CLI）的評量

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|引數  |描述  | 必要（Y/N）
|---------|---------|---------------|
| `/help or /?`     | 如何使用 dmacmd 的解說文字        | N
|`/AssessmentName`     |   評估專案的名稱   | Y
|`/AssessmentDatabases`     | 以空格分隔的連接字串清單。 資料庫名稱（初始目錄）會區分大小寫。 | Y
|`/AssessmentSourcePlatform`     | 評估的來源平臺： <br>支援的評估值： SqlOnPrem、RdsSqlServer （預設值） <br>支援的目標就緒評估值： SqlOnPrem、RdsSqlServer （預設值）、Cassandra （預覽）   | N
|`/AssessmentTargetPlatform`     | 評量的目標平臺：  <br> 支援的評估值： AzureSqlDatabase、ManagedSqlServer、Q l 2012、SqlServer2014、SqlServer2016、SqlServerLinux2017 和 SqlServerWindows2017 （預設值）  <br> 支援的目標就緒評估值： ManagedSqlServer （預設值）、CosmosDB （預覽）   | N
|`/AssessmentEvaluateFeatureParity`  | 執行功能同位規則。 如果來源平臺為 RdsSqlServer，則目標平臺 AzureSqlDatabase 不支援功能同位評估  | N
|`/AssessmentEvaluateCompatibilityIssues`     | 執行相容性規則  | Y <br> （必須是 AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendations）。
|`/AssessmentEvaluateRecommendations`     | 執行功能建議        | Y <br> （必須是 AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendations）
|`/AssessmentOverwriteResult`     | 覆寫結果檔案    | N
|`/AssessmentResultJson`     | JSON 結果檔案的完整路徑     | Y <br> （必須是 AssessmentResultJson 或 AssessmentResultCsv）
|`/AssessmentResultCsv`    | CSV 結果檔案的完整路徑   | Y <br> （必須是 AssessmentResultJson 或 AssessmentResultCsv）
|`/Action`    | 使用 SkuRecommendation 取得 SKU 建議，使用 AssessTargetReadiness 來執行目標就緒評估。   | N
|`/SourceConnections`    | 以空格分隔的連接字串清單。 [資料庫名稱（初始目錄）] 是選擇性的。 如果未提供任何資料庫名稱，則會評估來源上的所有資料庫。   | Y <br> （如果動作是 ' AssessTargetReadiness '，則為必要）
|`/TargetReadinessConfiguration`    | XML 檔案的完整路徑，描述名稱、來源連接和結果檔案的值。   | Y <br> （必須是 TargetReadinessConfiguration 或 SourceConnections）
|`/FeatureDiscoveryReportJson`    | 功能探索 JSON 報告的路徑。 如果產生此檔案，則它可以在不連線到來源的情況下，用來再次執行目標準備評估。 | N
|`/ImportFeatureDiscoveryReportJson`    | 先前建立之功能探索 JSON 報表的路徑。 不使用來源連接，將會使用這個檔案。   | N

## <a name="examples-of-assessments-using-the-cli"></a>使用 CLI 進行評量的範例

**Dmacmd .exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**使用 Windows 驗證和執行相容性規則的單一資料庫評估**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**使用 SQL Server 驗證和執行功能建議的單一資料庫評估**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;User Id=myUsername;Password=myPassword;"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**目標平臺的單一資料庫評估 SQL Server 2012，將結果儲存至 json 和 .csv 檔案**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2012"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**目標平臺 SQL Azure 資料庫的單一資料庫評估，將結果儲存至 json 和 .csv 檔案**

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

**多資料庫評估**

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

**使用 Windows 驗證的單一資料庫目標就緒評估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"
```

**使用 SQL Server authentication 的單一資料庫目標就緒評估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;User Id=myUsername;Password=myPassword;" /AssessmentEvaluateRecommendations 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json" 

```

**目標平臺 SQL Azure 資料庫的單一資料庫評估，將結果儲存至 json 和 .csv 檔案**

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

**多資料庫目標就緒評估**

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

**使用 Windows 驗證的伺服器上所有資料庫的目標就緒評量**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/SourceConnections="Server=SQLServerInstanceName;Integrated Security=true"
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**藉由匯入稍早建立的功能探索報告來鎖定就緒評估**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/ImportFeatureDiscoveryReportJson="c:\temp\feature_report.json" 
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**藉由提供設定檔的目標就緒性評估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/TargetReadinessConfiguration=.\Config.xml
```

使用來源連接時的設定檔內容：

```
<?xml version="1.0" encoding="utf-8" ?>
<TargetReadinessConfiguration xmlns="https://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
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

匯入功能探索報告時的設定檔內容：

```
<TargetReadinessConfiguration xmlns="https://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```

## <a name="azure-sql-databasemanaged-instance-sku-recommendations-using-the-cli"></a>使用 CLI Azure SQL Database/受控實例 SKU 建議

這些命令支援 Azure SQL Database 單一資料庫和受控實例部署選項的建議。

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true 
```

|引數  |描述  | 必要（Y/N）
|---------|---------|---------------|
|`/Action=SkuRecommendation` | 使用 DMA 命令列執行 SKU 評估 | Y
|`/SkuRecommendationInputDataFilePath` | 從主控資料庫的電腦收集到之效能計數器檔案的完整路徑 | Y
|`/SkuRecommendationTsvOutputResultsFilePath` | TSV 結果檔案的完整路徑 | Y <br> （需要 TSV 或 JSON 或 HTML 檔案路徑）
|`/SkuRecommendationJsonOutputResultsFilePath` | JSON 結果檔案的完整路徑 | Y <br> （需要 TSV 或 JSON 或 HTML 檔案路徑）
|`/SkuRecommendationHtmlResultsFilePath` | HTML 結果檔案的完整路徑 | Y <br> （需要 TSV 或 JSON 或 HTML 檔案路徑）
|`/SkuRecommendationPreventPriceRefresh` | 避免發生價格重新整理。 如果在離線模式下執行（例如 true），請使用。 | Y <br> （針對靜態價格選取此引數，或必須選取下列所有引數以取得最新價格）
|`/SkuRecommendationCurrencyCode` | 要在其中顯示價格的貨幣（例如「美元」） | Y <br> （適用于最新價格）
|`/SkuRecommendationOfferName` | 供應專案名稱（例如 "MS-MS-AZR-0017P-Ms-azr-0003p"）。 如需詳細資訊，請參閱[Microsoft Azure 供應專案詳細資料](https://azure.microsoft.com/support/legal/offer-details/)頁面。 | Y <br> （適用于最新價格）
|`/SkuRecommendationRegionName` | 區功能變數名稱稱（例如 "WestUS"） | Y <br> （適用于最新價格）
|`/SkuRecommendationSubscriptionId` | 訂用帳戶識別碼。 | Y <br> （適用于最新價格）
|`/SkuRecommendationDatabasesToRecommend` | 要建議的資料庫清單（以空格分隔）（例如 "Database1" "Database2" "Database3"）。 名稱區分大小寫，且必須以雙引號括住。 如果省略，則會為所有資料庫提供建議。 | N
|`/AzureAuthenticationTenantId` | 驗證租使用者。 | Y <br> （適用于最新價格）
|`/AzureAuthenticationClientId` | 用於驗證之 AAD 應用程式的用戶端識別碼。 | Y <br> （適用于最新價格）
|`/AzureAuthenticationInteractiveAuthentication` | 設定為 true 會快顯視窗。 | Y <br> （適用于最新價格） <br>（挑選3個驗證選項的其中一個-選項1）
|`/AzureAuthenticationCertificateStoreLocation` | 將設定為憑證存放區位置（例如 "CurrentUser"）。 | Y <br>（適用于最新價格） <br> （挑選3個驗證選項的其中一個-選項2）
|`/AzureAuthenticationCertificateThumbprint` | 設定為憑證指紋。 | Y <br> （適用于最新價格） <br>（挑選3個驗證選項的其中一個-選項2）
|`/AzureAuthenticationToken` | 將設定為憑證 token。 | Y <br> （適用于最新價格） <br>（挑選3個驗證選項的其中一個-選項3）

## <a name="examples-of-sku-assessments-using-the-cli"></a>使用 CLI 進行 SKU 評量的範例

**Dmacmd .exe**

`Dmacmd.exe /? or DmaCmd.exe /help`

**具有價格重新整理的 Azure SQL DB/MI SKU 建議（取得最新價格）-互動式驗證** 

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

**Azure SQL DB/MI SKU 建議與價格更新（取得最新價格）-憑證驗證**

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

**Azure SQL DB SKU/MI 建議與價格重新整理（取得最新價格）-權杖驗證並指定要建議的資料庫**
  
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationDatabasesToRecommend=“TPCDS1G,EDW_3G,TPCDS10G”
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationToken=<Your Authentication Token> 
```

**不需重新整理價格的 Azure SQL DB/MI SKU 建議（使用靜態價格）** 
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
- 本文會[為您的內部部署資料庫識別正確的 AZURE SQL DATABASE SKU](https://aka.ms/dma-sku-recommend-sqldb)。
