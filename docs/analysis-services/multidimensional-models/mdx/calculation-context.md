---
title: 計算內容 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 340d03ba8d0c5a66d89937627ab9389fc49abcae
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021765"
---
# <a name="calculation-context"></a>計算內容
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  計算內容是 Cube 中評估運算式以及所有座標為明確已知或可衍生自運算式的已知子空間。  
  
## <a name="determining-the-calculation-context"></a>決定計算內容  
 每個集合、成員、Tuple 或數值函數都是在整個 MDX 運算式或陳述式的內容中執行。 傳遞引數 (例如 Tuple) 至函數時，只會明確提供 Cube 空間中的部分座標。 其他座標是根據目前的計算內容取得。  
  
 未指定之資料格座標和屬性成員的計算內容是依下列順序決定：  
  
1.  FROM 子句 (如果有的話) - 採用 SELECT 陳述式的格式，這個子句可以指定整個 Cube，也可以指定 Subcube。  
  
2.  WHERE 子句 (如果有的話) - 這個子句也稱為「slicer 軸」，用來指定集合、Tuple 或成員，可限制查詢所傳回之欄軸和列軸上的成員。 概念上，資料行或資料列軸上沒有明確指定之每個屬性階層的預設成員都是 slicer 座標軸的一部分。  
  
    > [!NOTE]  
    >  當 slicer 座標軸和另一個座標軸上指定了特定屬性的資料格座標時，函數中指定的座標會優先使用來決定座標軸上的成員集合。 [Filter (MDX)](../../../mdx/filter-mdx.md) 和 [Order (MDX)](../../../mdx/order-mdx.md) 函數是這類函數的範例 - 您可以使用 WHERE 子句，或 FROM 子句的 SELECT 陳述式，依據從計算內容排除的屬性成員來篩選或排序結果。  
  
3.  在查詢或運算式中定義的命名集和導出成員。  
  
4.  資料列和資料行軸上指定的 Tuple 和集合，利用資料列、資料行或 slicer 座標軸上沒有出現之屬性的預設成員。  
  
5.  每個座標軸上的 Cube 或 Subcube 資料格，刪除座標軸上的空 Tuple 並且套用 HAVING 子句。  
  
6.  如需詳細資訊，請參閱[查詢 & #40; 在建立 Cube 內容MDX & #41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md).  
  
 在下列查詢中，資料列軸的計算內容受到 WHERE 子句中指定之 Country 屬性成員和 Calendar Year 屬性成員限制。  
  
```  
SELECT Customer.City.City.Members ON 0  
FROM [Adventure Works]  
WHERE (Customer.Country.France, [Date].[Calendar].[Calendar Year].[CY 2004],  
   Measures.[Internet Sales Amount])  
```  
  
 然而，如果您透過指定資料列軸上之 **FILTER** 函數的方式修改這個查詢，並且利用 **FILTER** 函數中的 Calendar Year 屬性階層成員，就可以修改 Calendar Year 屬性階層的屬性成員，這是用來提供資料行軸上集合成員的計算內容。  
  
```  
SELECT FILTER  
   (  
      Customer.City.City.Members,   
         ([Date].[Calendar].[Calendar Year].[CY 2003],  
            Measures.[Internet Order Quantity]) > 75   
   ) ON 0  
FROM [Adventure Works]  
WHERE (Customer.Country.France,  
   [Date].[Calendar].[Calendar Year].[CY 2004],  
   Measures.[Internet Sales Amount])  
```  
  
 在上述查詢中，資料行軸上所出現之 Tuple 內資料格的計算內容是依 Calendar Year 屬性階層的 CY 2003 成員篩選，可是 Calendar Year 屬性階層的名義計算內容則是 CY 2004。 此外，它是依 Internet Order Quantity 量值篩選。 然而，一旦設定資料行軸上的集合成員，座標軸上所出現成員之值的計算內容會再度由 WHERE 子句決定。  
  
> [!IMPORTANT]  
>  為了提高查詢效能，您應在解析程序中盡早刪除成員和 Tuple。 如此一來，最終一個成員集合上的複雜查詢階段計算便會在最少資料格上運作。  
  
## <a name="see-also"></a>另請參閱  
 [建立查詢 & #40; 中的 Cube 內容MDX & #41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)   
 [MDX 查詢基礎觀念 & #40;Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [MDX & #40; 中的重要概念Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  
