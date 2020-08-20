---
description: Ytd (MDX)
title: Ytd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 14f286a304e03624a9ce20c1bd7b045dffc38688
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491366"
---
# <a name="ytd-mdx"></a>Ytd (MDX)


  傳回一組與指定成員相同層級的一組同級成員，從第一個同級開始，並以指定的成員結束，如同時間維度中的 *Year* 層級所限制。  
  
## <a name="syntax"></a>語法  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果沒有指定成員運算式，預設值就是量值*群組中，* 第一個維度類型的第一個維度*中，* 第一個階層的目前成員。  
  
 **Ytd**函數是[PeriodsToDate](../mdx/periodstodate-mdx.md)函數的快捷方式函式，其中層級所依據之屬性階層的型別屬性會設定為*年份*。 也就是說，`Ytd(Member_Expression)` 相當於 `PeriodsToDate(Year_Level_Expression,Member_Expression)`。 請注意，當 Type 屬性設定為 *FiscalYears*時，這個函數將無法運作。  
  
## <a name="example"></a>範例  
 下列範例會傳回成員的總和 `Measures.[Order Quantity]` ，此成員是在維度所包含之日曆年度2003的前八個月 `Date` ，從 [ **艾德作品** ] cube 匯總而來。  
  
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
  
 **Ytd** 通常會搭配未指定參數的組合使用，這表示 [CurrentMember &#40;MDX&#41;](../mdx/currentmember-mdx.md) 函數將會在報表中顯示執行中的累積年初至今總計，如下列查詢所示：  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
