---
title: 評估企業並合併評定報告 (SQL Server) |Microsoft Docs
description: 了解如何使用 DMA，以評估企業，並合併評定報告，然後再升級 SQL Server，或移轉至 Azure SQL Database。
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: pochiraju
ms.author: rajpo
manager: craigg
ms.openlocfilehash: f748189446ca3d5cfd49c748fa058cf8dbef7fe7
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51601818"
---
# <a name="assess-an-enterprise-and-consolidate-assessment-reports-with-dma"></a>評估企業及彙總與 DMA 的評估報告

下列的逐步指示可協助您使用 Data Migration Assistant，以執行成功的縮放的評估，在內部部署 SQL Server 或 Azure Vm 上執行的 SQL Server 升級或移轉至 Azure SQL Database。

## <a name="prerequisites"></a>先決條件

- 指定工具電腦將會起始 DMA 您網路上。 請確定此電腦已連線到您的 SQL Server 目標。
- 下載並安裝：
    - [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) 3.6 版或更新版本。
    - [PowerShell](https://aka.ms/wmf5download) 5.0 版或更新版本。
    - [.NET framework](https://www.microsoft.com/download/details.aspx?id=30653) v4.5 或更新版本。
    - [SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.0 或更新版本。
    - [Power Bi desktop](https://docs.microsoft.com/power-bi/desktop-get-the-desktop)。
- 下載並解壓縮：
    - [DMA 報表 Power BI 範本](https://msdnshared.blob.core.windows.net/media/2018/04/PowerBI-Reports1.zip)。
    - [LoadWarehouse 指令碼](https://msdnshared.blob.core.windows.net/media/2018/10/LoadWarehouse.zip)。

## <a name="loading-the-powershell-modules"></a>正在載入 PowerShell 模組
儲存到 PowerShell 模組目錄的 PowerShell 模組，可讓您呼叫的模組，而不需要明確載入它們，才能使用。

若要載入的模組，請執行下列步驟：
1. 瀏覽至 C:\Program Files\WindowsPowerShell\Modules，然後建立名為資料夾**DataMigrationAssistant**。
2. 開啟[PowerShell 模組](https://msdnshared.blob.core.windows.net/media/2018/10/PowerShell-Modules.zip)，然後將它們儲存到您所建立的資料夾。

      ![PowerShell 模組](../dma/media//dma-consolidatereports/dma-powershell-modules.png)

    每個資料夾包含相關聯的 psm1 檔案，如下圖所示：

   ![PowerShell 模組 psm1 檔案](../dma/media//dma-consolidatereports/dma-powershell-modules-psm1-files.png)

   > [!NOTE]
   > 資料夾和它所包含的 psm1 檔案必須具有相同的名稱。

   > [!IMPORTANT]
   > 您可能需要解除封鎖 PowerShell 檔案之後將它們儲存到 WindowsPowerShell 的目錄，以確保正確載入的模組。 若要解除封鎖 PowerShell 檔案，以滑鼠右鍵按一下檔案，選取**屬性**，選取**解除封鎖**文字方塊中，然後選取**Ok**。

   ![psm1 檔案屬性](../dma/media//dma-consolidatereports/dma-psm1-file-properties.png)

    PowerShell 應該現在這些模組自動載入新的 PowerShell 工作階段啟動時。

## <a name="create-inventory"></a> 建立 SQL 伺服器的清查
之前執行的 PowerShell 指令碼，來評估您的 SQL Server，您必須建置您想要評估 SQL 伺服器的清查。

此清查可以處於兩種形式之一：
- Excel CSV 檔案
- SQL Server 資料表

### <a name="if-using-a-csv-file"></a>如果使用 CSV 檔案
當使用 csv 檔案匯入資料，請確定只有兩個資料行的資料 –**執行個體名稱**並**資料庫名稱**，資料行不會有標頭資料列。
 
 ![csv 檔案內容](../dma/media//dma-consolidatereports/dma-csv-file-contents.png)

### <a name="if-using-sql-server-table"></a>如果使用 SQL Server 資料表
建立名為的資料庫**EstateInventory**和名**DatabaseInventory**。 包含這個清查資料的資料表可以有任意數目的資料行，只要有下列四個資料行：
- ServerName
- InstanceName
- DatabaseName
- AssessmentFlag

![SQL Server 資料表的內容](../dma/media//dma-consolidatereports/dma-sql-server-table-contents.png)

如果此資料庫不在工具電腦上，請確定工具的電腦具有網路連線到此 SQL Server 執行個體。

透過 CSV 檔案中使用 SQL Server 資料表的好處是，您可以使用評估旗標資料行控制執行個體 / 資料庫取得撿起進行評估，可讓您更輕鬆地分隔成較小區塊的評估。  您接著可以跨越多個評量 （請參閱區段在本文稍後執行評量），也就是容易維護多個 CSV 檔案。

請記住，根據物件和其複雜性的數目，評估可能需要更長的時間 （小時 +，） 區隔成易於管理的區塊評估容錯度加倍，因此。

## <a name="running-a-scaled-assessment"></a>執行縮放的評定
載入的模組目錄中的 PowerShell 模組，並建立詳細目錄之後，您需要開啟 PowerShell 並執行 dmaDataCollector 函式執行縮放的評估。
 
  ![dmaDataCollector 函式清單](../dma/media//dma-consolidatereports/dma-dmaDataCollector-function-listing.png)

下表說明 dmaDataCollector 函式相關聯的參數。

|參數  |描述
|---------|---------|
|**getServerListFrom** | 您的清查。 可能的值為**SqlServer**並**CSV**。<br/>如需詳細資訊，請參閱 <<c0> [ 建立的 SQL 伺服器清查](#create-inventory)。 |
|**serverName** | 清查時使用的 SQL Server 執行個體名稱**SqlServer**中**getServerListFrom**參數。 |
|**databaseName** | 裝載清查資料表的資料庫。 |
|**AssessmentName** | DMA 評估的名稱。 |
|**TargetPlatform** | 您想要執行之評定目標型別。  可能的值為**AzureSQLDatabase**， **SQLServer2012**， **SQLServer2014**， **SQLServer2016**， **SQLServerLinux2017**，並**SQLServerWindows2017**。 |
|**AuthenticationMethod** | 您想要評估的驗證方法連接到 SQL Server 目標。 可能的值為**SQLAuth**並**WindowsAuth**。 |
|**OutputLocation** | 要儲存 JSON 評估輸出檔案目錄。 根據要評估的資料庫數目與在資料庫內的物件數目，評估可能需要更長的時間。 所有評定皆已都完成之後，就會寫入檔案。 |

如果有未預期的錯誤，將會終止命令視窗，取得由這個處理程序。  檢閱錯誤記錄檔，以判斷失敗的原因。
 
  ![錯誤記錄檔位置](../dma/media//dma-consolidatereports/dma-error-log-file-location.png)

## <a name="consuming-the-assessment-json-file"></a>使用評估 JSON 檔案

完成您的評估之後，您現在準備好資料匯入至 SQL Server 進行分析。 若要使用評估的 JSON 檔案，請開啟 PowerShell 並執行 dmaProcessor 函式。
 
  ![dmaProcessor 函式清單](../dma/media//dma-consolidatereports/dma-dmaProcessor-function-listing.png)

下表說明 dmaProcessor 函式相關聯的參數。

|參數  |描述
|---------|---------|
|**processTo**  | 處理 JSON 檔案的位置。 可能的值為**SQLServer**並**AzureSQLDatabase**。 |
|**serverName** | 處理資料的 SQL Server 執行個體。  如果您指定**AzureSQLDatabase** for **processTo**參數，則會包含只有 SQL Server 名稱 (不包括。 database.windows.net)。 您在目標為 Azure SQL Database; 時的兩個登入提示第一個是您的 Azure 租用戶認證，而第二個是您的系統管理員登入 Azure SQL server。 |
|**CreateDMAReporting** | 要建立來處理 JSON 檔案的暫存資料庫。  如果您已經指定此資料庫確實存在，而且您將此參數設定為其中一個，不會建立物件。  此參數可用於重新建立已卸除單一物件。 |
|**CreateDataWarehouse** | 建立將用於 Power BI 報表資料倉儲。 |
|**databaseName** | DMAReporting 資料庫的名稱。 |
|**warehouseName** | 資料倉儲資料庫的名稱。 |
|**jsonDirectory** | 包含 JSON 評估檔案的目錄。  如果在目錄中，有多個 JSON 檔案，則它們會處理一一。 |

DmaProcessor 函式應該只需要幾秒鐘的時間處理單一檔案。

## <a name="loading-the-data-warehouse"></a>正在載入資料倉儲
DmaProcessor 已完成處理評估檔案之後，資料會載入 DMAReporting 資料庫 ReportData 資料表中。 此時，您需要載入資料倉儲。

1. 您可以使用 LoadWarehouse 指令碼來填入維度中的任何遺漏值。

    指令碼會在 DMAReporting 資料庫採取 ReportData 資料表中的資料，並將其載入至倉儲的資料。  如果此載入程序期間發生任何錯誤，它們可能遺漏的項目維度資料表中的結果。

2. 載入資料倉儲。
 
      ![載入的 LoadWarehouse 內容](../dma/media//dma-consolidatereports/dma-LoadWarehouse-loaded.png)

## <a name="set-your-database-owners"></a>設定您的資料庫擁有者
雖然並非必要項目，以取得最大價值的報表，建議您設定資料庫擁有者**dimDBOwner**維度，然後再更新**DBOwnerKey**在**FactAssessment**資料表。  遵循此程序，可讓配量和篩選特定的資料庫擁有者為基礎的 Power BI 報表。

您也可以使用 LoadWarehouse 指令碼，以提供基本的 TSQL 陳述式，為您設定資料庫擁有者。

  ![LoadWarehouse 設定擁有者](../dma/media//dma-consolidatereports/dma-LoadWarehouse-set-owners.png)

## <a name="dma-reports"></a>DMA 報表

1. 在 Power BI Desktop 中開啟 DMA 報表 Power BI 的範本。
2. 輸入伺服器的詳細資料，以指向您**DMAWarehouse**資料庫，然後按**負載**。

    > [!IMPORTANT]
    > 不要按 Enter 以接受的值。

      ![載入的 DMA 報表 Power BI 範本](../dma/media//dma-consolidatereports/dma-reports-powerbi-template-loaded.png)

   已重新整理報表中的資料之後**DMAWarehouse**資料庫中，將會看到類似下列的報表。

   ![DMAWarehouse 報表檢視](../dma/media//dma-consolidatereports/dma-DMAWarehouse-report.png)

   > [!TIP]
   > 如果看不到您所預期的資料，請嘗試變更作用中的書籤。  如需詳細資訊，請參閱功能 > 一節。

## <a name="working-with-dma-reports"></a>使用 DMA 報表
若要使用 DMA 報表，使用交叉分析篩選器來篩選：
- 執行個體名稱
- 資料庫名稱
- 小組名稱

您也可以使用書籤，報表的內容之間切換：
- 雲端評量
- 在內部部署環境評量

  ![DMA 報告書籤](../dma/media//dma-consolidatereports/dma-report-bookmarks.png)

> [!NOTE]
> 如果您只會執行 Azure SQL Database 評量，會填入僅雲端報告。 相反地，如果您只會執行內部評量，就會填入僅在內部部署報表。 不過，如果您執行 Azure 和內部評估，然後載入您的倉儲中的兩個評量，您可以切換報表雲端及內部 CTRL 按一下關聯的圖示。

## <a name="reports-visuals"></a>報表視覺效果
下列各節會顯示在 Power BI 報表中顯示的詳細資料。

### <a name="readiness-"></a>整備 %

  ![DMA 整備百分比](../dma/media//dma-consolidatereports/dma-readiness-percentage.png)

此視覺效果會更新選取項目內容為基礎 (所有項目，執行個體，資料庫 [的倍數])。

### <a name="readiness-count"></a>更新整備小計數

  ![DMA 整備計數](../dma/media//dma-consolidatereports/dma-readiness-count.png)

此視覺效果會顯示已準備好移轉還沒準備要移轉的資料庫數目的資料庫計數。

### <a name="readiness-bucket"></a>整備貯體

  ![DMA 整備貯體](../dma/media//dma-consolidatereports/dma-readiness-bucket.png)

此視覺效果會顯示資料庫的下列整備貯體的明細：
- 100%已準備好
- 75 99%已準備好
- 50 到 75%已準備好
- 未就緒

### <a name="issues-word-cloud"></a>問題 Word 雲端
 
  ![DMA 問題 WordCloud](../dma/media//dma-consolidatereports/dma-issues-word-cloud.png)

此視覺效果中選取項目內容顯示目前內發生的問題 (所有項目，執行個體，資料庫 [的倍數])。 越大這個字出現在畫面上，較大者該類別中的問題數目。 將滑鼠指標暫留文字會顯示該類別中所發生的問題數目。

### <a name="database-readiness"></a>資料庫的整備程度

  ![DMA 資料庫整備報表](../dma/media//dma-consolidatereports/dma-database-readiness-report.png)

本節是報告，其中會顯示執行個體資料庫的完備性的主要部分。 此報表包含向下鑽研的階層：
- InstanceDatabase
- ChangeCategory
- Title
- ObjectType
- ImpactedObjectName

 ![DMA 資料庫整備報表向下鑽研](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown.png)

此報表也可作為建立補救計劃報表的篩選器點。

若要向下鑽研到補救計劃報表，以滑鼠右鍵按一下此圖中的資料點，指向**鑽研**，然後選取**補救計劃**。

這項工作會篩選目前選取的鑽研選項的點為基礎的階層層級補救計劃報表。

  ![DMA 資料庫整備報表向下鑽研篩選](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown-filtered.png)

  ![DMA 補救計劃報表](../dma/media//dma-consolidatereports/dma-remediation-plan-report.png)

您也可以使用它自己建置自訂的補救方案修復計劃報表，使用中的篩選條件**視覺效果篩選**刀鋒視窗。
 
  ![DMA 補救計劃的報表篩選選項](../dma/media//dma-consolidatereports/dma-remediation-plan-report-filter-options.png)

### <a name="script-disclaimer"></a>指令碼免責聲明
*在本文中提供的範例指令碼不受任何 Microsoft 標準支援計畫或服務。所有的指令碼是現狀提供，不含任何種類的擔保。Microsoft 同時否認所有默示的擔保，包括但不限於任何默示之瑕疵擔保適售性或適合某特定用途。因使用或展示的範例指令碼和文件的風險由使用者承擔。在任何情況 Microsoft、 其作者或任何其他參與建立、 生產環境或傳遞的指令碼的人應該對於任何損害賠償責任運作 （包括但不限於，商業利潤、 營業中斷、 損失的損害嗎商務資訊或其他金錢損失） 因使用或無法使用的範例指令碼或文件，即使 Microsoft 已獲知該等損害之可能性。搜尋權限，才能在其他站台/存放庫/部落格上，這些指令碼會重新張貼。*
