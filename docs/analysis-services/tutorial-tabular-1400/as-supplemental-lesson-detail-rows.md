---
title: Analysis Services 教學課程，補充課程： 詳細資料列 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0518cdd7707c5973bfd055af997a75c9b67d7479
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34045742"
---
# <a name="supplemental-lesson---detail-rows"></a>補充課程-詳細資料列

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這個補充課程中，您可以使用 DAX 編輯器來定義自訂的詳細資料列運算式。 詳細資料列運算式是量值，屬性提供使用者有關彙總結果的量值的詳細資訊。 
  
完成本課程的估計時間：**10 分鐘**  
  
## <a name="prerequisites"></a>필수 구성 요소  

本文補充課程是表格式模型教學課程的一部分。 然後再執行工作，這個補充課程中，您應已完成所有先前的課程或已完成的 Adventure Works Internet Sales 範例模型專案。  
  
## <a name="whats-the-issue"></a>什麼是問題？

讓我們看看 InternetTotalSales 量值的詳細資料然後再加入詳細資料列運算式。

1.  在 SSDT 中，按一下 **模型**功能表 >**在 Excel 中的進行分析**開啟 Excel，並建立空白的樞紐分析表。
  
2.  在**樞紐分析表欄位**，新增**InternetTotalSales** FactInternetSales 資料表中的量值**值**， **CalendarYear** DimDate 資料表的**資料行**，和**EnglishCountryRegionName**至**列**。 樞紐分析表現在會提供從依區域和年份 InternetTotalSales 量值的彙總的結果。 

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-pivottable.png)

3. 在樞紐分析表中，按兩下彙總值的年份和地區名稱。 這裡我們按兩下澳大利亞及 2014 年的值。 新的工作表隨即開啟其中包含資料，但無用處的資料。

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-sheet.png)
  
我們想要看到如下的表格，內含資料行和構成 InternetTotalSales 量值的彙總的結果資料列。 若要這樣做，我們可以加入詳細資料列運算式作為量值的屬性。

## <a name="add-a-detail-rows-expression"></a>加入詳細資料列運算式

#### <a name="to-create-a-detail-rows-expression"></a>若要建立詳細資料列運算式 
  
1. 在 FactInternetSales 資料表的量值方格中，按一下  **InternetTotalSales**量值。 

2. 在**屬性** > **詳細資料列運算式**，按一下 編輯 按鈕以開啟 DAX 編輯器。

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

    這個運算式會指定名稱，資料行，以及當使用者按兩下彙總的結果在樞紐分析表或報表中會傳回從 FactInternetSales 資料表和相關的資料表的量值結果。

4. 傳回在 Excel 中，刪除步驟 3 中建立的工作表，然後按兩下彙總的值。 這次的詳細資料列運算式內容來定義量值，新的工作表會開啟包含更多有用的資料。

    ![as-lesson-detail-rows-detailsheet](../tutorial-tabular-1400/media/as-lesson-detail-rows-detailsheet.png)

5. 重新部署您的模型。

  
## <a name="see-also"></a>另請參閱  

[SELECTCOLUMNS 函數 (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)  
[補充課程 - 動態安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[補充課程 - 不完全階層](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)  
