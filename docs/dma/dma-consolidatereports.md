---
title: 使用 Data Migration Assistant 評估企業和合併評估報告
description: 瞭解如何在升級 SQL Server 或遷移至 Azure SQL Database 之前，使用 DMA 評估企業和合併評量報告。
ms.date: 06/21/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: dd3b2d26b79cf612c18a201a2b077323b1b68420
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823240"
---
# <a name="assess-an-enterprise-and-consolidate-assessment-reports-with-dma"></a>使用 DMA 評估企業及整合評估報告

下列逐步指示可協助您使用 Data Migration Assistant 來執行成功調整規模的評估，以升級內部部署 SQL Server 或 Azure Vm 上執行的 SQL Server，或遷移至 Azure SQL Database。

## <a name="prerequisites"></a>必要條件

- 指定您網路上將從中起始 DMA 的工具電腦。 確定這部電腦可連線到您的 SQL Server 目標。
- 下載與安裝：
  - [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) 3.6 或更新版本。
  - [PowerShell](https://aka.ms/wmf5download) 5.0 版或更新版本。
  - [.NET Framework](https://www.microsoft.com/download/details.aspx?id=30653) 4.5 或更新版本。
  - [SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.0 或更新版本。
  - [Power BI 桌面](/power-bi/fundamentals/desktop-get-the-desktop)]。
  - [Azure PowerShell 模組](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.0.0)
- 下載並解壓縮：
  - [DMA 會報告 Power BI 範本](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/161/2/PowerBI-Reports.zip)。
  - [LoadWarehouse 腳本](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/161/3/LoadWarehouse1.zip)。

## <a name="loading-the-powershell-modules"></a>載入 PowerShell 模組

將 PowerShell 模組儲存至 PowerShell 模組目錄，可讓您呼叫模組，而不需要在使用之前明確載入它們。

若要載入模組，請執行下列步驟：

1. 流覽至 C:\Program Files\WindowsPowerShell\Modules，然後建立名為**DataMigrationAssistant**的資料夾。
2. 開啟[PowerShell 模組](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/161/1/PowerShell-Modules2.zip)，然後將它們儲存到您建立的資料夾中。

      ![PowerShell 模組](../dma/media//dma-consolidatereports/dma-powershell-modules.png)

    每個資料夾都包含相關聯的 .psm1 檔案，如下圖所示：

   ![PowerShell 模組 .psm1 檔](../dma/media//dma-consolidatereports/dma-powershell-modules-psm1-files.png)

   > [!NOTE]
   > 其包含的資料夾和 .psm1 檔案必須具有相同的名稱。

   > [!IMPORTANT]
   > 將 PowerShell 檔案儲存到 WindowsPowerShell 目錄之後，您可能需要解除封鎖這些檔案，以確保模組正確載入。 若要解除封鎖 PowerShell 檔案，請在檔案上按一下滑鼠右鍵，選取 [**屬性**]，選取 [**解除封鎖**] 文字方塊，然後選取 **[確定]**。

   ![.psm1 檔案屬性](../dma/media//dma-consolidatereports/dma-psm1-file-properties.png)

    PowerShell 現在應該會在新的 PowerShell 會話啟動時自動載入這些模組。

## <a name="create-an-inventory-of-sql-servers"></a><a name="create-inventory"></a>建立 SQL Server 的清查

執行 PowerShell 腳本來評估您的 SQL Server 之前，您必須先建立要評估的 SQL Server 清查。

此清查可以是下列兩種形式的其中一種：

- Excel CSV 檔案
- SQL Server 資料表

### <a name="if-using-a-csv-file"></a>如果使用 CSV 檔案

> [!IMPORTANT]
> 請確定清查檔案儲存為逗號分隔 (CSV) 檔。
>
> 若為預設實例，請將實例名稱設定為 MSSQLServer。

當您使用 csv 檔案匯入資料時，請確定只有兩個數據行的資料**實例名稱**和**資料庫名稱**，而且資料行沒有標題列。

 ![csv 檔案內容](../dma/media//dma-consolidatereports/dma-csv-file-contents.png)

### <a name="if-using-a-sql-server-table"></a>如果使用 SQL Server 資料表

> [!IMPORTANT]
> 若為預設實例，請將實例名稱設定為 MSSQLServer。

建立名為**EstateInventory**的資料庫和名為**DatabaseInventory**的資料表。 包含此清查資料的資料表可以有任意數目的資料行，只要有下列四個數據行：

- ServerName
- InstanceName
- DatabaseName
- AssessmentFlag

![SQL Server 資料表內容](../dma/media//dma-consolidatereports/dma-sql-server-table-contents-database-inventory.png)

如果此資料庫不在工具電腦上，請確定工具電腦具有與此 SQL Server 實例的網路連線。

在 CSV 檔案上使用 SQL Server 資料表的優點是，您可以使用 [評估旗標] 資料行來控制所收取的實例/資料庫，以供評估之用，讓您更輕鬆地將評量分成較小的區塊。  接著，您可以跨越多個評量 (參閱本文稍後的執行評估一節) ，這比維護多個 CSV 檔案更容易。

請記住，視物件的數目及其複雜度而定，評估可能會花很長的時間 (時數 +) ，因此將評量分成可管理的區塊是謹慎的。

### <a name="if-using-an-instance-inventory"></a>如果使用實例清查

建立名為**EstateInventory**的資料庫和名為**InstanceInventory**的資料表。 包含此清查資料的資料表可以有任意數目的資料行，只要有下列四個數據行：

- ServerName
- InstanceName
- 連接埠
- AssessmentFlag

![SQL Server 資料表內容](../dma/media//dma-consolidatereports/dma-sql-server-table-contents-instance-inventory.png)

## <a name="running-a-scaled-assessment"></a>執行調整規模的評估

將 PowerShell 模組載入至模組目錄並建立清查之後，您必須開啟 PowerShell 並執行 dmaDataCollector 函式，以執行調整的評估。

  ![dmaDataCollector 函數清單](../dma/media//dma-consolidatereports/dma-dmaDataCollector-function-listing.png)

下表說明與 dmaDataCollector 函數相關聯的參數。

|參數  |描述 |
|---------|---------|
|**getServerListFrom** | 您的清查。 可能的值為**SqlServer**和**CSV**。<br/>如需詳細資訊，請參閱[建立 SQL server 的清查](#create-inventory)。 |
|**csvPath** | CSV 清查檔案的路徑。  只有在**getServerListFrom**設定為**CSV**時才會使用。 |
|**serverName** | 在**getServerListFrom**參數中使用**SqlServer**時，清查的 SQL Server 實例名稱。 |
|**名稱** | 主控清查資料表的資料庫。 |
|**useInstancesOnly** | 位旗標，用來指定是否要使用實例的清單進行評估。  如果設定為0，則會使用 DatabaseInventory 資料表來建立評量目標清單。 |
|**AssessmentName** | DMA 評估的名稱。 |
|**TargetPlatform** | 您想要執行的評量目標型別。  可能的值為**AzureSQLDatabase**、 **ManagedSqlServer**、 **q l 2012**、 **SQLServer2014**、 **SQLServer2016**、 **SQLServerLinux2017**、 **SQLServerWindows2017**、 **SqlServerWindows2019**和**SqlServerLinux2019**。  |
|**AuthenticationMethod** | 用來連接到您想要評估之 SQL Server 目標的驗證方法。 可能的值為**SQLAuth**和**WindowsAuth**。 |
|**OutputLocation** | 要在其中儲存 JSON 評估輸出檔案的目錄。 根據要評估的資料庫數目和資料庫內的物件數目而定，評量可能會花很長的時間。 檔案將會在所有評量完成後寫入。 |

如果發生未預期的錯誤，則會終止由這個進程起始的命令視窗。  請檢查錯誤記錄檔，以判斷失敗的原因。

  ![錯誤記錄檔位置](../dma/media//dma-consolidatereports/dma-error-log-file-location.png)

## <a name="consuming-the-assessment-json-file"></a>使用評估 JSON 檔案

評估完成後，您就可以開始將資料匯入 SQL Server 以進行分析。 若要使用評估 JSON 檔案，請開啟 PowerShell 並執行 dmaProcessor 函式。

  ![dmaProcessor 函式清單](../dma/media//dma-consolidatereports/dma-dmaProcessor-function-listing.png)

下表說明與 dmaProcessor 函數相關聯的參數。

|參數  |描述 |
|---------|---------|
|**processTo** | 將處理 JSON 檔案的位置。 可能的值為**SQLServer**和**AzureSQLDatabase**。 |
|**serverName** | 將處理資料的 SQL Server 實例。  如果您針對**processTo**參數指定**AzureSQLDatabase** ，則只包含 SQL Server 名稱 (不包含 database.windows.net) 。 當您以 Azure SQL Database 為目標時，系統會提示您輸入兩次登入;第一個是您的 Azure 租使用者認證，而第二個則是 Azure SQL Server 的系統管理員登入。 |
|**CreateDMAReporting** | 要建立以處理 JSON 檔案的臨時資料庫。  如果您指定的資料庫已存在，而且您將此參數設定為其中一個，則不會建立物件。  這個參數對於重新建立已卸載的單一物件很有用。 |
|**CreateDataWarehouse** | 建立 Power BI 報表將使用的資料倉儲。 |
|**名稱** | DMAReporting 資料庫的名稱。 |
|**warehouseName** | 資料倉儲資料庫的名稱。 |
|**jsonDirectory** | 包含 JSON 評估檔案的目錄。  如果目錄中有多個 JSON 檔案，則會逐一處理這些檔案。 |

DmaProcessor 函數應該只需要幾秒鐘的時間來處理單一檔案。

## <a name="loading-the-data-warehouse"></a>載入資料倉儲

在 dmaProcessor 完成評估檔案的處理之後，資料將會載入至 ReportData 資料表中的 DMAReporting 資料庫。 此時，您需要載入資料倉儲。

1. 使用 LoadWarehouse 腳本，在維度中填入任何遺漏的值。

    此腳本會從 DMAReporting 資料庫中的 ReportData 資料表取出資料，並將其載入倉儲中。  如果在此載入程式期間發生任何錯誤，可能是因為維度資料表中遺漏專案所造成。

2. 載入資料倉儲。

  ![已載入 LoadWarehouse 內容](../dma/media//dma-consolidatereports/dma-load-warehouse-loaded.png)

## <a name="set-your-database-owners"></a>設定您的資料庫擁有者

雖然這不是強制性的，但若要從報表取得最大的值，建議您在**dimDBOwner**維度中設定資料庫擁有者，然後在**FactAssessment**資料表中更新**DBOwnerKey** 。  遵循此程式可讓您根據特定的資料庫擁有者，切割和篩選 Power BI 報表。

您也可以使用 LoadWarehouse 腳本來提供基本的 TSQL 語句，讓您設定資料庫擁有者。

  ![LoadWarehouse 設定擁有者](../dma/media//dma-consolidatereports/dma-load-warehouse-set-owners.png)

## <a name="dma-reports"></a>DMA 報告

1. 在 Power BI Desktop 中開啟 [DMA 報表 Power BI] 範本。
2. 輸入指向您的**DMAWarehouse**資料庫的伺服器詳細資料，然後選取 [**載入**]。

   ![已載入 Power BI 範本的 DMA 報告](../dma/media//dma-consolidatereports/dma-reports-powerbi-template-loaded.png)

   在報表重新整理**DMAWarehouse**資料庫中的資料之後，您會看到類似下面的報表。

   ![DMAWarehouse 報表檢視](../dma/media//dma-consolidatereports/dma-DMAWarehouse-report1.png)

   > [!TIP]
   > 如果您看不到您預期的資料，請嘗試變更作用中書簽。  如需詳細資訊，請參閱下一節中的詳細資料。

## <a name="working-with-dma-reports"></a>使用 DMA 報告

若要使用 DMA 報表，請使用書簽和交叉分析篩選器來篩選：

- 評量類型 (Azure SQL Database、Azure SQL 受控執行個體、SQL Server)  
- 執行個體名稱
- 資料庫名稱
- 小組名稱

若要存取 [書簽和篩選] 分頁，請在主報表頁面上選取 [篩選] 書簽：

![DMA 報表書簽和篩選](../dma/media//dma-consolidatereports/dma-report-bookmarks-filters.png)

選取 [篩選] 書簽會啟用下列分頁：

![DMA 報表檢視分頁](../dma/media//dma-consolidatereports/dma-report-views-blade.png)

您可以使用書簽來切換中的報告內容：

- Azure SQL Database 雲端評量
- Azure SQL 受控執行個體雲端評量
- 內部部署評量

![DMA 報表查看書簽](../dma/media//dma-consolidatereports/dma-report-bookmarks1.png)

若要隱藏篩選器分頁，請按 [上一步] 按鈕：

![DMA 報表 Views 上一頁按鈕](../dma/media//dma-consolidatereports/dma-report-bookmarks-back.png)

報表頁面左下方會出現一個提示，顯示篩選目前是否已套用至下列任何專案：

- FactAssessment – InstanceName
- FactAssessment – DatabaseName
- dimDBOwner-DBOwner

![篩選套用的提示](../dma/media//dma-consolidatereports/dma-filter-applied-prompt.png)

> [!NOTE]
> 如果您只執行 Azure SQL Database 評估，則只會填入雲端報表。 相反地，如果您只執行內部部署評估，則只會填入內部部署報表。 不過，如果您同時執行 Azure 和內部部署評量，然後將這兩個評量載入倉儲，您可以在雲端報表和內部部署報表之間切換，方法是按一下相關聯的圖示。

## <a name="reports-visuals"></a>報表視覺效果

Power BI 報告中顯示的詳細資料會顯示在下列各節中。

### <a name="readiness-"></a>好

  ![DMA 就緒百分比](../dma/media//dma-consolidatereports/dma-readiness-percentage.png)

此視覺效果會根據選取內容進行更新， (所有專案、實例、資料庫 [倍數] ) 。

### <a name="readiness-count"></a>就緒計數

  ![DMA 準備就緒計數](../dma/media//dma-consolidatereports/dma-readiness-count.png)

此視覺效果會顯示已準備好遷移尚未準備好遷移之資料庫計數的資料庫計數。

### <a name="readiness-bucket"></a>就緒 bucket

  ![DMA 就緒值區](../dma/media//dma-consolidatereports/dma-readiness-bucket.png)

此視覺效果會依據下列準備就緒值區，顯示資料庫的細目：

- 100% 就緒
- 75-99% 就緒
- 50-75% 就緒
- 未就緒

### <a name="issues-word-cloud"></a>Word Cloud 的問題

  ![DMA 問題 WordCloud](../dma/media//dma-consolidatereports/dma-issues-word-cloud.png)

此視覺效果會顯示目前在選取範圍內容中發生的問題 (所有專案、實例、資料庫 [倍數] ) 。 畫面上出現較大的文字，表示該類別中的問題數目愈大。 將滑鼠指標暫留在文字上會顯示該類別中發生的問題數目。

### <a name="database-readiness"></a>資料庫準備就緒

  ![DMA 資料庫就緒報告](../dma/media//dma-consolidatereports/dma-database-readiness-report.png)

此區段是報表的主要部分，它會顯示實例資料庫的就緒程度。 此報表具有的向下切入階層：

- InstanceDatabase
- ChangeCategory
- Title
- ObjectType
- ImpactedObjectName

 ![DMA 資料庫就緒程度報告深入探討](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown.png)

此報表也可做為建立補救計畫報告的篩選點。

若要深入探索補救計畫報告，請以滑鼠右鍵按一下此圖表中的資料點，指向 [**鑽取**]，然後選取 [**補救計畫**]。

此工作會根據您選取 [向下切入] 選項的時間點，將補救計畫報告篩選到目前的階層層級。

  ![已篩選 DMA 資料庫就緒程度報告深入分析](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown-filtered.png)

  ![DMA 補救計畫報告](../dma/media//dma-consolidatereports/dma-remediation-plan-report.png)

您也可以使用 [**視覺效果篩選**] 分頁中的篩選器，自行使用補救計畫報告來建立自訂的補救計畫。

  ![DMA 補救計畫報告篩選選項](../dma/media//dma-consolidatereports/dma-remediation-plan-report-filter-options.png)

### <a name="script-disclaimer"></a>腳本免責聲明

*在任何 Microsoft 標準支援計畫或服務下，都不支援本文中所提供的範例腳本。所有的腳本都是依原樣提供，不含任何種類的擔保。Microsoft 將不會有任何默示擔保，包括（但不限於）適售性或符合特定目的之適用性的任何默示擔保。在使用或執行範例腳本和檔的效能時，所產生的全部風險都會隨您一起進行。Microsoft、其作者、或者，在建立、生產或交付腳本時所牽涉到的任何人，都必須負責因應任何損害 (包括不受影響、失去商業利潤損失、業務中斷、公司資訊遺失或其他 pecuniary 遺失) 因使用或無法使用範例腳本或檔而引發，即使 Microsoft 已建議這類損害的可能性。 在其他網站/存放庫/blog 上 reposting 這些腳本之前，搜尋許可權。*
