---
title: 使用集合函式 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ca9c5e1a3e110e1f1f2f14e9bd9b52e245d457a6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251595"
---
# <a name="using-set-functions"></a>使用集合函數


  集合函數可以擷取維度、階層、層級的集合，或是在這些物件內成員的絕對與相對位置往返，以許多方式建構集合。  
  
 集合函數跟成員函數與 tuple 函數一樣，對於交涉 Analysis Services 中找到的多維度結構而言不可或缺。 因為集合運算式會定義 MDX 查詢的座標軸，所以要取得多維度運算式 (MDX) 查詢的結果也必須要有集合函數。  
  
 其中一個最常見的 set 函式是[成員&#40;設定&#41; &#40;MDX&#41; ](../mdx/members-set-mdx.md)函式，它會擷取包含所有從維度、 階層或層級成員的集合。 下列是它在查詢中的範例用法：  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns all of the members on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 另一個常用的函數是[Crossjoin &#40;MDX&#41; ](../mdx/crossjoin-mdx.md)函式。 它會傳回一組 tuple，代表當做參數傳給它的 cartesian 產品集合。 在實際用語中，這個函數會讓您在查詢中建立「巢狀」或 CROSSTAB 座標軸：  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns a set containing every combination of all of the members`  
  
 `//on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension and all of the members on the Category level`  
  
 `//of the Category hierarchy on the Product dimension`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 [子代&#40;MDX&#41; ](../mdx/descendants-mdx.md)函數很相似**子系**函式，但是功能比較強大。 它會在階層中的一個或多個層級上傳回任何成員的下階：  
  
 SELECT  
  
 [Measures].[Internet Sales Amount]  
  
 ON Columns,  
  
 //Returns a set containing all of the Dates beneath Calendar Year  
  
 //2004 in the Calendar hierarchy of the Date dimension  
  
 DESCENDANTS(  
  
 [日期]。[行事曆]。[Calendar Year]。 & [2004]  
  
 , [Date].[Calendar].[Date])  
  
 ON Rows  
  
 FROM [Adventure Works]  
  
 [順序&#40;MDX&#41; ](../mdx/order-mdx.md)函式可讓您一組以遞增或遞減順序，根據特定的數值運算式的內容。 下列查詢會傳回與前一查詢相同的資料列成員，但是現在會根據 Internet Sales Amount 量值加以排序：  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//ordered by Internet Sales Amount`  
  
 `ORDER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount], BDESC)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 這個查詢也會說明從一個集合函數 Descendants 傳回的集合要如何當做參數傳遞給另一個集合函數 Order。  
  
 篩選一組根據特定準則時，很有幫助撰寫查詢，並針對此目的，您可以使用[篩選&#40;MDX&#41; ](../mdx/filter-mdx.md)函式，如下列範例所示：  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//where Internet Sales Amount is greater than $70000`  
  
 `FILTER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount]>70000)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 也有其他更複雜的函數可讓您以其他方式篩選集合。 例如，下列查詢會顯示[TopCount &#40;MDX&#41; ](../mdx/topcount-mdx.md)函式傳回集合中的前 n 個項目：  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing the top 10 Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension by Internet Sales Amount`  
  
 `TOPCOUNT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,10, [Measures].[Internet Sales Amount])`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 最後就能夠執行使用類似的邏輯集合作業的數量[Intersect &#40;MDX&#41;](../mdx/intersect-mdx.md)，[聯集&#40;MDX&#41; ](../mdx/union-mdx.md)並[&#40;MDX&#41; ](../mdx/except-mdx-function.md)函式。 下列查詢顯示後兩個函數的範例：  
  
 `SELECT`  
  
 `//Returns a set containing the Measures Internet Sales Amount, Internet Tax Amount and`  
  
 `//Internet Total Product Cost`  
  
 `UNION(`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}`  
  
 `, {[Measures].[Internet Total Product Cost]}`  
  
 `)`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//except the January 1st 2004`  
  
 `EXCEPT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,{[Date].[Calendar].[Date].&[915]})`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [函式&#40;MDX 語法&#41;](../mdx/functions-mdx-syntax.md)   
 [使用成員函式](../mdx/using-member-functions.md)   
 [使用 Tuple 函式](../mdx/using-tuple-functions.md)  
  
  
