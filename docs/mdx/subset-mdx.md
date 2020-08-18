---
description: Subset (MDX)
title: 子集 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d0b7e79ebf0415011665ae63e7b9699200e374b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386724"
---
# <a name="subset-mdx"></a>Subset (MDX)


  從指定集合中傳回 Tuple 的子集。  
  
## <a name="syntax"></a>語法  
  
```  
  
Subset(Set_Expression, Start [ ,Count ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *啟動*  
 有效的數值運算式，會指定要傳回之第一個 Tuple 的位置。  
  
 *Count*  
 有效的數值運算式，會指定要傳回的 Tuple 數目。  
  
## <a name="remarks"></a>備註  
 從指定的集合中， **子集** 函數會從指定的開始位置開始，傳回包含指定之元組數目的子集。 開始位置是根據以零為基底的索引，也就是說，零 (0) 對應至指定集合中的第一個 Tuple，1 對應至第二個，依此類推。  
  
 如果未指定 *Count* ，函數會從 *開始* 到集合的結尾傳回所有的元組。  
  
## <a name="example"></a>範例  
 下列範例不考慮階層，而根據 Reseller Gross Profit 傳回前五名產品銷售子類別的 Reseller Sales 量值。 在使用**Order**函數排序結果之後，會使用**子集**函數來傳回結果中的前五個集合。  
  
```  
SELECT Subset  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,0  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
