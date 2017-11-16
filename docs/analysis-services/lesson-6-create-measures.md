---
title: "第 7 課： 建立量值 |Microsoft 文件"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f486e0094e66ed503b63fb52c4cba88dbcadbb62
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-6-create-measures"></a>第 6 課： 建立量值
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將建立要包含在模型中的量值。 類似於您在上一課中建立的導出資料行，量值是透過使用 DAX 公式所建立的計算。 不過，與導出資料行不同的是，量值是根據使用者選取的「篩選」進行評估；例如，加入樞紐分析表之 [資料列標籤] 欄位中的特殊資料行或交叉分析篩選器。 然後套用的量值就會計算篩選中每個資料格的值。 量值是功能強大、 有彈性的計算，您會想要包含在幾乎所有表格式模型中，對數值資料執行動態計算。 若要進一步了解，請參閱[量值](../analysis-services/tabular-models/measures-ssas-tabular.md)。  
  
若要建立量值，您將使用*量值方格*。 根據預設，每個資料表都有一個空白的量值方格，不過，通常您不會為每個資料表建立量值。 在 [資料檢視] 中，量值方格會出現在模型設計師中的資料表下方。 若要隱藏或顯示資料表的量值方格，請按一下 [資料表] 功能表，然後按一下 [顯示量值方格]。  
  
您可以按一下量值方格中的空白資料格，然後在公式列中輸入 DAX 公式，藉此建立量值。 按 ENTER 完成公式時，量值就會出現在資料格中。 您也可以使用標準彙總函式建立量值，只要按一下資料行，然後按一下工具列上的 [自動加總] 按鈕 (**∑**) 即可。 使用自動加總 功能建立的量值會出現在資料行正下方的量值方格資料格，但是可以移動。  
  
在這一課，您將藉由在公式列中輸入 DAX 公式以及使用 [自動加總] 功能這兩種方式建立量值。  
  
完成本課程的估計時間： **30 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 然後再執行工作，在這一課，您應已完成上一課：[第 5 課： 建立導出資料行](../analysis-services/lesson-5-create-calculated-columns.md)。  
  
## <a name="create-measures"></a>建立量值  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>若要建立 DaysCurrentQuarterToDate 量值與 DimDate 資料表中  
  
1.  在模型設計師中，按一下**DimDate**資料表。  
  
2.  在量值方格中，按一下左上方的空資料格。  
  
3.  在公式列中，輸入下列公式：  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    請注意左上資料格現在包含量值名稱， **DaysCurrentQuarterToDate**，後面接著結果**92**。
    
      ![做為表格式-lesson6-newmeasure](../analysis-services/media/as-tabular-lesson6-newmeasure.png) 
    
    不同於導出資料行，量值公式與您可以輸入量值名稱，加上逗號，後面接著公式的運算式。

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>若要建立 DaysInCurrentQuarter 量值與 DimDate 資料表中  
  
1.  與**DimDate**資料表仍為使用中模型設計師中，在量值方格中，按一下您剛建立之量值下方的空資料格。  
  
2.  在公式列中，輸入下列公式：  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    在一個不完整期間與前一個期間之間建立比率時，公式必須考慮期間內已經過的比例，並且將它與前一個期間中的相同比例進行比較。 在這種情況下，[DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 提供比例經過目前期間內。  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>在 [FactInternetSales] 資料表中建立 InternetDistinctCountSalesOrder 量值  
  
1.  按一下**FactInternetSales**資料表。   
  
2.  按一下**SalesOrderNumber**資料行標題。  
  
3.  在工具列上按一下 [自動加總] \(**∑**) 按鈕旁的向下箭號，然後選取 [DistinctCount]。  
  
    [自動加總] 功能會使用 DistinctCount 標準彙總公式，自動為選取的資料行建立量值。  
    
       ![做為表格式-lesson6-newmeasure2](../analysis-services/media/as-tabular-lesson6-newmeasure2.png)
  
4.  在量值方格中，按一下 新增量值，然後在**屬性**視窗，請在**量值名稱**，重新命名量值**InternetDistinctCountSalesOrder**。 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>FactInternetSales 資料表中建立其他量值  
  
1.  使用 [自動加總] 功能建立並命名下列量值：  
  
    |[量值名稱]|資料行|自動加總 (∑)|公式|  
    |----------------|----------|-----------------|-----------|  
    |InternetOrderLinesCount|SalesOrderLineNumber|Count|=COUNTA([SalesOrderLineNumber])|  
    |InternetTotalUnits|OrderQuantity|Sum|=SUM([OrderQuantity])|  
    |InternetTotalDiscountAmount|DiscountAmount|Sum|=SUM([DiscountAmount])|  
    |InternetTotalProductCost|TotalProductCost|Sum|=SUM([TotalProductCost])|  
    |InternetTotalSales|SalesAmount|Sum|=SUM([SalesAmount])|  
    |InternetTotalMargin|Margin|Sum|=SUM([Margin])|  
    |InternetTotalTaxAmt|TaxAmt|Sum|=SUM([TaxAmt])|  
    |InternetTotalFreight|Freight|Sum|=SUM([Freight])|  
  
2.  藉由按一下量值方格中的空資料格以及使用公式列中，建立並命名下列量值順序：  
  
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
  
針對 FactInternetSales 資料表所建立的量值可以用來分析關鍵的財務資料，例如銷售額、 成本以及使用者所選取的篩選所定義的項目獲利率。  
  
## <a name="whats-next"></a>下一步
移至下一課：[第 7 課： 建立關鍵效能指標](../analysis-services/lesson-7-create-key-performance-indicators.md)。  

  

