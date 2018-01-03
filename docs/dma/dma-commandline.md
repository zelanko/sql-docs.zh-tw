---
title: "從命令列執行 （SQL Server 資料移轉小幫手） |Microsoft 文件"
ms.custom: 
ms.date: 09/01/2017
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
helpviewer_keywords: Data Migration Assistant, Command Line
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6147d01802a363082baf27d6b909e2c98f9afef2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>從命令列執行資料移轉小幫手
2.1 版和更新版本，當您安裝資料移轉小幫手，它也會安裝在 dmacmd.exe *%programfiles%\\Microsoft 資料移轉小幫手\\*。 使用 dmacmd.exe 來評估您的資料庫，以自動模式，並輸出結果以 JSON 或 CSV 檔案。 在評估數個資料庫或大型資料庫時，這是特別有用。 

> [!NOTE]
> Dmacmd.exe 支援執行只評估。 在此階段不支援移轉。


## <a name="command-line-arguments"></a>命令列引數

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```


|引數  |描述  | 必要 (Y/N)
|---------|---------|---------------|
| `/help or /?`     | 如何使用 dmacmd.exe 說明文字        | N
|`/AssessmentName`     |   評估專案的名稱   | Y
|`/AssessmentDatabases`     | 以空格分隔的連接字串的清單。 資料庫名稱 （初始目錄） 會區分大小寫。 | Y
|`/AssessmentTargetPlatform`     | 支援的值評估的目標平台： SqlServer2012、 SqlServer2014、 SqlServer2016 和 AzureSqlDatabaseV12。 預設值是 SqlServer2016   | N
|`/AssessmentEvaluateFeatureParity`  | 執行功能同位檢查規則  | N
|`/AssessmentEvaluateCompatibilityIssues`     | 執行相容性規則  | Y <br> （AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendations 是必要）。
|`/AssessmentEvaluateRecommendations`     | 執行功能的建議        | Y <br> （AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendationsis 所需）
|`/AssessmentOverwriteResult`     | 覆寫結果檔案    | N
|`/AssessmentResultJson`     | JSON 結果檔案的完整路徑     | Y <br> （AssessmentResultJson 或 AssessmentResultCsv 是必要）
|`/AssessmentResultCsv`    | CSV 結果檔案的完整路徑   | Y <br>（AssessmentResultJson 或 AssessmentResultCsv 是必要）




## <a name="examples"></a>範例

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**使用 Windows 驗證和執行相容性規則的單一資料庫評估**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***Integrated Security=true*"**
***/AssessmentEvaluateCompatibilityIssues*** /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```



**使用 SQL Server 驗證 」 和 「 執行功能的建議事項的單一資料庫評估**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***User Id=myUsername;Password=myPassword;***"
***/AssessmentEvaluateRecommendations*** /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```


**單一資料庫評估為目標平台的 SQL Server 2012，並將結果儲存至.json 和.csv 檔案**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
***/AssessmentTargetPlatform="SqlServer2012"***
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
***/AssessmentResultJson***="C:\\temp\\Results\\AssessmentReport.json"
***/AssessmentResultCsv***="C:\\temp\\Results\\AssessmentReport.csv"
```


**目標平台的 SQL Azure 資料庫的單一資料庫評估將結果儲存至.json 和.csv 檔案**

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
***/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"***
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```



## <a name="see-also"></a>另請參閱

[資料移轉小幫手下載](https://www.microsoft.com/download/details.aspx?id=53595)
