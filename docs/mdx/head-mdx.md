---
description: Head (MDX)
title: Head (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 51a832bf38d3834c44f9b31f5bbfd27833d6d691
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429920"
---
# <a name="head-mdx"></a>Head (MDX)


  傳回集合中指定數目的前幾個元素，同時保留重複項。  
  
## <a name="syntax"></a>語法  
  
```  
  
Head(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Count*  
 有效的數值運算式，會指定要傳回的 Tuple 數目。  
  
## <a name="remarks"></a>備註  
 **Head**函數會從指定集合的開頭傳回指定的元組數目。 保留元素的順序。 Count 的預設值是 1。 如果指定的元組數目小於1，則 **Head** 函數會傳回空集合。 如果指定的 Tuple 數目超過集合中的 Tuple 數目，則函數會傳回原始的集合。  
  
## <a name="example"></a>範例  
 下列範例不考慮階層，而根據 Reseller Gross Profit 傳回前五名產品銷售子類別目錄。 在使用**Order**函數排序結果之後，會使用**Head**函數來傳回結果中的前5個集合。  
  
```  
SELECT   
[Measures].[Reseller Gross Profit] ON 0,  
Head  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,5  
   ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [Tail &#40;MDX&#41;](../mdx/tail-mdx.md)   
 [專案 &#40;元組&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [專案 &#40;成員&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [順位 &#40;MDX&#41;](../mdx/rank-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
