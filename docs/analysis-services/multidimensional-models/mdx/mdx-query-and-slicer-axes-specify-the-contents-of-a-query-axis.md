---
title: "指定查詢座標軸 (MDX) 的內容 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cellsets [MDX]
- query axis [MDX]
ms.assetid: c745ade0-738e-4a98-a3f0-3eabfd3eeba2
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b8149620e62d94c97cfb499006d55b798c829324
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-query-and-slicer-axes---specify-the-contents-of-a-query-axis"></a>MDX 查詢及 Slicer 軸-指定查詢座標軸的內容
  查詢座標軸指定多維度運算式 (MDX) SELECT 陳述式傳回的資料格集邊緣。 指定資料格集邊緣，您就可以限制用戶端能看見的傳回資料。  
  
 若要指定查詢座標軸，您可以使用 `<SELECT query axis clause>` ，將集合指派給特定查詢座標軸。 每個 `<SELECT query axis clause>` 值定義一個查詢座標軸。 資料集中的座標軸數等於 SELECT 陳述式中的 `<SELECT query axis clause>` 值。  
  
## <a name="query-axis-syntax"></a>查詢座標軸語法  
 以下語法顯示 `<SELECT query axis clause>`的語法：  
  
```  
  
<SELECT query axis clause> ::=  
   [ NON EMPTY ] Set_Expression [ <SELECT dimension property list clause> ] [<HAVING clause>]  
   ON {  
      Integer_Expression |   
      AXIS( Integer_Expression ) |   
      {COLUMNS | ROWS | PAGES | SECTIONS | CHAPTERS}     
      }  
  
```  
  
 每一個查詢座標軸都有一個號碼：x-軸是零 (0)，y-軸是 1，z-軸是 2，依此類推。 在 `<SELECT query axis clause>`的語法中， `Integer_Expression` 值指定座標軸數目。 MDX 查詢最多可以支援 128 個指定座標軸，但只有極少數的 MDX 查詢會使用 5 個以上的座標軸。 對於前 5 個座標軸，可改為使用別名 COLUMNS、ROWS、PAGES、SECTIONS 與 CHAPTERS。  
  
 MDX 查詢無法略過查詢座標軸。 也就是說，包含一個或多個查詢座標軸的查詢絕不能排除編號較低或中間的座標軸。 例如，查詢不可以只有 ROWS 座標軸，而沒有 COLUMNS 座標軸，或者有 COLUMNS 與 PAGES 座標軸，但沒有 ROWS 座標軸。  
  
 但是，您可以指定沒有座標軸的 SELECT 子句 (也就是說，一個空的 SELECT 子句)。 在此狀況下，所有的維度都是切片維度，且 MDX 查詢選取一個資料格。  
  
 在先前顯示的查詢座標軸語法中， `Set_Expression` 值指定了定義查詢座標軸內容的集合。 如需集合的詳細資訊，請參閱[使用成員、Tuple 和集合 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)。  
  
## <a name="examples"></a>範例  
 下列簡單的 SELECT 陳述式會傳回 Columns 軸上的量值 Internet Sales Amount，並且使用 MDX MEMBERS 函數傳回 Rows 軸的 Date 維度上，Calendar 階層的所有成員：  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
{[Date].[Calendar].MEMBERS} ON ROWS  
FROM [Adventure Works]  
  
```  
  
 後續兩個查詢會傳回完全相同的結果，但是會示範使用軸數，而非別名：  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON 0,  
{[Date].[Calendar].MEMBERS} ON 1  
FROM [Adventure Works]  
  
SELECT {[Measures].[Internet Sales Amount]} ON AXIS(0),  
{[Date].[Calendar].MEMBERS} ON AXIS(1)  
FROM [Adventure Works]  
  
```  
  
 在設定定義之前使用的 NON EMPTY 關鍵字是從軸中移除所有空白 Tuple 的簡單方式。 例如，在目前為止的範例中，我們已看到 2004 年 8 月以後的 Cube 中沒有任何資料。 若要從任何資料行都沒有資料的資料格集中移除所有資料列，只要在設定 Rows 軸定義之前加入 NON EMPTY 即可，如下所示：  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].MEMBERS} ON ROWS  
FROM [Adventure Works]  
  
```  
  
 NON EMPTY 可以在查詢中的所有軸上使用。 比較下面兩個查詢的結果，第一個未使用 NON EMPTY，第二個則在兩個軸上都使用：  
  
```  
SELECT {[Measures].[Internet Sales Amount]}   
* [Promotion].[Promotion].[Promotion].MEMBERS  
ON COLUMNS,  
{[Date].[Calendar].[Calendar Year].MEMBERS} ON ROWS  
FROM [Adventure Works]  
WHERE([Product].[Subcategory].&[19])  
  
SELECT NON EMPTY {[Measures].[Internet Sales Amount]}   
* [Promotion].[Promotion].[Promotion].MEMBERS  
ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].[Calendar Year].MEMBERS} ON ROWS  
FROM [Adventure Works]  
WHERE([Product].[Subcategory].&[19])  
  
```  
  
 HAVING 子句可以依據特定準則篩選軸的內容；雖然它的彈性比其他可達成相同結果的方法小 (例如 FILTER 函數)，不過它比較容易使用。 以下範例只會傳回 Internet Sales Amount 大於 $15,000 的日期：  
  
```  
SELECT {[Measures].[Internet Sales Amount]}   
ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].[Date].MEMBERS}   
HAVING [Measures].[Internet Sales Amount]>15000  
ON ROWS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>請參閱＜  
 [指定 Slicer 軸的內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)  
  
  

