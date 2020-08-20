---
description: 除 MDX 運算子參考
title: " (將) 分割 (MDX) |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a0d6947e1e0b4dc45d56980b734c2de98d8ad24c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484021"
---
# <a name="divide---mdx-operator-reference"></a>除 MDX 運算子參考


  執行算術運算，將一個數字除以另一個數字。  
  
## <a name="syntax"></a>語法  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>參數  
 *股利*  
 傳回數值的有效多維度運算式 (MDX) 運算式。  
  
 *因數*  
 傳回數值的有效 MDX 運算式。  
  
## <a name="return-value"></a>傳回值  
 具有較高優先順序之參數的資料類型的值。  
  
## <a name="remarks"></a>備註  
 **/ (除以) **運算子所傳回的實際值，代表第一個運算式除以第二個運算式的商。  
  
 兩個運算式的資料類型必須相同，或者其中一個運算式必須可以用隱含方式轉換為另一個運算式的資料類型。 如果 *除數* 評估為 null 值，則運算子會引發錯誤。 如果 *除數* 和被 *除數* 都評估為 null 值，則運算子會傳回 null 值。  
  
## <a name="examples"></a>範例  
 以下範例示範此運算子的用法。  
  
```  
-- This query returns the freight cost per user,  
-- for products, averaged by month.   
With Member [Measures].[Freight Per Customer] as  
    [Measures].[Internet Freight Cost]  
    /   
    [Measures].[Customer Count]  
  
SELECT   
    [Ship Date].[Calendar].[Calendar Year] Members ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
 將非零或非 null 值除以零或 null 時將會傳回 Infinity 值，它會以 "1.#INF" 形式顯示在查詢結果中。 在大多數情況下，您應該檢查除數是否為零，以避免這個狀況。 下列範例為您示範作法：  
  
 `//Returns 1.#INF when Internet Sales Amount is zero or null`  
  
 `Member [Measures].[Reseller to Internet Ratio] AS`  
  
 `[Measures].[Reseller Sales Amount]`  
  
 `/`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `//Traps the division by zero scenario and returns null instead of 1.#INF`  
  
 `Member [Measures].[Reseller to Internet Ratio With Error Handling] AS`  
  
 `IIF([Measures].[Internet Sales Amount]=0, NULL,`  
  
 `[Measures].[Reseller Sales Amount]`  
  
 `/`  
  
 `[Measures].[Internet Sales Amount])`  
  
 `SELECT`  
  
 `{[Measures].[Reseller to Internet Ratio],[Measures].[Reseller to Internet Ratio With Error Handling]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 `WHERE([Date].[Calendar].[Calendar Year].&[2001])`  
  
## <a name="see-also"></a>另請參閱  
 [IIf &#40;MDX&#41;](../mdx/iif-mdx.md)   
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
