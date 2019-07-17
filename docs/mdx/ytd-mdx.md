---
title: 年初迄今 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e3fcd823dea5d651cd7be9295fa4c6bba25380c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125755"
---
# <a name="ytd-mdx"></a>Ytd (MDX)


  從指定的成員，開始第一個同層級，並以指定成員結束，如同受條件約束相同的層級傳回成員的同層級集合*年份*Time 維度中的層級。  
  
## <a name="syntax"></a>語法  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果未指定成員運算式，預設值是第一個階層的目前成員的型別層級*年份*類型的第一個維度*時間*量值群組中。  
  
 **Ytd**功能的捷徑函數[PeriodsToDate](../mdx/periodstodate-mdx.md)函式所在的層級依據屬性階層的 Type 屬性設為*年*。 也就是說，`Ytd(Member_Expression)` 相當於 `PeriodsToDate(Year_Level_Expression,Member_Expression)`。 請注意，此函式將無法運作時的類型屬性設定為*FiscalYears*。  
  
## <a name="example"></a>範例  
 下列範例會傳回的總和`Measures.[Order Quantity]`成員前, 八個月 2003年日曆年度中包含在彙總`Date`維度中，從**Adventure Works** cube。  
  
```  
WITH MEMBER [Date].[Calendar].[First8MonthsCY2003] AS  
    Aggregate(  
        YTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First8MonthsCY2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 **年初迄今**經常在組合中未指定參數，表示[CurrentMember &#40;MDX&#41; ](../mdx/currentmember-mdx.md)函式會顯示累計的年度迄今總計在報表中，如中所示下列查詢：  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
