---
title: ParallelPeriod (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8cde031af19fff309520cd72e145b6c04dc19d9c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580820"
---
# <a name="parallelperiod-mdx"></a>ParallelPeriod (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 雖然類似[Cousin](../mdx/cousin-mdx.md)函式， **ParallelPeriod**函式更密切的時間序列。 **ParallelPeriod**函式會在指定的層級的指定成員的上階，尋找上階的同層級，與指定的延遲，和最後會傳回指定成員的同層級之下階當中的平行週期。  
  
 **ParallelPeriod**函式具有下列的預設值：  
  
-   如果指定層級運算式或成員運算式，預設成員值是一種之第一個維度的第一個階層的目前成員*時間*量值群組中。  
  
-   如果指定層級運算式，但沒有指定成員運算式，預設成員值是*Level_Expression*。**Hierarchy.CurrentMember**。  
  
-   預設索引值為 1。  
  
-   預設層級是指定成員之父系的層級。  
  
 **ParallelPeriod**函數即相當於以下 MDX 陳述式：  
  
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
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
