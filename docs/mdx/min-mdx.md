---
title: 最小值 (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2af77108922baa3767f9f8d478ec38509f1dac06
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581520"
---
# <a name="min-mdx"></a>Min (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在集合評估後傳回數值運算式的最小值。  
  
## <a name="syntax"></a>語法  
  
```  
  
Min( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果指定數值運算式，會在集合上評估指定的數值運算式，然後傳回該評估的最小值。 如果沒有指定數值運算式，則會在集合成員的目前內容中評估指定的集合，然後傳回該評估的最小值。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在計算數字集合中的最小值時會忽略 Null。  
  
## <a name="example"></a>範例  
 下列範例會傳回 Adventure Works Cube 中每個子類別目錄和每個國家 (地區) 的每季銷售最小值。  
  
```  
WITH MEMBER Measures.x AS Min   
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
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
