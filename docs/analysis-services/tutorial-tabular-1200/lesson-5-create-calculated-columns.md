---
title: 第 5 課：建立計算結果的欄 |Microsoft Docs
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df9b5a6d490b33b9aea786290acb7454d0066453
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65404180"
---
# <a name="lesson-5-create-calculated-columns"></a>第 5 課：建立導出資料行
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將藉由加入導出資料行的方式在模型中建立新資料。 導出資料行是以已存在模型中的資料為基礎。 若要進一步了解，請參閱[導出資料行](../tabular-models/ssas-calculated-columns.md)。  
  
您將在三個不同的資料表中建立五個新的導出資料行。 各項工作的步驟稍有不同。 這樣做的目的在於說明，您可以透過數種方式建立新的資料行、重新命名資料行，以及將它們放到資料表中的不同位置。  
  
估計的時間才能完成這一課：**15 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 執行工作之前在這一課，您應已完成上一課：[第 4 課：建立關聯性](lesson-4-create-relationships.md)。 
  
## <a name="create-calculated-columns"></a>建立導出資料行  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>在 DimDate 資料表中建立 MonthCalendar 計算結果的欄  
  
1.  按一下 [**模型**功能表 >**模型檢視** > **資料檢視**。  
  
    導出資料行只能使用模型設計師在「資料檢視」中建立。  
  
2.  在模型設計師中，按一下**DimDate**資料表 （標籤）。  
  
3.  以滑鼠右鍵按一下**CalendarQuarter**資料行標頭，，然後按一下**插入資料行**。  
  
    名為 [Calculated Column 1] 的新資料行將會插入 [日曆季] 資料行的左側。  
  
4.  在資料表上方的公式列中，輸入下列公式。 「自動完成」可協助您輸入資料行和資料表的完整名稱，以及列出可用的函數。  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    接著導出資料行中的所有資料列就會填入值。 如果您向下捲動資料表，將會看到此資料行的資料列可以根據每個資料列中的資料而擁有不同的值。    
  
5.  重新命名此資料行**MonthCalendar**。 

    ![as-tabular-lesson5-newcolumn](media/as-tabular-lesson5-newcolumn.png) 
  
MonthCalendar 計算結果欄提供可排序的月份名稱。  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>在 DimDate 資料表中建立 DayOfWeek 計算結果的欄  
  
1.  具有**DimDate**資料表仍為使用中，按一下 [**資料行**功能表，然後再按一下**加入資料行**。  
  
2.  在公式列中，輸入下列公式：  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    當您完成建立公式時，請按 ENTER 鍵。 新的資料行就會加入資料表的最右側。  
  
3.  重新命名的資料行**DayOfWeek**。  
  
4.  按一下資料行標頭，然後拖曳之間的資料行**EnglishDayNameOfWeek**資料行和有**DayNumberOfMonth**資料行。  
  
    > [!TIP]  
    > 移動資料表中的資料行可使導覽更方便。  
  
DayOfWeek 計算結果欄提供可排序的星期幾名稱。  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>在 DimProduct 資料表中建立 ProductSubcategoryName 計算結果的欄  
  
  
1.  在 [ **DimProduct**資料表中，捲動到右邊的資料表。 您會發現，最右側的資料行命名為 [加入資料行] \(斜體)，請按一下該欄位標題。  
  
2.  在公式列中，輸入下列公式。  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  重新命名的資料行**ProductSubcategoryName**。  
  
ProductSubcategoryName 導出資料行用來建立階層，其中包括 [englishproductsubcategoryname] 資料行來自 DimProductSubcategory 資料表中資料的 DimProduct 資料表內。 階層不可跨越多個資料表。 稍後在第 9 課，您將建立階層。  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>在 DimProduct 資料表中建立 ProductCategoryName 計算結果的欄  
  
1.  具有**DimProduct**資料表仍在作用中，按一下 [**資料行**功能表，然後再按一下**加入資料行**。  
  
2.  在公式列中，輸入下列公式：  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  重新命名的資料行**ProductCategoryName**。  
  
ProductCategoryName 導出資料行用來建立階層，其中包括 [englishproductcategoryname] 資料行來自 DimProductCategory 資料表中資料的 DimProduct 資料表內。 階層不可跨越多個資料表。  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>在 FactInternetSales 資料表中建立 Margin 計算結果的欄  
  
1.  在模型設計師中，選取**FactInternetSales**資料表。  
  
2.  加入新資料行。  
  
3.  在公式列中，輸入下列公式：  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  將這個資料行重新命名為 **Margin**。  
  
5.  資料行之間拖曳**SalesAmount**資料行和有**TaxAmt**資料行。 
 
      ![as-tabular-lesson5-newmargin](media/as-tabular-lesson5-newmargin.png)
      
    Margin 計算結果的欄用來分析每個銷售的利率。  
  
## <a name="whats-next"></a>下一步
請移至下一課：[第 6 課：建立量值](lesson-6-create-measures.md)。
  
  
  
