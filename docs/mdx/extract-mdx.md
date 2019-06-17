---
title: 擷取 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a3c58799cc3e95efd7d49b3aff0bf31a1fce22b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63155218"
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
 **擷取**函式會傳回一組，從擷取之階層元素的 tuple 所組成。 對於指定集合中的每個 Tuple，指定的階層成員會擷取至結果集中的新 Tuple。 此函數永遠會移除重複的 Tuple。  
  
 **擷取**函式會執行相反動作[Crossjoin](../mdx/crossjoin-mdx.md)函式。  
  
## <a name="examples"></a>範例  
 下列查詢會示範如何使用**擷取**函式所傳回的 tuple 集合上**NonEmpty**函式：  
  
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
  
  
