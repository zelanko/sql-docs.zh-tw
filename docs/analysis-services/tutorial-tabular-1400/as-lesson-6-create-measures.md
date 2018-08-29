---
title: Analysis Services 教學課程第 6 課： 建立量值 |Microsoft 文件
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f9b466a703dd04a53c6ebf7c6fac624476abcc52
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43093961"
---
# <a name="create-measures"></a>建立量值

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您可以建立要包含在您的模型中的量值。 類似於您所建立的導出資料行，量值是使用 DAX 公式所建立的計算。 不過，不同於導出資料行，量值評估是根據使用者選取*篩選*。 例如，特定資料行或交叉分析篩選器加入至樞紐分析表中的資料列標籤 欄位。 然後套用的量值就會計算篩選中每個資料格的值。 量值是功能強大又靈活的計算，您想要包含在幾乎所有表格式模型中，對數值資料執行動態計算。 若要進一步了解，請參閱[量值](../tabular-models/measures-ssas-tabular.md)。
  
若要建立量值，您使用*量值方格*。 根據預設，每個資料表都有一個空的量值方格;不過，您通常請勿建立針對每個資料表的量值。 在 [資料檢視] 中，量值方格會出現在模型設計師中的資料表下方。 若要隱藏或顯示資料表的量值方格，請按一下 [資料表] 功能表，然後按一下 [顯示量值方格]。  
  
若要建立量值，您可以按一下空白儲存格在量值方格中，然後在公式列中輸入 DAX 公式。 當您按 ENTER 完成公式，量值，則會出現在資料格。 您也可以建立使用標準彙總函式，藉由按一下資料行，然後按一下 自動加總 按鈕的量值 (**∑**) 工具列上。 使用 「 自動加總 」 功能建立量值會出現在資料行的下方的量值方格資料格中，但是可以移動。  
  
在這一課，您會建立量值，在公式列中，輸入 DAX 公式和使用 「 自動加總 」 功能。  
  
完成本課程的估計時間： **30 分鐘**  
  
## <a name="prerequisites"></a>先決條件  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 執行工作之前在這一課，您應已完成上一課：[第 5 課： 建立計算結果的欄](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)。  
  
## <a name="create-measures"></a>建立量值  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>在 DimDate 資料表中建立 DaysCurrentQuarterToDate 量值  
  
1.  在模型設計師中，按一下**DimDate**資料表。  
  
2.  在量值方格中，按一下左上方的空資料格。  
  
3.  在公式列中，輸入下列公式：  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    請注意左上方資料格現在包含量值名稱**DaysCurrentQuarterToDate**，後面接著結果**92**。 結果不相關此時因為沒有使用者篩選已經套用。
    
      ![為 lesson6 newmeasure](../tutorial-tabular-1400/media/as-lesson6-newmeasure.png) 
    
    不同於導出資料行，量值公式與您可以輸入量值名稱，後面接著冒號，後面接著公式運算式。

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>若要在 DimDate 資料表中建立 DaysInCurrentQuarter 量值  
  
1.  具有**DimDate**資料表在模型設計師中，量值方格中，按一下您所建立之量值下方的空資料格。  
  
2.  在公式列中，輸入下列公式：  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    當建立一個不完整期間與前一個期間之間的比率。 此公式必須計算期間已過，與前一個期間中的相同比例比較的比例。 在此情況下，[DaysCurrentQuarterToDate] / [daysincurrentquarter] 比例目前期間內已經過。  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>在 FactInternetSales 資料表中建立 InternetDistinctCountSalesOrder 量值  
  
1.  按一下  **FactInternetSales**資料表。   
  
2.  按一下  **SalesOrderNumber**資料行標題。  
  
3.  在工具列上按一下 [自動加總] \(**∑**) 按鈕旁的向下箭號，然後選取 [DistinctCount]。  
  
    [自動加總] 功能會使用 DistinctCount 標準彙總公式，自動為選取的資料行建立量值。  
    
       ![as-lesson6-newmeasure2](../tutorial-tabular-1400/media/as-lesson6-newmeasure2.png)
  
4.  在量值方格中，按一下 [新增量值，然後在**屬性**] 視窗，請在**量值名稱**，重新命名的量值**InternetDistinctCountSalesOrder**。 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>建立 FactInternetSales 資料表中的其他量值  
  
1.  使用 [自動加總] 功能建立並命名下列量值：  

    |「資料行」|量值名稱|自動加總 (∑)|公式|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Count|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|SUM|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|SUM|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|SUM|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|SUM|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|SUM|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|SUM|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|SUM|=SUM([Freight])|  
  
2.  按一下空白儲存格在量值方格中，並使用公式列中，建立，順序中的下列自訂量值：  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
建立 FactInternetSales 資料表的量值可用來分析重要財務資料，例如銷售額、 成本和獲利率的使用者選取的篩選條件所定義的項目。  
  
## <a name="whats-next"></a>下一步

[第 7 課： 建立關鍵效能指標](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)。  

  
