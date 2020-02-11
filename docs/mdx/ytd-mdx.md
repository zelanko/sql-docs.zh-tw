---
title: 年初迄今（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e3fcd823dea5d651cd7be9295fa4c6bba25380c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125755"
---
# <a name="ytd-mdx"></a>Ytd (MDX)


  傳回與指定成員相同層級的一組兄弟成員，從第一個兄弟開始，並以指定的成員結束，如同時間維度中的*Year*層級所限制。  
  
## <a name="syntax"></a>語法  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果未指定成員運算式，預設值為第一個階層的目前成員，其在量值群組中類型為*Time*的第一個*維度中，* 層級為 year 類型。  
  
 **Ytd**函數是[PeriodsToDate](../mdx/periodstodate-mdx.md)函數的快捷方式函式，其中層級所依據之屬性階層的 Type 屬性會設定為*年*。 也就是說，`Ytd(Member_Expression)` 相當於 `PeriodsToDate(Year_Level_Expression,Member_Expression)`。 請注意，當 Type 屬性設定為*FiscalYears*時，此函數將無法運作。  
  
## <a name="example"></a>範例  
 下列範例會從「**艾德公司**」 `Measures.[Order Quantity]` cube 中傳回成員的總和（在`Date`維度中包含的前八2003個月內）。  
  
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
  
 年初**迄今**常用於不指定任何參數的情況下，這表示[CurrentMember &#40;MDX&#41;](../mdx/currentmember-mdx.md)函數會在報表中顯示執行中累計年初至今的總計，如下列查詢所示：  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
