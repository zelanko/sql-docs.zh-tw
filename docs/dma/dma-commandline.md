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
author: rajeshsetlem
ms.author: rajpo
ms.openlocfilehash: a4fdc0343d1346833fd58c4e2fa0240e1a2af668
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950973"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>從命令列執行 Data Migration Assistant

在2.1 版和更新版本中，當您安裝 Data Migration Assistant 時，它也會在 *% ProgramFiles \\ % \\ Microsoft Data Migration Assistant*中安裝 dmacmd.exe。 使用 dmacmd.exe 以自動模式評估您的資料庫，並將結果輸出至 JSON 或 CSV 檔案。 當評估數個資料庫或大型資料庫時，這個方法特別有用。 

> [!NOTE]
> Dmacmd.exe 僅支援執行評量。 目前不支援遷移。

## <a name="assessments-using-the-command-line-interface-cli"></a>使用命令列介面 (CLI) 進行評量

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|引數  |描述  | 必要 (Y/N) 
|---------|---------|---------------|
| `/help or /?`     | 如何使用 dmacmd.exe 解說文字        | N
|`/AssessmentName`     |   評估專案的名稱   | Y
|`/AssessmentDatabases`     | 以空格分隔的連接字串清單。 資料庫名稱 (初始目錄) 區分大小寫。 | Y
|`/AssessmentSourcePlatform`     | 評估的來源平臺： <br>支援的評估值： SqlOnPrem、RdsSqlServer (預設值)  <br>目標就緒評估支援的值： SqlOnPrem、RdsSqlServer (預設) 、Cassandra (preview)    | N
|`/AssessmentTargetPlatform`     | 評量的目標平臺：  <br> 支援的評估值： AzureSqlDatabase、ManagedSqlServer、Q l 2012、SqlServer2014、SqlServer2016、SqlServerLinux2017 和 SqlServerWindows2017 (預設值)   <br> 目標就緒評估支援的值： ManagedSqlServer (預設) ，CosmosDB (preview)    | N
|`/AssessmentEvaluateFeatureParity`  | 執行功能同位規則。 如果來源平臺為 RdsSqlServer，則目標平臺 AzureSqlDatabase 不支援功能同位評估  | N
|`/AssessmentEvaluateCompatibilityIssues`     | 執行相容性規則  | Y <br>  (必須是 AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendations。 ) 
|`/AssessmentEvaluateRecommendations`     | 執行功能建議        | Y <br>  (需要 AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendations) 
|`/AssessmentOverwriteResult`     | 覆寫結果檔案    | N
|`/AssessmentResultJson`     | JSON 結果檔案的完整路徑     | Y <br>  (需要 AssessmentResultJson 或 AssessmentResultCsv) 
|`/AssessmentResultCsv`    | CSV 結果檔案的完整路徑   | Y <br>  (需要 AssessmentResultJson 或 AssessmentResultCsv) 
|`/AssessmentResultDma`    | Dma 結果檔案的完整路徑   | N
|`/Action`    | 使用 SkuRecommendation 取得 SKU 建議。 <br> 使用 AssessTargetReadiness 來執行目標就緒評估。 <br> 使用 AzureMigrateUpload 上傳 AzzessmentResultInputFolder 中的所有 DMA 評估檔案，以大量上傳至 Azure Migrate。動作類型使用方式/Action = AzureMigrateUpload   | N
|`/SourceConnections`    | 以空格分隔的連接字串清單。 資料庫名稱 (初始目錄) 是選擇性的。 如果未提供任何資料庫名稱，則會評估來源上的所有資料庫。   | Y <br> 如果動作是 ' AssessTargetReadiness '，則需要 () 
|`/TargetReadinessConfiguration`    | XML 檔案的完整路徑，描述名稱、來源連接和結果檔案的值。   | Y <br>  (需要 TargetReadinessConfiguration 或 SourceConnections) 
|`/FeatureDiscoveryReportJson`    | 功能探索 JSON 報告的路徑。 如果產生此檔案，則它可以在不連線到來源的情況下，用來再次執行目標準備評估。 | N
|`/ImportFeatureDiscoveryReportJson`    | 先前建立之功能探索 JSON 報表的路徑。 不使用來源連接，將會使用這個檔案。   | N
|`/EnableAssessmentUploadToAzureMigrate`    | 啟用上傳和發佈評估結果至 Azure Migrate   | N
|`/AzureCloudEnvironment`    |選取要連接的 Azure 雲端環境，預設值為 Azure 公用雲端。 支援的值： Azure (預設) 、AzureChina、AzureGermany、AzureUSGovernment。   | N 
|`/SubscriptionId`    |Azure 訂用帳戶識別碼。   | Y <br> 如果指定 EnableAssessmentUploadToAzureMigrate 引數，則需要 () 
|`/AzureMigrateProjectName`    |要上傳評估結果的 Azure Migrate 專案名稱。   | Y <br> 如果指定 EnableAssessmentUploadToAzureMigrate 引數，則需要 () 
|`/ResourceGroupName`    |Azure Migrate 的資源組名。   | Y <br> 如果指定 EnableAssessmentUploadToAzureMigrate 引數，則需要 () 
|`/AssessmentResultInputFolder`    |包含的輸入資料夾路徑。要上傳至 Azure Migrate 的 DMA 評估檔案。   | Y <br> AzureMigrateUpload 動作時需要 () 



