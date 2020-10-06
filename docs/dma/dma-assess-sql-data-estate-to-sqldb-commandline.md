---
title: DMACMD：評定 SQL Server 準備好遷移至 Azure SQL
titleSuffix: Data Migration Assistant
description: 瞭解如何使用 Data Migration Assistant 命令列工具 (DMACMD) 來評定要遷移至 Azure SQL 的 SQL Server 資料資產
ms.date: 10/02/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: ''
ms.openlocfilehash: a631ed40344fc8661cef23b9758aa35feb041c45
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91729249"
---
# <a name="dmacmd-assess-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database"></a>DMACMD：評定遷移至 Azure SQL Database SQL Server 資料資產的就緒程度 

有許多組織嘗試遷移至 Azure 時，請務必評估現有的內部部署 SQL Server 實例，並在 Azure Vm 上找出正確的 Azure SQL 目標 Azure SQL Database、Azure SQL 受控執行個體或 SQL Server。 

[Data Migration Assistant (DMA) ](dma-overview.md) 可協助您評估特定 Azure sql 目標的 SQL Server 實例，並量測 SQL Server 資料庫移轉至 Azure sql 的就緒程度。 將 DMA 評定結果上傳至 Azure Migrate 中樞，以取得整個資料資產的集中式就緒程度。 

本文將指導您使用 DMA 命令列介面 (DMACMD) ，大規模執行評量，並將結果上傳至 Azure Migrate hub。 或者，您可以改為使用 [DMA GUI](dma-assess-sql-data-estate-to-sqldb.md) 來執行評量。 

## <a name="prerequisites"></a>必要條件 

若要使用 DMACMD 來執行評量，並將結果上傳至 Azure Migrate hub，您需要下列各項： 

