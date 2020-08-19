---
description: BottomCount (MDX)
title: BottomCount (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e331a84efe36cef11951afac3f304957e4ffcb00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494974"
---
# <a name="bottomcount-mdx"></a>BottomCount (MDX)


  以遞增的順序排序集合，並傳回指定集合中數值最低的指定 Tuple 數。  
  
## <a name="syntax"></a>語法  
  
```  
  
BottomCount(Set_Expression, Count [,Numeric_Expression])  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Count*  
 有效的數值運算式，會指定要傳回的 Tuple 數目。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果指定了數值運算式，這個函數會根據集合評估後指定的數值運算式值，以遞增順序來排序指定集合中的 Tuple。 然後， **BottomCount** 函式會傳回具有最小值的指定數量的元組。  
  
> [!IMPORTANT]  
>  **BottomCount**函式（例如[TopCount](../mdx/topcount-mdx.md)函數）一律會中斷階層。  
  
 如果未指定數值運算式，則函式會以自然順序傳回成員的集合，不含任何排序，其行為就像 [Tail (MDX) ](../mdx/tail-mdx.md) 函數一樣。  
  
## <a name="example"></a>範例  
 下列範例會傳回每個日曆年度最低五檔 Product SubCategory 銷售的 Reseller Order Quantity 量值，並根據 Reseller Sales Amount 量值排序。  
  
```  
SELECT BottomCount([Product].[Product Categories].[Subcategory].Members  
   , 10  
   , [Measures].[Reseller Sales Amount]) ON 0,  
   [Date].[Calendar].[Calendar Year].Members ON 1  
  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Reseller Order Quantity]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
