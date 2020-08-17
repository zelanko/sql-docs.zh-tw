---
description: Extract (MDX)
title: 解壓縮 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0b168794a38a515d4ace97d576710041eac86195
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387514"
---
# <a name="extract-mdx"></a>Extract (MDX)


  從擷取的階層元素傳回 Tuple 集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Extract(Set_Expression, Hierarchy_Expression1 [,Hierarchy_Expression2, ...n] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Hierarchy_Expression1*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
 *Hierarchy_Expression2*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **解壓縮**函式會傳回集合，其中包含來自已解壓縮之階層元素的元組。 對於指定集合中的每個 Tuple，指定的階層成員會擷取至結果集中的新 Tuple。 此函數永遠會移除重複的 Tuple。  
  
 **解壓縮**函式會執行[交叉](../mdx/crossjoin-mdx.md)聯結函數的相反動作。  
  
## <a name="examples"></a>範例  
 下列查詢示範如何在非**空白函數所傳回的一**組元組上使用**解壓縮**函式：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `//Returns the distinct combinations of Customer and Date for all purchases`  
  
 `//of Bike Racks or Bike Stands`  
  
 `EXTRACT(`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `*`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `*`  
  
 `{[Product].[Product Categories].[Subcategory].&[26],[Product].[Product Categories].[Subcategory].&[27]}`  
  
 `*`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `)`  
  
 `,  [Customer].[Customer], [Date].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
