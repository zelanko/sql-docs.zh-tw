---
description: NonEmpty (MDX)
title: 非空白的 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b887988327908f128633349de52f39a17d1e0978
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483721"
---
# <a name="nonempty-mdx"></a>NonEmpty (MDX)


  根據指定集合與第二個集合的交叉乘積，從指定集合傳回非空的 Tuple 集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
NONEMPTY(set_expression1 [,set_expression2])  
```  
  
## <a name="arguments"></a>引數  
 *set_expression1*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *set_expression2*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 在第二個集合中的 Tuple 評估後，這個函數會傳回第一個指定集合中非空的 Tuple。 非 **空白函數會** 將計算納入考慮，並保留重複的元組。 如果沒有提供第二個集合，則會在 Cube 中屬性階層和量值之成員的目前座標內容中，評估運算式。  
  
> [!NOTE]  
>  請使用此函式，而不是已被取代的 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md) 函數。  
  
> [!IMPORTANT]  
>  非空的是 Tuple 所參考之資料格參考的特性，而不是 Tuple 本身的特性。  
  
## <a name="examples"></a>範例  
 下列查詢顯示非空白的簡單範例 **，會**傳回在2001年7月1日的網際網路銷售金額為非 null 值的所有客戶：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `, {([Date].[Calendar].[Date].&[20010701], [Measures].[Internet Sales Amount])}`  
  
 `)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 下列範例會傳回包含客戶和購買日期的元組集合，使用**篩選**函數和非空白**NonEmpty**的函式來尋找每個客戶購買的最後一個日期：  
  
 `WITH SET MYROWS AS FILTER`  
  
 `(NONEMPTY`  
  
 `([Customer].[Customer Geography].[Customer].MEMBERS`  
  
 `* [Date].[Date].[Date].MEMBERS`  
  
 `, [Measures].[Internet Sales Amount]`  
  
 `) AS MYSET`  
  
 `, NOT(MYSET.CURRENT.ITEM(0)`  
  
 `IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))`  
  
 `)`  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `MYROWS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [DefaultMember &#40;MDX&#41;](../mdx/defaultmember-mdx.md)   
 [篩選 &#40;MDX&#41;](../mdx/filter-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)   
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)  
  
  
