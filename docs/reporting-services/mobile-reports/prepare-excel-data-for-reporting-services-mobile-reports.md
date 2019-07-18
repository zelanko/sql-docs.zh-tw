---
title: 準備 Reporting Services 行動報表的 Excel 資料 | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 16698f8d-bfc7-4eca-9e97-82c99d8bc08e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9285b9b89930fe540f9b5493f1730184cf4e9526
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62499939"
---
# <a name="prepare-excel-data-for-reporting-services-mobile-reports"></a>準備 Reporting Services 行動報表的 Excel 資料
  
當準備 Excel 檔案和工作表以搭配行動報表使用時，以下是一些要記住的事項：  
  
## <a name="do"></a>要做的事  
  
- 每個資料集一個工作表。  
- 在第一個資料列中提供資料行標頭。  
- 保持每個資料行中的資料類型一致。  
- 將資料格格式化為 Excel 中適當的類型。  
- 以工作表提供資料，而非以 Excel 中的資料模型。  
- 當使用公式，確定整個資料行都使用相同的公式計算。  
- 使用 Excel 2007 或更新版本。  
- 使用副檔名 XLSX 儲存 Excel 檔案。  
          
## <a name="dont"></a>不要做的事  
  
- 在資料集工作表中包含影像、圖形、樞紐分析表或其他內嵌物件。  
- 包含總計或計算結果列。  
- 在匯入時仍在 Excel 中保持檔案開啟。  
- 新增貨幣或其他符號手動格式化數字。  
- 使用活頁簿搭配儲存在資料模型中的資料。  
  
## <a name="worksheets"></a>工作表  
          
當準備 Excel 檔案作為行動報表的資料集時，請確定您在每在工作表中只有一個資料集。 每張個別的工作表會匯入 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 做為個別的資料表。 多個 Excel 來源的相同具名工作表，在匯入時會加上遞增數字來重新命名。 例如，如果活頁簿有三個標題為 "MyWorksheet" 的工作表，則第二個和第三個工作表會重新命名為 "MyWorksheet0" 和 "MyWorksheet1"。 以下的螢幕擷取畫面說明準備好匯入的理想 Excel 工作表的前幾個資料列。  
  
![SS_MRP_ExcelDataSheet](../../reporting-services/mobile-reports/media/ss-mrp-exceldatasheet.png)  
          
## <a name="column-headers"></a>資料行標頭  
  
如您在上述的範例中所見，第一個資料列包含該資料行中的度量名稱。 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 會保留這些資料行標頭，以便組件庫項目設定中的簡單參考使用。 不過，資料行標頭並非必要。 如果遺漏， [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 會使用 Excel 的 A、B、C,...、AA、BB、...慣例來產生標題。  
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 會比較每個資料行中前兩個資料格的資料類型，在匯入 Excel 工作表時自動偵測第一個資料列的標頭。 如果任何資料行中前兩個資料格的資料類型不相符，第一個資料列會判斷為包含資料行標頭。 因此，若資料表有數值資料行標頭、請在標頭名稱前面加上字串，如此它們在匯入程序時就會偵測為標頭。  
  
## <a name="cells"></a>資料格  
  
工作表資料集每個資料行中的資料格資料必須一致。 匯入時每個資料行會指派資料類型。 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 會自動偵測資料類型為 string、double (數值)、boolean (true/false) 或 datetime。 在相同資料行中混合資料類型可能會導致這個偵測錯誤或完全失敗。 這項偵測會將字串類型視為可能的資料行標頭。 資料格應該在 Excel 中格式化為正確的類型，以確保 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 會偵測所需的類型。 在上述的範例中，其六個資料行的類型為：  
*  一個 datetime 資料行  
*  一個 string 資料行  
*  四個 double 資料行  
  
如果工作表包含導出資料格或公式，則只有結果顯示值會匯入至 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]。  
  
## <a name="file-location-and-refreshing-excel-data"></a>檔案位置及重新整理 Excel 資料  
  
匯入至 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]的 Excel 檔案儲存位置沒有任何限制。 不過，如果您在匯入後移動或重新命名檔案，您將無法透過 [資料檢視] 中的 **refresh all data** 命令重新整理該資料。   
  
>**注意**： [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 不會自動重新整理 Excel 資料。 您可以透過 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] **refresh** command, but only if the file hasn't moved.  
  
## <a name="dates"></a>日期  
  
日期欄位對許多行動報表來說很重要，因此請在 Excel 中將資料格正確地格式化為日期。 在某些情況下這代表必須要轉換。 以下是在 Excel 中將資料格從文字轉換為日期的公式範例。  
  
    Week 24-2013=DATE(MID(A2,9,4),1,-2)-WEEKDAY(DATE(MID(A2,9,4),1,3))+MID(A2,6,2)*7  
  
    2013/03/21=DATEVALUE(A1)  
  
    2013-mar-12=DATEVALUE(RIGHT(A1,2)&"-"&MID(A1,6,3)&"-"&LEFT(A1,4))  
  
在您轉換資料格後，您必須將它們格式化為日期，方法是選取它們或整個資料行 > **操作**功能表 > [儲存格格式]   > [類別目錄]  清單中的 [日期]  。 您也可以使用 Excel 資料剖析精靈將文字資料格轉換為正確格式的日期。  
  
## <a name="unsupported"></a>不支援  
  
除了上述的格式外，其他格式的工作表資料匯入時可能會導致無法預期的結果。 將 Excel 檔案中的工作表限制為只能搭配行動報表使用的正確格式是不錯的作法。  
  
Excel 工作表中的自訂物件，包括樞紐分析表、視覺效果和影像等，均不會匯入至 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]。  
  
### <a name="see-also"></a>另請參閱  
- [Prepare data for Reporting Services mobile reports (準備 Reporting Services 行動報表的資料)](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)  
- [使用 SQL Server 行動報表發行工具建立與發行行動報表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  在 [iPad app 中檢視 SQL Server 行動報表和 KPI](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI for iOS)  
-  請參閱 [在 iPhone 應用程式中檢視 SQL Server 行動報表和 KPI (iOS 版 Power BI)](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (iOS 版 Power BI)  
  
  
  
  
  
  
  

