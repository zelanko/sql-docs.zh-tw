---
title: "BottomCount (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: BOTTOMCOUNT
dev_langs: kbMDX
helpviewer_keywords: BottomCount function
ms.assetid: 1441dab3-7885-4e92-9d48-21d832286677
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: bf3eb5bebe5c282dd32298665b3f5888ae1dc227
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="bottomcount-mdx"></a>BottomCount (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>請參閱＜  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
