---
title: CASE 語句（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 756300f1efc93e47a7af3913b34d9318cbe5e559
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68016829"
---
# <a name="case-statement-mdx"></a>CASE 陳述式 (MDX)


  讓您根據條件傳回多個比較的特定值。 CASE 陳述式有兩種類型：  
  
-   簡單的 CASE 陳述式，會將運算式與一組簡單運算式進行比較以傳回特定值。  
  
-   搜尋的 CASE 陳述式，會評估一組布林運算式以傳回特定值。  
  
## <a name="syntax"></a>語法  
  
```  
  
Simple Case Statement  
CASE [input_expression]  
WHEN when_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
  
Search Case Statement  
CASE   
WHEN Boolean_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
```  
  
## <a name="arguments"></a>引數  
 *input_expression*  
 解析成純量值的多維度運算式 (MDX) 運算式。  
  
 *when_expression*  
 針對評估*input_expression*的指定純量值，評估為 true 時，會傳回*else_result_expression*的純量值。  
  
 *when_true_result_expression*  
 當 WHEN 子句評估為 true 時，所傳回的純量值。  
  
 *else_result_expression*  
 當沒有任何 WHEN 子句評估為 true 時，所傳回的純量值。  
  
 *Boolean_expression*  
 評估為純量值的 MDX 運算式。  
  
## <a name="remarks"></a>備註  
 如果沒有 ELSE 子句，而且所有 WHEN 子句都評估為 false，則結果會是空的資料格。  
  
## <a name="simple-case-expression"></a>簡單的 CASE 運算式  
 MDX 會藉由將*input_expression*解析成純量值，來評估簡單的 case 運算式。 然後，此純量值會與*when_expression*的純量值進行比較。 如果兩個純量值相符，則 CASE 語句會傳回*when_true_expression*的值。 如果兩個純量值不符，則會評估下一個 WHEN 子句。 如果所有 WHEN 子句都評估為 false，則會傳回 ELSE 子句中*else_result_expression*的值（如果有的話）。  
  
 在下列範例中，會針對數個 WHEN 子句來評估 Reseller Order Count 量值，並根據每年 Reseller Order Count 量值來傳回結果。 若轉售商訂單計數值不符合 WHEN 子句的*when_expression*中指定的純量值，則會傳回*else_result_expression*的純量值。  
  
```  
WITH MEMBER [Measures].x AS   
CASE [Measures].[Reseller Order Count]  
   WHEN 0 THEN 'NONE'  
   WHEN 1 THEN 'SMALL'  
   WHEN 2 THEN 'SMALL'  
   WHEN 3 THEN 'MEDIUM'  
   WHEN 4 THEN 'MEDIUM'  
   WHEN 5 THEN 'LARGE'  
   WHEN 6 THEN 'LARGE'  
      ELSE 'VERY LARGE'  
END  
SELECT Calendar.[Calendar Year] on 0  
, NON EMPTY [Geography].[Postal Code].Members ON 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="searched-case-expression"></a>搜尋的 CASE 運算式  
 若要使用 CASE 運算式來執行更複雜的評估，請使用搜尋的 CASE 運算式。 此搜尋運算式的變化讓您能評估輸入運算式是否在值範圍內。 MDX 會以 WHEN 子句出現在 CASE 陳述式中的順序，來評估這些子句。  
  
 在下列範例中，會針對數個 WHEN 子句的指定*Boolean_expression*評估「轉售商訂單計數」量值。 根據每年 Reseller Order Count 量值來傳回結果。 因為 WHEN 子句是依出現順序評估，所以大於 6 的所有值都會被輕易指定 "VERY LARGE" 值，而不需明確指定每個值。 對於在 WHEN 子句中未指定的轉售商訂單計數值，會傳回*else_result_expression*的純量值。  
  
```  
WITH MEMBER [Measures].x AS   
CASE   
   WHEN [Measures].[Reseller Order Count] > 6 THEN 'VERY LARGE'  
   WHEN [Measures].[Reseller Order Count] > 4 THEN 'LARGE'  
   WHEN [Measures].[Reseller Order Count] > 2 THEN 'MEDIUM'  
   WHEN [Measures].[Reseller Order Count] > 0 THEN 'SMALL'  
   ELSE "NONE"  
END  
SELECT Calendar.[Calendar Year] on 0,  
NON EMPTY [Geography].[Postal Code].Members on 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 指令碼陳述式 &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
