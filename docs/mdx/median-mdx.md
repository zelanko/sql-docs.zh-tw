---
title: 中間值 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e962507d6e437974708aa042919ea6fb7bd632d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048522"
---
# <a name="median-mdx"></a>Median (MDX)


  在集合評估後傳回數值運算式的中間值。  
  
## <a name="syntax"></a>語法  
  
```  
  
Median(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果指定數值運算式，會在集合上評估指定的數值運算式，然後傳回該評估的中間值。 如果沒有指定數值運算式，則會在集合成員的目前內容中評估指定的集合，然後傳回評估的中間值。  
  
 中間值是排序的數字集合中的中間值。 (中間值和平均值不同，平均值是將數字集合的總和除以集合中的數字計數)。 藉由在集合中選擇至少有一半的值小於選擇的最小值，來決定中間值。 如果集合內值的數目是奇數，則中間值對應至單一的值。 如果集合內值的數目是偶數，則中間值對應至兩個中間值的總和除以 2。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在計算排序數字集合中的中間值時會忽略 Null。  
  
## <a name="example"></a>範例  
 下列範例會傳回 Adventure Works Cube 中每季每個子類別目錄和每個國家 (地區) 的月銷售中間值。  
  
```  
WITH MEMBER Measures.x AS Median   
   ([Date].[Calendar].CurrentMember.Children  
      , [Measures].[Reseller Order Quantity]  
   )  
SELECT Measures.x ON 0  
,NON EMPTY [Date].[Calendar].[Calendar Quarter]*   
   [Product].[Product Categories].[Subcategory].members *  
   [Geography].[Geography].[Country].Members  
ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
