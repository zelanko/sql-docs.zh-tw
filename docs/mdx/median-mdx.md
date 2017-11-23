---
title: "中間值 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: MEDIAN
dev_langs: kbMDX
helpviewer_keywords: Median function
ms.assetid: 7a326a3f-0123-45c4-9b18-31f83b90d986
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 44e92801c99d7ca2990d656fda13b395a9b0229b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="median-mdx"></a>Median (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>請參閱＜  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
