---
title: Analysis Services 教學課程第 5 課：建立計算結果的欄 |Microsoft Docs
ms.date: 04/25/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: b56fe07237faa6570fd4b8c1adb31d3cce8e4540
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "64776066"
---
# <a name="create-calculated-columns"></a>建立導出資料行

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您建立資料模型中加入導出資料行。 您可以建立導出資料行 （作為自訂資料行） 時使用 取得資料，使用查詢編輯器中，或稍後在模型設計工具類似您執行以下。 若要進一步了解，請參閱[導出資料行](../tabular-models/ssas-calculated-columns.md)。
  
您可以建立五個新的導出資料行中，三個不同的資料表。 步驟會稍有不同顯示有數種方式建立資料行、 重新命名，並將它們放在資料表中的不同位置的每個工作項目。  

這一課也是第一次使用 Data Analysis Expressions (DAX)。 DAX 是一種特殊的語言來建立高度自訂的表格式模型的公式運算式。 在本教學課程中，您可以使用 DAX 來建立導出資料行、 量值和角色篩選條件。 若要進一步了解，請參閱[表格式模型中的 DAX](../tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)。 
  
估計的時間才能完成這一課：**15 分鐘**  
  
## <a name="prerequisites"></a>先決條件  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 執行工作之前在這一課，您應已完成上一課：[第 4 課：建立關聯性](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)。 
  
## <a name="create-calculated-columns"></a>建立導出資料行  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>在 DimDate 資料表中建立 MonthCalendar 計算結果的欄  
  
1.  按一下 **模型**功能表 >**模型檢視** > **資料檢視**。  
  
    導出資料行只能使用模型設計師在「資料檢視」中建立。  
  
2.  在模型設計師中，按一下**DimDate**資料表 （標籤）。  
  
3.  以滑鼠右鍵按一下**CalendarQuarter**資料行標頭，，然後按一下**插入資料行**。  
  
    名為 [Calculated Column 1]  的新資料行將會插入 [日曆季]  資料行的左側。  
  
4.  在資料表上方的公式列中輸入下列 DAX 公式：自動完成協助您輸入的資料行和資料表的完整格式的名稱，並列出可用的函式。  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    接著導出資料行中的所有資料列就會填入值。 如果您向下捲動到資料表，您會看到資料列可以有不同的值，這個資料行，根據每個資料列中的資料。    
  
5.  重新命名此資料行**MonthCalendar**。 

    ![as-lesson5-newcolumn](../tutorial-tabular-1400/media/as-lesson5-newcolumn.png) 
  
MonthCalendar 計算結果欄提供可排序的月份名稱。  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>在 DimDate 資料表中建立 DayOfWeek 計算結果的欄  
  
1.  具有**DimDate**資料表仍在作用中，按一下 **資料行**功能表，然後再按一下**加入資料行**。  
  
2.  在公式列中，輸入下列公式：  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    當您完成建立公式時，請按 ENTER 鍵。 新的資料行就會加入資料表的最右側。  
  
3.  重新命名的資料行**DayOfWeek**。  
  
4.  按一下 資料行標題，，然後將拖曳的資料行之間**EnglishDayNameOfWeek**資料行和有**DayNumberOfMonth**資料行。  
  
    > [!TIP]  
    > 移動資料表中的資料行可使導覽更方便。  
  
DayOfWeek 計算結果欄提供可排序的星期幾名稱。  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>在 DimProduct 資料表中建立 ProductSubcategoryName 計算結果的欄  
  
  
1.  在  **DimProduct**資料表中，捲動到右邊的資料表。 請注意名為最右側資料行***加入資料行***，按一下 資料行標題。  
  
2.  在公式列中，輸入下列公式：  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  重新命名的資料行**ProductSubcategoryName**。  
  
ProductSubcategoryName 計算結果的欄用於在 DimProduct 資料表中，納入 DimProductSubcategory 資料表之 EnglishProductSubcategoryName 資料行的資料建立階層。 階層不可跨越多個資料表。 您稍後在第 9 課中建立階層。  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>在 DimProduct 資料表中建立 ProductCategoryName 計算結果的欄  
  
1.  具有**DimProduct**資料表仍在作用中，按一下 **資料行**功能表，然後再按一下**加入資料行**。  
  
2.  在公式列中，輸入下列公式：  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  重新命名的資料行**ProductCategoryName**。  
  
ProductCategoryName 計算結果的欄用於在 DimProduct 資料表中，納入 DimProductCategory 資料表之 EnglishProductCategoryName 資料行的資料建立階層。 階層不可跨越多個資料表。  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>在 FactInternetSales 資料表中建立 Margin 計算結果的欄  
  
1.  在模型設計師中，選取**FactInternetSales**資料表。  
  
2.  建立新的導出資料行之間**SalesAmount**資料行和有**TaxAmt**資料行。  
  
3.  在公式列中，輸入下列公式：  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  將這個資料行重新命名為 **Margin**。  
 
      ![as-lesson5-newmargin](../tutorial-tabular-1400/media/as-lesson5-newmargin.png)
      
    Margin 計算結果的欄用來分析每個銷售的利率。  
  
## <a name="whats-next"></a>下一步

[第 6 課：建立量值](../tutorial-tabular-1400/as-lesson-6-create-measures.md)。
  
  
  
