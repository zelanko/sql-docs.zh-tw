---
title: Analysis Services 教學課程第 6 課： 建立量值 |Microsoft 文件
description: 描述如何在 Analysis Services 教學課程專案中建立量值。
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 1d304d20649c4a2ab3c5a91646cc69ff66820f54
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="create-measures"></a>建立量值

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您可以建立要包含在模型中的量值。 類似於您所建立的導出資料行，量值是透過使用 DAX 公式所建立的計算。 不過，不同於導出資料行，量值會根據評估使用者選取*篩選*。 例如，特定資料行或交叉分析篩選器加入至樞紐分析表中之資料列標籤欄位。 然後套用的量值就會計算篩選中每個資料格的值。 量值是您想要在數值資料上執行動態計算幾乎所有表格式模型中包含的功能強大、 有彈性的計算。 若要進一步了解，請參閱[量值](../tabular-models/measures-ssas-tabular.md)。
  
若要建立的量值，您使用*量值方格*。 根據預設，每一個資料表具有空白量值方格;不過，您通常不建立每個資料表的量的值。 在 [資料檢視] 中，量值方格會出現在模型設計師中的資料表下方。 若要隱藏或顯示資料表的量值方格，請按一下 [資料表] 功能表，然後按一下 [顯示量值方格]。  
  
您可以按一下量值方格中的空資料格，然後在公式列中輸入 DAX 公式建立量值。 當您按 ENTER 完成公式，量值，則會出現在資料格。 您也可以建立使用按一下資料行，然後再按一下 [自動加總] 按鈕的標準彙總函式的量值 (**∑**) 在工具列上。 使用自動加總 功能建立的量值會出現在資料行正下方的量值方格資料格，但是可以移動。  
  
在這一課，您會建立量值，藉由在公式列中，這兩個輸入 DAX 公式，而藉由使用 [自動加總] 功能。  
  
完成本課程的估計時間： **30 分鐘**  
  
## <a name="prerequisites"></a>필수 구성 요소  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 然後再執行工作，在這一課，您應已完成上一課：[第 5 課： 建立導出資料行](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)。  
  
## <a name="create-measures"></a>建立量值  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>若要建立 DaysCurrentQuarterToDate 量值與 DimDate 資料表中  
  
1.  在模型設計師中，按一下**DimDate**資料表。  
  
2.  在量值方格中，按一下左上方的空資料格。  
  
3.  在公式列中，輸入下列公式：  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    請注意左上資料格現在包含量值名稱， **DaysCurrentQuarterToDate**，後面接著結果**92**。 結果無關此時因為沒有使用者篩選已經套用。
    
      ![做為 lesson6 newmeasure](../tutorial-tabular-1400/media/as-lesson6-newmeasure.png) 
    
    不同於導出資料行，量值公式與您可以輸入量值名稱，後面接著冒號，後面接著公式的運算式。

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>若要建立 DaysInCurrentQuarter 量值與 DimDate 資料表中  
  
1.  與**DimDate**資料表仍為使用中模型設計師中，在量值方格中，按一下您所建立的量值下方的空白資料格。  
  
2.  在公式列中，輸入下列公式：  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    當建立一個不完整期間與前一個期間之間的比率。 公式必須計算期間已過，與前一個期間中的相同比例比較的比例。 在這種情況下，[DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 提供比例經過目前期間內。  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>在 [FactInternetSales] 資料表中建立 InternetDistinctCountSalesOrder 量值  
  
1.  按一下**FactInternetSales**資料表。   
  
2.  按一下**SalesOrderNumber**資料行標題。  
  
3.  在工具列上按一下 [自動加總] \(**∑**) 按鈕旁的向下箭號，然後選取 [DistinctCount]。  
  
    [自動加總] 功能會使用 DistinctCount 標準彙總公式，自動為選取的資料行建立量值。  
    
       ![as-lesson6-newmeasure2](../tutorial-tabular-1400/media/as-lesson6-newmeasure2.png)
  
4.  在量值方格中，按一下 新增量值，然後在**屬性**視窗，請在**量值名稱**，重新命名量值**InternetDistinctCountSalesOrder**。 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>FactInternetSales 資料表中建立其他量值  
  
1.  使用 [自動加總] 功能建立並命名下列量值：  

    |資料行|量值名稱|自動加總 (∑)|公式|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Count|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|SUM|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|SUM|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|SUM|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|SUM|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|SUM|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|SUM|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|SUM|=SUM([Freight])|  
  
2.  藉由按一下量值方格中的空資料格以及使用公式列中，建立，順序中的下列自訂量值：  
  
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

[第 7 課： 建立關鍵效能指標](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)。  

  
