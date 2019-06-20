---
title: PeriodsToDate (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e33ac5562e7304b71779134b02488733b9d576a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63277489"
---
# <a name="periodstodate-mdx"></a>PeriodsToDate (MDX)


  傳回與指定成員層級相同的同層級成員集合，以第一個同層級成員開始，以指定的成員結束，如同受 Time 維度中的指定層級條件約束。  
  
## <a name="syntax"></a>語法  
  
```  
  
PeriodsToDate( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>引數  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 指定的層級的範圍內**PeriodsToDate**函式會傳回一組期間，為指定的成員，第一個週期開始和結束與指定成員位於同一層級。  
  
-   如果指定層級，階層的目前成員推斷*階層*。**CurrentMember**，其中*階層*是指定層級的階層。  
  
-   如果沒有指定層級或成員，此層級為量值群組中 Time 類型之第一個維度上、第一個階層的目前成員的父層級。  
  
 `PeriodsToDate( Level_Expression, Member_Expression )` 的功能與以下 MDX 運算式相同：  
  
 `TopCount(Descendants(Ancestor(Member_Expression, Level_Expression), Member_Expression.Level), 1):Member_Expression`  
  
## <a name="examples"></a>範例  
 下列範例會傳回的總和`Measures.[Order Quantity]`成員前, 八個月 2003年日曆年度中包含在彙總`Date`維度中，從**Adventure Works** cube。  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 下列範例會彙總 2003 日曆年度下半年度的前 2 個月。  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Semester],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
## <a name="see-also"></a>另請參閱  
 [TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
