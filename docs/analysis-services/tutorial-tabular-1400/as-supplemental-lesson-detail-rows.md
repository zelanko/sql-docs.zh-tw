---
title: Analysis Services 教學課程補充課程： 詳細資料列 |Microsoft Docs
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 28c5124508cedca026d262e34257bf48518580fb
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43078651"
---
# <a name="supplemental-lesson---detail-rows"></a>補充課程 - 詳細資料列

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在此補充課程中，您可以使用 DAX 編輯器來定義自訂的詳細資料列運算式。 詳細資料列運算式是屬性，以量值，提供使用者有關量值的彙總結果的詳細資訊。 
  
完成本課程的估計時間： **10 分鐘**  
  
## <a name="prerequisites"></a>先決條件  

本文補充課程是表格式模型教學課程的一部分。 執行工作之前在此補充課程中，您應已完成所有先前的課程或已完成的 Adventure Works Internet Sales 範例模型專案。  
  
## <a name="whats-the-issue"></a>什麼是問題？

讓我們看看 InternetTotalSales 量值的詳細資料再新增詳細資料列運算式。

1.  在 SSDT 中，按一下**模型**功能表 >**在 Excel 中的進行分析**以開啟 Excel 並建立空白的樞紐分析表。
  
2.  在 **樞紐分析表欄位**，新增**InternetTotalSales** FactInternetSales 資料表的量值**值**， **CalendarYear**從若要在 DimDate 資料表**資料行**，和**EnglishCountryRegionName**來**的資料列**。 樞紐分析表現在會提供 InternetTotalSales 量值，依照區域和年度的彙總的結果。 

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-pivottable.png)

3. 在樞紐分析表中，按兩下彙的總值年度和區域名稱。 我們在此按兩下澳洲 2014 年值。 包含資料，但非實用資料的新工作表隨即開啟。

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-sheet.png)
  
我們想要查看以下是包含資料行和構成 InternetTotalSales 量值的彙總結果資料列的資料表。 若要這樣做，我們可以新增詳細資料列運算式，當做量值的屬性。

## <a name="add-a-detail-rows-expression"></a>新增詳細資料列運算式

#### <a name="to-create-a-detail-rows-expression"></a>若要建立詳細資料列運算式 
  
1. 在 FactInternetSales 資料表的量值方格中，按一下**InternetTotalSales**量值。 

2. 在 **屬性** > **詳細資料列運算式**，按一下編輯器按鈕以開啟 DAX 編輯器。

    ![as-lesson-detail-rows-ellipse](../tutorial-tabular-1400/media/as-lesson-detail-rows-ellipse.png)

3. 在 [DAX 編輯器] 中，輸入下列運算式：

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    此運算式會指定名稱、 資料行，以及當使用者按兩下樞紐分析表或報告中的彙總的結果時，會傳回從 FactInternetSales 資料表和相關的資料表的量值結果。

4. 傳回在 Excel 中，刪除在步驟 3 中建立的工作表，然後按兩下彙的總值。 此時，定義量值詳細資料列運算式屬性，新的工作表隨即開啟包含更多有用的資料。

    ![as-lesson-detail-rows-detailsheet](../tutorial-tabular-1400/media/as-lesson-detail-rows-detailsheet.png)

5. 重新部署您的模型。

  
## <a name="see-also"></a>另請參閱  

[SELECTCOLUMNS 函式 (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)  
[補充課程 - 動態安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[補充課程 - 不完全階層](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)  