## <a name="examples-of-assessments-using-the-cli"></a>使用 CLI 進行評量的範例

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

**目標平臺的單一資料庫評估 Azure SQL Database，將結果儲存至 json 和 .csv 檔案**

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

**目標平臺的單一資料庫評估 Azure SQL Database，將結果儲存至 json 和 .csv 檔案**

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

匯入功能探索報告時的設定檔內容：

```
<TargetReadinessConfiguration xmlns="https://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```
**評估並上傳至 Azure 公用雲端中的 Azure Migrate (預設) **
```
DmaCmd.exe
/Action="Assess" 
/AssessmentSourcePlatform=SqlOnPrem 
/AssessmentTargetPlatform=ManagedSqlServer
/AssessmentEvaluateCompatibilityIssues 
/AssessmentEvaluateRecommendations 
/AssessmentEvaluateFeatureParity 
/AssessmentOverwriteResult 
/AssessmentName="assess-myDatabase"
/AssessmentDatabases="Server=myServer;Initial Catalog=myDatabase;Integrated Security=true" 
/AssessmentResultDma="C:\assessments\results\assess-1.dma"
/SubscriptionId="Subscription Id" 
/AzureMigrateProjectName="Azure Migrate project ame" 
/ResourceGroupName="Resource Group name" 
/AzureAuthenticationInteractiveAuthentication
/AzureAuthenticationTenantId="Azure Tenant Id"
/EnableAssessmentUploadToAzureMigrate

```
**Batch 將 DMA 評估檔案上傳至 Azure 公用雲端中的 Azure Migrate (預設) **
```
DmaCmd.exe 
/Action="AzureMigrateUpload" 
/AssessmentResultInputFolder="C:\assessments\results" 
/SubscriptionId="Subscription Id" 
/AzureMigrateProjectName="Azure Migrate project name" 
/ResourceGroupName="Resource Group name" 
/AzureAuthenticationInteractiveAuthentication
/AzureAuthenticationTenantId="Azure Tenant Id"
/EnableAssessmentUploadToAzureMigrate

```
## <a name="azure-sql-database--azure-sql-managed-instance-sku-recommendations-using-the-cli"></a>使用 CLI Azure SQL Database/Azure SQL 受控執行個體 SKU 建議

