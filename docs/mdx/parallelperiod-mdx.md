---
description: ParallelPeriod (MDX)
title: ParallelPeriod (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4c8a6c91bae50ca06be46926f34de172e424e613
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471720"
---
# <a name="parallelperiod-mdx"></a>ParallelPeriod (MDX)


  傳回先前跟特定成員在同樣相對位置上的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
ParallelPeriod( [ Level_Expression [ ,Index [ , Member_Expression ] ] ] )  
```  
  
## <a name="arguments"></a>引數  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
 *Index*  
 指定落後的平行週期數目之有效數值運算式。  
  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 雖然類似于 [Cousin](../mdx/cousin-mdx.md) 函式， **ParallelPeriod** 函式與時間序列更密切相關。 **ParallelPeriod**函式會在指定的層級採用指定成員的上階，找出具有指定延隔的上階的同級，最後在同級的子系之間傳回指定成員的平行週期。  
  
 **ParallelPeriod**函數具有下列預設值：  
  
-   如果沒有指定層級運算式或成員運算式，預設成員值就是量值群組中具有 *時間* 類型之第一個維度上第一個階層的目前成員。  
  
-   如果指定了層級運算式，但未指定成員運算式，則預設成員值為 *Level_Expression*。**CurrentMember**。  
  
-   預設索引值為 1。  
  
-   預設層級是指定成員之父系的層級。  
  
 **ParallelPeriod**函數相當於下列 MDX 語句：  
  
 `Cousin(Member_Expression, Ancestor(Member_Expression, Level_Expression) .Lag(Numeric_Expression))`  
  
## <a name="example"></a>範例  
 下列範例會根據季層級傳回比 2003 年 10 月落後三個週期的平行週期，亦即傳回 2003 年 1 月。  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Quarter]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 下列範例會根據半年度層級傳回比 2003 年 10 月落後三個週期的平行週期，亦即傳回 2002 年 4 月。  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Semester]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
