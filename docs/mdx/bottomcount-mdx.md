---
title: BottomCount (MDX) |Microsoft 文件
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 424c928f64b784070520f4cebe450dd5465fea41
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739777"
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
  
 *計數*  
 有效的數值運算式，會指定要傳回的 Tuple 數目。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果指定了數值運算式，這個函數會根據集合評估後指定的數值運算式值，以遞增順序來排序指定集合中的 Tuple。 **BottomCount**函式會傳回指定的最低值的 tuple 數目。  
  
> [!IMPORTANT]  
>  **BottomCount**函式，例如[TopCount](../mdx/topcount-mdx.md)函式，必會破壞階層架構。  
  
 如果未指定數值運算式，函數會傳回成員的集合以自然的順序，不進行任何排序，其運作方式[Tail (MDX)](../mdx/tail-mdx.md)函式。  
  
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
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
