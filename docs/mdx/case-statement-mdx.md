---
title: CASE 陳述式 (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- statements [MDX], CASE
ms.assetid: 0aee3b4a-d5f7-4c9a-87b8-e5efc2da6b6d
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: a4dbcc7ab42a0e044be0c7561adff4049fd8d1b9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="case-statement-mdx"></a>CASE 陳述式 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 指定的純量值依據*input_expression*評估時，當評估為 true，傳回純量值*else_result_expression*。  
  
 *when_true_result_expression*  
 當 WHEN 子句評估為 true 時，所傳回的純量值。  
  
 *else_result_expression*  
 當沒有任何 WHEN 子句評估為 true 時，所傳回的純量值。  
  
 *Boolean_expression*  
 評估為純量值的 MDX 運算式。  
  
## <a name="remarks"></a>備註  
 如果沒有 ELSE 子句，而且所有 WHEN 子句都評估為 false，則結果會是空的資料格。  
  
## <a name="simple-case-expression"></a>簡單的 CASE 運算式  
 MDX 會評估簡單 case 運算式解析*input_expression*純量值。 這個純量值進行比較的純量值*when_expression*。 如果兩個純量值相符，CASE 陳述式傳回的值*when_true_expression*。 如果兩個純量值不符，則會評估下一個 WHEN 子句。 如果所有 WHEN 子句都評估為 false 的值*else_result_expression* ELSE 子句中，如果有的話，會傳回。  
  
 在下列範例中，會針對數個 WHEN 子句來評估 Reseller Order Count 量值，並根據每年 Reseller Order Count 量值來傳回結果。 Reseller Order Count 值不符合指定的純量值*when_expression* WHEN 子句，純量值中*else_result_expression*傳回。  
  
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
  
 在下列範例中，評估 Reseller Order Count 量值針對指定*Boolean_expression*每數個 WHEN 子句。 根據每年 Reseller Order Count 量值來傳回結果。 因為 WHEN 子句是依出現順序評估，所以大於 6 的所有值都會被輕易指定 "VERY LARGE" 值，而不需明確指定每個值。 未指定 WHEN 子句，純量值中的 Reseller Order Count 值*else_result_expression*傳回。  
  
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
  
## <a name="see-also"></a>請參閱  
 [MDX 指令碼陳述式 &#40;MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
