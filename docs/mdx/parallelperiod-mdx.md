---
title: ParallelPeriod （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b4122c13a5371cc0ffe1c5c6235ad750e7fdadad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020706"
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
  
 *索引*  
 指定落後的平行週期數目之有效數值運算式。  
  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 雖然與[Cousin](../mdx/cousin-mdx.md)函式類似，但**ParallelPeriod**函數與時間序列更密切相關。 **ParallelPeriod**函數會在指定的層級取得指定成員的上階、尋找具有指定之延遲的上階的兄弟，最後在兄弟的子系中傳回指定成員的平行期間。  
  
 **ParallelPeriod**函數具有下列預設值：  
  
-   如果沒有指定層級運算式或成員運算式，預設成員值就是在量值群組中具有*時間*類型之第一個維度上第一個階層的目前成員。  
  
-   如果指定了層級運算式，但未指定成員運算式，則會*Level_Expression*預設成員值。**CurrentMember**。  
  
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
  
  
