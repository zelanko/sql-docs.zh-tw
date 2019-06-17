---
title: IIf (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0b05929d24533e0bdcdbcac59820307a373428ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63125474"
---
# <a name="iif-mdx"></a>IIf (MDX)


  根據 Boolean 條件為 true 或 false 來評估不同的分支運算式。  
  
## <a name="syntax"></a>語法  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>引數  
 IIf 函式接受三個引數： iif (\<條件 >，\<然後分支 >， \<else 分支 >)。  
  
 *Logical_Expression*  
 條件評估為**真**(1) 或**false** (0)。 它必須是有效的多維度運算式 (MDX) 邏輯運算式。  
  
 *Expression1 Hint [Eager|Strict|Lazy]]*  
 邏輯運算式評估為時，使用 **，則為 true**。 Expression1 必須是有效的多維度運算式 (MDX) 運算式。  
  
 *Expression2 Hint [Eager|Strict|Lazy]]*  
 邏輯運算式評估為時，使用**false**。 Expression2 必須是有效的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 由邏輯運算式指定的條件評估為**false**當此運算式的值為零。 任何其他值評估為 **，則為 true**。  
  
 條件時**真**，則**IIf**函式會傳回第一個運算式。 否則，此函數會傳回第二個運算式。  
  
 指定的運算式可以傳回值或 MDX 物件。 而且，指定的運算式不需要類型相符。  
  
 **IIf**函式不建議在建立一組根據搜尋準則的成員。 請改用[篩選](../mdx/filter-mdx.md)函式評估的邏輯運算式針對指定集合中每個成員，並傳回成員子集。  
  
> [!NOTE]  
>  如果任何一個運算式評估為 NULL，符合該條件時，結果集將是 NULL。  
  
 提示是選擇性的修飾詞，可決定評估運算式的方式和時機。 它可讓您藉由指定運算式的評估方式來覆寫預設查詢計畫。  
  
-   EAGER 會針對原始 IIF 子空間來評估運算式。  
  
-   STRICT 只評估由邏輯條件運算式所建立之限制子空間內的運算式。  
  
-   LAZY 會依照逐資料格模式來評估運算式。  
  
 EAGER 和 STRICT 只適用於 IIF 的 then-else 分支，LAZY 則適用於所有 MDX 運算式。 所有 MDX 運算式後面都可以跟著 HINT LAZY，後者將會依照逐資料格模式來評估該運算式。  
  
 EAGER 和 STRICT 在提示中互斥，它們可以在不同的運算式中，用於相同的 IIF(,,)。  
  
 如需詳細資訊，請參閱 < [SQL Server Analysis Services 2008 中的 IIF 函數查詢提示](https://go.microsoft.com/fwlink/?LinkId=269540)並[的執行計畫與 MDX IIF 函數和 CASE 陳述式的計畫提示](https://go.microsoft.com/fwlink/?LinkId=269565)。  
  
## <a name="examples"></a>範例  
 下列查詢示範簡單的用法**IIF**內導出量值傳回兩個不同的字串值時的量值 Internet Sales Amount 大於或小於 $10000 其中之一：  
  
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
  
 以下是範例**IIF**傳回資料列上建立一組複雜 tuple 在 Generate 函數內的兩個集合的其中一個：  
  
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
  
  