這些命令支援 Azure SQL Database 單一資料庫和 Azure SQL 受控執行個體部署選項的建議。

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true 
```

|引數  |描述  | 必要 (Y/N) 
|---------|---------|---------------|
|`/Action=SkuRecommendation` | 使用 DMA 命令列執行 SKU 評估 | Y
|`/SkuRecommendationInputDataFilePath` | 從主控資料庫的電腦收集到之效能計數器檔案的完整路徑 | Y
|`/SkuRecommendationTsvOutputResultsFilePath` | TSV 結果檔案的完整路徑 | Y <br>  (需要 TSV 或 JSON 或 HTML 檔案路徑) 
|`/SkuRecommendationJsonOutputResultsFilePath` | JSON 結果檔案的完整路徑 | Y <br>  (需要 TSV 或 JSON 或 HTML 檔案路徑) 
|`/SkuRecommendationHtmlResultsFilePath` | HTML 結果檔案的完整路徑 | Y <br>  (需要 TSV 或 JSON 或 HTML 檔案路徑) 
|`/SkuRecommendationPreventPriceRefresh` | 避免發生價格重新整理。 如果以離線模式執行 (例如 true) ，請使用。 | Y <br>  (為靜態價格選取此引數，或必須選取下列所有引數，才能取得最新的價格) 
|`/SkuRecommendationCurrencyCode` | 要在其中顯示價格 (例如「美元」的貨幣 )  | Y <br> 最新價格的 () 
|`/SkuRecommendationOfferName` | 供應專案名稱 (例如 "MS-AZR-0017P-Ms-azr-0003p" ) 。 如需詳細資訊，請參閱[Microsoft Azure 供應專案詳細資料](https://azure.microsoft.com/support/legal/offer-details/)頁面。 | Y <br> 最新價格的 () 
|`/SkuRecommendationRegionName` | 區功能變數名稱稱 (例如 "WestUS" )  | Y <br> 最新價格的 () 
|`/SkuRecommendationSubscriptionId` | 訂閱識別碼。 | Y <br> 最新價格的 () 
|`/SkuRecommendationDatabasesToRecommend` |  (的以空格分隔的資料庫清單，例如 "Database1" "Database2" "Database3" ) 。 名稱區分大小寫，且必須以雙引號括住。 如果省略，則會為所有資料庫提供建議。 | N
|`/AzureAuthenticationTenantId` | 驗證租使用者。 | Y <br> 最新價格的 () 
|`/AzureAuthenticationClientId` | 用於驗證之 Azure AD 應用程式的用戶端識別碼。 | Y <br> 最新價格的 () 
|`/AzureAuthenticationInteractiveAuthentication` | 設定為 true 會快顯視窗。 | Y <br> 最新價格的 ()  <br> (挑選3個驗證選項之一-選項 1) 
|`/AzureAuthenticationCertificateStoreLocation` | 將設定為憑證存放區位置 (例如 "CurrentUser" ) 。 | Y <br>最新價格的 ()  <br>  (挑選3個驗證選項之一-選項 2) 
|`/AzureAuthenticationCertificateThumbprint` | 設定為憑證指紋。 | Y <br> 最新價格的 ()  <br> (挑選3個驗證選項之一-選項 2) 
|`/AzureAuthenticationToken` | 將設定為憑證 token。 | Y <br> 最新價格的 ()  <br> (挑選3個驗證選項之一-選項 3) 

## <a name="examples-of-sku-assessments-using-the-cli"></a>使用 CLI 進行 SKU 評量的範例

**Dmacmd.exe**

`Dmacmd.exe /? or DmaCmd.exe /help`

**Azure SQL Database/Azure SQL 受控執行個體 SKU 建議與價格重新整理 (取得最新價格) -互動式驗證** 

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

**Azure SQL Database/Azure SQL 受控執行個體 SKU 建議與價格重新整理 (取得最新價格) -憑證驗證**

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

**Azure SQL Database/Azure SQL 受控執行個體使用價格重新整理的建議 (取得最新價格) 權杖驗證，並指定要建議的資料庫**
  
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

**Azure SQL Database/Azure SQL 受控執行個體 SKU 建議（不含價格更新） (使用靜態價格) ** 
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
