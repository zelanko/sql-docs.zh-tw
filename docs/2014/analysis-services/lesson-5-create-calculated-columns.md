---
title: 第 6 課：建立計算結果的欄 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: adc7b7bf3335c8c9c7530d18f4d553492cfe9e1b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728636"
---
# <a name="lesson-6-create-calculated-columns"></a>第 6 課：建立導出資料行
  在這一課，您將藉由加入導出資料行的方式在模型中建立新資料。 導出資料行是以已存在模型中的資料為基礎。 如需詳細資訊，請參閱[導出資料行 &#40;SSAS 表格式&#41;](tabular-models/ssas-calculated-columns.md)。  
  
 您將在三個不同的資料表中建立五個新的導出資料行。 各項工作的步驟稍有不同。 這樣做的目的在於說明，您可以透過數種方式建立新的資料行、重新命名資料行，以及將它們放到資料表中的不同位置。  
  
 估計的時間才能完成這一課：**15 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
 本主題是表格式模型教學課程的一部分，必須依序完成。 執行工作之前在這一課，您應已完成上一課：[第 5 課：建立關聯性](lesson-4-create-relationships.md)。  
  
## <a name="create-calculated-columns"></a>建立導出資料行  
  
#### <a name="create-a-month-calendar-calculated-column-in-the-date-table"></a>在日期資料表中建立 Month Calendar 導出資料行  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，按一下 [模型] 功能表，然後指向 [模型檢視]，再按一下 [資料檢視]。  
  
     導出資料行只能使用模型設計師在「資料檢視」中建立。  
  
2.  在模型設計師中，按一下 [Date] 資料表 (索引標籤)。  
  
3.  以滑鼠右鍵按一下**日曆季**資料行，然後再按一下**插入資料行**。  
  
     新的資料行，名為**CalculatedColumn1**插入至左邊**日曆季**資料行。  
  
4.  在資料表上方的公式列中，輸入下列公式。 「自動完成」可協助您輸入資料行和資料表的完整名稱，以及列出可用的函數。  
  
     `=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]`  
  
     完成建立公式時，按 ENTER。  
  
     接著導出資料行中的所有資料列就會填入值。 如果您向下捲動資料表，將會看到此資料行的資料列可以根據每個資料列中的資料而擁有不同的值。  
  
    > [!NOTE]  
    >  如果您收到錯誤，請確認公式中的資料行名稱符合您在中變更的資料行名稱[第 3 課：重新命名資料行](rename-columns.md)。  
  
5.  重新命名此資料行`Month Calendar`。  
  
 Month Calendar 導出資料行會提供可排序的月份名稱。  
  
#### <a name="create-a-day-of-week-calculated-column-in-the-date-table"></a>在日期資料表中建立 Day of Week 導出資料行  
  
1.  在 [日期] 資料表仍為使用中狀態時，按一下 [資料行] 功能表，然後按一下 [加入資料行]。  
  
     新的資料行就會加入資料表的最右側。  
  
2.  在公式列中，輸入下列公式：  
  
     `=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]`  
  
     完成建立公式時，按 ENTER。  
  
3.  重新命名的資料行`Day of Week`。  
  
4.  按一下欄位標題，然後將資料行拖曳到 [Day Name] 資料行和 [Day of Month] 資料行之間。  
  
    > [!TIP]  
    >  移動資料表中的資料行可使導覽更方便。  
  
 [Day of Week] 導出資料行會提供可排序的星期日期名稱。  
  
#### <a name="create-a-product-subcategory-name-calculated-column-in-the-product-table"></a>在產品資料表中建立 Product Subcategory Name 導出資料行  
  
1.  在模型設計師中，選取 [產品] 資料表。  
  
2.  捲動到資料表的最右側。 您會發現，最右側的資料行命名為 [加入資料行] (斜體)，請按一下該欄位標題。  
  
3.  在公式列中，輸入下列公式。  
  
     `=RELATED('Product Subcategory'[Product Subcategory Name])`  
  
     完成建立公式時，按 ENTER。  
  
4.  重新命名的資料行`Product Subcategory Name`。  
  
 [Product Subcategory Name] 導出資料行可用來在 [產品] 資料表中建立階層，其中包括來自 [產品子類別目錄] 資料表中 [Product Subcategory Name] 資料行的資料。 階層不可跨越多個資料表。 您稍後將在第 7 課中建立階層。  
  
#### <a name="create-a-product-category-name-calculated-column-in-the-product-table"></a>在產品資料表中建立 Product Category Name 導出資料行  
  
1.  在 [產品] 資料表仍為使用中狀態時，按一下 [資料行] 功能表，然後按一下 [加入資料行]。  
  
2.  在公式列中，輸入下列公式：  
  
     `=RELATED('Product Category'[Product Category Name])`  
  
     完成建立公式時，按 ENTER。  
  
3.  重新命名的資料行`Product Category Name`。  
  
 [Product Category Name] 導出資料行可用來在 [產品] 資料表中建立階層，其中包括來自 [產品類別目錄] 資料表中 [Product Category Name] 資料行的資料。 階層不可跨越多個資料表。  
  
#### <a name="create-a-margin-calculated-column-in-the-internet-sales-table"></a>在網際網路銷售資料表中建立 Margin 導出資料行  
  
1.  在模型設計師中，選取 [網際網路銷售] 資料表。  
  
2.  加入新資料行。  
  
3.  在公式列中，輸入下列公式：  
  
     `=[Sales Amount]-[Total Product Cost]`  
  
     完成建立公式時，按 ENTER。  
  
4.  重新命名的資料行`Margin`。  
  
5.  將這個資料行拖曳至 [Sales Amount] 資料行和 [Tax Amt] 資料行之間。  
  
 [Margin] 導出資料行可用來分析每個 (產品) 資料列的利率。  
  
## <a name="next-step"></a>下一個步驟  
 若要繼續這一課，請移至下一課：[第 7 課：建立量值](lesson-6-create-measures.md)。  
  
  