- [Data Migration Assistant (DMA) 的最新版本](https://www.microsoft.com/en-us/download/details.aspx?id=53595)。
- [Azure Migrate 專案](dma-assess-sql-data-estate-to-sqldb.md#create-a-project-and-add-a-tool)。 
- Azure Migrate 專案資源的參與者角色存取權。

## <a name="use-dmacmd"></a>使用 DMACMD

使用 XML 檔案做為輸入，以使用命令列介面 ( # A0) 來大規模執行評量。 

使用下列範例命令將 XML 檔案傳遞至 DMACMD，並開始進行評定：

```console
C:\Program Files\Microsoft Data Migration Assistant\DmaCmd.exe /Action=Assess /AssessmentConfiguration= C:\Demo\ScaleAssessment\Assess-for-AzureSQLMI.xml
```

範例的內容會 `Assess-for-AzureSQLMI.xml` 定義元素，以評估 SQL 受控執行個體目標的 SQL Server 實例： 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<AssessmentConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/AssessmentConfiguration">
   <AssessmentName>Scale-Assessment-for-AzureSQLManagedInstance</AssessmentName>
   <AssessmentSourcePlatform>SqlOnPrem</AssessmentSourcePlatform>
   <AssessmentTargetPlatform>ManagedSqlServer</AssessmentTargetPlatform>
   <AssessmentDatabases>
      <AssessmentDatabase>Server=ServerName\SQL2017;Integrated Security=true</AssessmentDatabase>
      <AssessmentDatabase>Server=ServerName\SQL2016;Integrated Security=true;Initial Catalog=AdventureWorks2016</AssessmentDatabase>
      <AssessmentDatabase>Server=ServerName\SQL2016;Integrated Security=true;Initial Catalog=TestDB</AssessmentDatabase>
   </AssessmentDatabases>
   <AssessmentResultDma>C:\Demo\ScaleAssessment\AssessmentConfiguration\Scale-Assessment-for-AzureSQLManagedInstance.dma</AssessmentResultDma>
   <AssessmentResultJson>C:\Demo\ScaleAssessment\AssessmentConfiguration\Scale-Assessment-for-AzureSQLManagedInstance.json</AssessmentResultJson>
   <AssessmentResultCsv>C:\Demo\ScaleAssessment\AssessmentConfiguration\Scale-Assessment-for-AzureSQLManagedInstance.csv</AssessmentResultCsv>
   <AssessmentOverwriteResult>true</AssessmentOverwriteResult>
   <AssessmentEvaluateCompatibilityIssues>true</AssessmentEvaluateCompatibilityIssues>
   <AssessmentEvaluateFeatureParity>true</AssessmentEvaluateFeatureParity>
   <AzureCloudEnvironment>Azure</AzureCloudEnvironment>
   <SubscriptionId>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxx</SubscriptionId>
   <AzureMigrateProjectName>Scale-Assessment-for-AzureSQLMI</AzureMigrateProjectName>
   <ResourceGroupName>Resource-Group-Name</ResourceGroupName>
   <AzureAuthenticationInteractiveAuthentication>true</AzureAuthenticationInteractiveAuthentication>
   <AzureAuthenticationTenantId>xxxxxxxx-xxxx-xxxxxxxx</AzureAuthenticationTenantId>
   <EnableAssessmentUploadToAzureMigrate>true</EnableAssessmentUploadToAzureMigrate>
</AssessmentConfiguration>
```



## <a name="xml-elements"></a>XML 元素 

傳遞至 DMACMD 的 XML 元素定義于下表中： 


|**XML 元素** |**[定義]**  |
|---------|---------|
|`AssessmentName`|評量的名稱|
|`AssessmentSourcePlatform`|來源 SQL Server 平臺。 預設值是 `SqlOnPrem`。|
|`AssessmentTargetPlatform`|以 SQL Server 平臺為目標。  </br> `AzureSqlDatabase` 適用于 Azure SQL Database 目標。 </br> `ManagedSqlServer` 適用于 Azure SQL 受控執行個體目標。 </br></br>**AzureSQLMI**評估 SQL 受控執行個體目標的評估範例。|
|`AssessmentDatabases`|如果您需要評估實例中的所有資料庫，請只指定實例名稱，否則會列出每一行中的特定資料庫。 </br></br>**AzureSQLMI**評估範例中的所有資料庫 `Servername\SQL2017` ，以及實例中的兩個特定資料庫 `Servername\SQL2016` 。  |
|`AssessmentResultDma` </br> `AssessmentResultJson` </br> `AssessmentResultCsv` | 指定結果檔的格式。 `.DMA`、 `.JSON` 和 `.CSV` 分別。 按兩下 `.DMA` 以在 DMA UI 中開啟。 <br> `AssessmentResultDma` 需要將評量結果上傳至 Azure Migrate hub。  |
|`AssessmentOverwriteResult`| 指出是否要覆寫與或相同路徑的任何現有評定結果 `AssessmentResultJson` 檔 `AssessmentResultDma` `AssessmentResultCsv` 。|
|`AssessmentEvaluateCompatibilityIssues` </br> `AssessmentEvaluateFeatureParity` |執行評量以分別評估相容性問題和功能同位問題。|
|`AzureCloudEnvironment`|要連線的 azure 雲端環境，預設值為 Azure 公用雲端。 </br></br> 支援的值： </br>`Azure (default)`, `AzureChina`, `AzureGermany`, `AzureUSGovernment`.|
|`SubscriptionId`|Azure 訂用帳戶識別碼。|
|`AzureMigrateProjectName`|要上傳評量結果 Azure Migrate 專案名稱。|
|`ResourceGroupName`|Azure Migrate 資源組名。|
|`AzureAuthenticationInteractiveAuthentication`|設定為 `true` 以顯示驗證視窗。|
|`AzureAuthenticationTenantId`|Azure Active Directory 租用戶識別碼。 </br></br>請從[Azure 入口網站](https://portal.azure.com)之 Azure Active Directory 的**總覽**分頁取得這項功能。 |
|`EnableAssessmentUploadToAzureMigrate`| 將設定為， `true` 以將評量結果上傳併發布至 Azure Migrate hub。|
|   |   |


## <a name="results"></a>結果 

DMACMD 成功完成時，會輸出狀態。 


以下是範例結果輸出： 

```console
Assessment finished for project: Scale-Assessment-for-AzureSQLManagedInstance
DATABASES:
Succeeded             : 4
Failed                : 0
SERVER INSTANCES:
Succeeded             : 2
Failed                : 0
CSV result file       : C:\Demo\ScaleAssessment\Scale-Assessment-for-AzureSQLManagedInstance.csv
JSON result file      : C:\Demo\ScaleAssessment\Scale-Assessment-for-AzureSQLManagedInstance.json
--------------------------------------------------------------------------------
```

在 [Azure Migrate](dma-assess-sql-data-estate-to-sqldb.md#view-target-readiness-assessment-results) 中查看上傳的結果，以集中查看整個資料資產。 . 

## <a name="best-practices"></a>最佳作法 

使用 DMACMD 時，請考慮下列最佳做法： 

- 以邏輯方式分組以應用程式為基礎的目標 SQL Server 實例和資料庫，而不是評估整個資料資產中的所有 SQL Server 實例。 
- 為每個 Azure SQL 目標建立個別的 Azure Migrate 專案，以避免覆寫結果。 
- 執行評量的時間取決於資料庫物件的數目。 可能的話，請避免在生產系統上執行評量，並改為卸載至虛擬機器或預備伺服器，尤其是針對具有大量物件的資料庫。 


## <a name="see-also"></a>另請參閱

* [Data Migration Assistant (DMA)](../dma/dma-overview.md) \(英文\)
* [Data Migration Assistant： Configuration settings](../dma/dma-configurationsettings.md)
* [Data Migration Assistant：最佳作法](../dma/dma-bestpractices.md)
