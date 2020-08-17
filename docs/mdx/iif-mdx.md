---
description: IIf (MDX)
title: IIf (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8a9a8da3ec20a34ba1dea30b1285d6a9c147e55d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387464"
---
# <a name="iif-mdx"></a>IIf (MDX)


  根據 Boolean 條件為 true 或 false 來評估不同的分支運算式。  
  
## <a name="syntax"></a>語法  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>引數  
 IIf 函式會採用三個引數： iif (\<condition> 、 \<then branch> 、 \<else branch>) 。  
  
 *Logical_Expression*  
 評估為 **true** (1) 或 **false** (0) 的條件。 它必須是有效的多維度運算式 (MDX) 邏輯運算式。  
  
 *運算式運算式提示 [積極 |Strict |延遲]]*  
 當邏輯運算式評估為 **true**時使用。 Expression1 必須是有效的多維度運算式 (MDX) 運算式。  
  
 *運算式提示 [積極 |Strict |延遲]]*  
 當邏輯運算式評估為 **false**時使用。 Expression2 必須是有效的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 當此運算式的值為零時，由邏輯運算式指定的條件會評估為 **false** 。 任何其他值都會評估為 **true**。  
  
 當條件為 **true**時， **IIf** 函數會傳回第一個運算式。 否則，此函數會傳回第二個運算式。  
  
 指定的運算式可以傳回值或 MDX 物件。 而且，指定的運算式不需要類型相符。  
  
 不建議根據搜尋準則來建立一組成員的 **IIf** 函數。 相反地，請使用 [Filter](../mdx/filter-mdx.md) 函數來評估指定之集合中的每個成員是否針對邏輯運算式，並傳回成員子集。  
  
> [!NOTE]  
>  如果任何一個運算式評估為 NULL，符合該條件時，結果集將是 NULL。  
  
 提示是選擇性的修飾詞，可決定評估運算式的方式和時機。 它可讓您藉由指定運算式的評估方式來覆寫預設查詢計畫。  
  
-   EAGER 會針對原始 IIF 子空間來評估運算式。  
  
-   STRICT 只評估由邏輯條件運算式所建立之限制子空間內的運算式。  
  
-   LAZY 會依照逐資料格模式來評估運算式。  
  
 EAGER 和 STRICT 只適用於 IIF 的 then-else 分支，LAZY 則適用於所有 MDX 運算式。 所有 MDX 運算式後面都可以跟著 HINT LAZY，後者將會依照逐資料格模式來評估該運算式。  
  
 EAGER 和 STRICT 在提示中互斥，它們可以在不同的運算式中，用於相同的 IIF(,,)。  
  
 如需詳細資訊，請參閱 [SQL Server Analysis Services 2008 中的 IIF 函數查詢提示](http://www.ssas-info.com/analysis-services-articles/50-mdx/1103-iif-function-query-hints-in-sql-server-analysis-services-2008) ，以及 [MDX IIF 函數和 CASE 語句的執行計畫和計畫提示](https://go.microsoft.com/fwlink/?LinkId=269565)。  
  
## <a name="examples"></a>範例  
 下列查詢顯示當量值網際網路銷售量大於或小於 $10000 時，在匯出量值內使用 **IIF** 的簡單用法，以傳回兩個不同字串值的其中一個：  
  
 `WITH MEMBER MEASURES.IIFDEMO AS`  
  
 `IIF([Measures].[Internet Sales Amount]>10000`  
  
 `, "Sales Are High", "Sales Are Low")`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.IIFDEMO} ON 0,`  
  
 `[Date].[Date].[Date].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 IIF 的常見用法是在導出量值內處理「除數為零」的錯誤，如以下範例所示：  
  
 `WITH`  
  
 `//Returns 1.#INF when the previous period contains no value`  
  
 `//but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth With Errors] AS`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `,FORMAT_STRING='PERCENT'`  
  
 `//Traps division by zero and returns null when the previous period contains`  
  
 `//no value but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth] AS`  
  
 `IIF(([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)=0,`  
  
 `NULL,`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `),FORMAT_STRING='PERCENT'`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.[Previous Period Growth With Errors], MEASURES.[Previous Period Growth]} ON 0,`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004],`  
  
 `[Date].[Calendar].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 下列範例會在產生函數中傳回兩個 **集合的其中** 一個，以在資料列上建立一組複雜的元組：  
  
 `SELECT {[Measures].[Internet Sales Amount]} ON 0,`  
  
 `//If Internet Sales Amount is zero or null`  
  
 `//returns the current year and the All Customers member`  
  
 `//else returns the current year broken down by Country`  
  
 `GENERATE(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `, IIF([Measures].[Internet Sales Amount]=0,`  
  
 `{([Date].[Calendar Year].CURRENTMEMBER, [Customer].[Country].[All Customers])}`  
  
 `, {{[Date].[Calendar Year].CURRENTMEMBER} * [Customer].[Country].[Country].MEMBERS}`  
  
 `))`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 最後，這個範例示範計畫提示的用法：  
  
 `WITH MEMBER MEASURES.X AS`  
  
 `IIF(`  
  
 `[Measures].[Internet Sales Amount]=0`  
  
 `, NULL`  
  
 `, (1/[Measures].[Internet Sales Amount]) HINT EAGER)`  
  
 `SELECT {[Measures].x} ON 0,`  
  
 `[Customer].[Customer Geography].[Country].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
