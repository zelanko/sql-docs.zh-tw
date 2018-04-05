---
title: NonEmpty (MDX) |Microsoft 文件
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
- NonEmpty function
ms.assetid: dfbfa747-3175-405c-aa5b-15c187b06338
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: a17e8cf51ac2c2a8bac98315b85f53421d7c3c4b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="nonempty-mdx"></a>NonEmpty (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 在第二個集合中的 Tuple 評估後，這個函數會傳回第一個指定集合中非空的 Tuple。 **NonEmpty**函式會考慮到計算並且保留重複的 tuple。 如果沒有提供第二個集合，則會在 Cube 中屬性階層和量值之成員的目前座標內容中，評估運算式。  
  
> [!NOTE]  
>  使用此函式而不是已被取代[NonEmptyCrossjoin &#40;MDX &#41;](../mdx/nonemptycrossjoin-mdx.md)函式。  
  
> [!IMPORTANT]  
>  非空的是 Tuple 所參考之資料格參考的特性，而不是 Tuple 本身的特性。  
  
## <a name="examples"></a>範例  
 下列查詢示範簡單的範例**NonEmpty**，傳回所有客戶的非 null 值的 Internet Sales Amount 年 7 月 1 日 2001:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `, {([Date].[Calendar].[Date].&[20010701], [Measures].[Internet Sales Amount])}`  
  
 `)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 下列範例會傳回包含客戶和購買日期，使用的 tuple 集合**篩選**函式和**NonEmpty**尋找的最後一個日期，每一位客戶購買的函式：  
  
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
  
## <a name="see-also"></a>請參閱  
 [DefaultMember &#40;MDX &#41;](../mdx/defaultmember-mdx.md)   
 [篩選 &#40;MDX &#41;](../mdx/filter-mdx.md)   
 [IsEmpty &#40;MDX &#41;](../mdx/isempty-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX &#41;](../mdx/nonemptycrossjoin-mdx.md)  
  
  
