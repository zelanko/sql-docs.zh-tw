---
title: 第 6 課：建立量值 |Microsoft Docs
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f8ad53f78acb862101ff633f663ea03198825ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65404660"
---
# <a name="lesson-6-create-measures"></a>第 6 課：建立量值
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將建立要包含在模型中的量值。 類似於您在上一課中建立的導出資料行，量值是使用 DAX 公式所建立的計算。 不過，與導出資料行不同的是，量值是根據使用者選取的「篩選」  進行評估；例如，加入樞紐分析表之 [資料列標籤] 欄位中的特殊資料行或交叉分析篩選器。 然後套用的量值就會計算篩選中每個資料格的值。 量值是功能強大又靈活的計算，您會想要包含在幾乎所有表格式模型中，對數值資料執行動態計算。 若要進一步了解，請參閱[量值](../tabular-models/measures-ssas-tabular.md)。  
  
若要建立量值，您將使用*量值方格*。 根據預設，每個資料表都有一個空白的量值方格，不過，通常您不會為每個資料表建立量值。 在 [資料檢視] 中，量值方格會出現在模型設計師中的資料表下方。 若要隱藏或顯示資料表的量值方格，請按一下 [資料表]  功能表，然後按一下 [顯示量值方格]  。  
  
您可以按一下量值方格中的空白資料格，然後在公式列中輸入 DAX 公式，藉此建立量值。 按 ENTER 完成公式時，量值就會出現在資料格中。 您也可以使用標準彙總函式建立量值，只要按一下資料行，然後按一下工具列上的 [自動加總] 按鈕 (**∑**) 即可。 使用 「 自動加總 」 功能建立量值會出現在資料行的下方的量值方格資料格中，但是可以移動。  
  
在這一課，您將藉由在公式列中輸入 DAX 公式以及使用 [自動加總] 功能這兩種方式建立量值。  
  
估計的時間才能完成這一課：**30 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 執行工作之前在這一課，您應已完成上一課：[第 5 課：建立計算結果的欄](lesson-5-create-calculated-columns.md)。  
  
## <a name="create-measures"></a>建立量值  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>在 DimDate 資料表中建立 DaysCurrentQuarterToDate 量值  
  
1.  在模型設計師中，按一下**DimDate**資料表。  
  
2.  在量值方格中，按一下左上方的空資料格。  
  
3.  在公式列中，輸入下列公式：  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    請注意左上方資料格現在包含量值名稱**DaysCurrentQuarterToDate**，後面接著結果**92**。
    
      ![as-tabular-lesson6-newmeasure](media/as-tabular-lesson6-newmeasure.png) 
    
    不同於導出資料行，量值公式與您可以輸入量值名稱，後面接著逗號，後面接著公式運算式。

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>若要在 DimDate 資料表中建立 DaysInCurrentQuarter 量值  
  
1.  具有**DimDate**資料表在模型設計師中，量值方格中，按一下您剛建立之量值下方的空資料格。  
  
2.  在公式列中，輸入下列公式：  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    在一個不完整期間與前一個期間之間建立比率時，公式必須考慮期間內已經過的比例，並且將它與前一個期間中的相同比例進行比較。 在此情況下，[DaysCurrentQuarterToDate] / [daysincurrentquarter] 比例目前期間內已經過。  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>在 FactInternetSales 資料表中建立 InternetDistinctCountSalesOrder 量值  
  
1.  按一下  **FactInternetSales**資料表。   
  
2.  按一下  **SalesOrderNumber**資料行標題。  
  
3.  在工具列上按一下 [自動加總] \(**∑**) 按鈕旁的向下箭號，然後選取 [DistinctCount]  。  
  
    [自動加總] 功能會使用 DistinctCount 標準彙總公式，自動為選取的資料行建立量值。  
    
       ![as-tabular-lesson6-newmeasure2](media/as-tabular-lesson6-newmeasure2.png)
  
4.  在量值方格中，按一下 [新增量值，然後在**屬性**] 視窗，請在**量值名稱**，重新命名的量值**InternetDistinctCountSalesOrder**。 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>建立 FactInternetSales 資料表中的其他量值  
  
1.  使用 [自動加總] 功能建立並命名下列量值：  
  
    |[量值名稱]|「資料行」|自動加總 (∑)|公式|  
    |----------------|----------|-----------------|-----------|  
    |InternetOrderLinesCount|SalesOrderLineNumber|Count|=COUNTA([SalesOrderLineNumber])|  
    |InternetTotalUnits|OrderQuantity|Sum|=SUM([OrderQuantity])|  
    |InternetTotalDiscountAmount|DiscountAmount|Sum|=SUM([DiscountAmount])|  
    |InternetTotalProductCost|TotalProductCost|Sum|=SUM([TotalProductCost])|  
    |InternetTotalSales|SalesAmount|Sum|=SUM([SalesAmount])|  
    |InternetTotalMargin|Margin|Sum|=SUM([Margin])|  
    |InternetTotalTaxAmt|TaxAmt|Sum|=SUM([TaxAmt])|  
    |InternetTotalFreight|Freight|Sum|=SUM([Freight])|  
  
2.  按一下空白儲存格在量值方格中，並使用公式列中，建立並命名下列量值的順序：  
  
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
請移至下一課：[第 7 課：建立關鍵效能指標](lesson-7-create-key-performance-indicators.md)。  

  
