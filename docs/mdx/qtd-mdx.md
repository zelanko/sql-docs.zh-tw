---
title: Qtd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 182a86a05cd0dae6adf85d2168fe884ace910a82
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278414"
---
# <a name="qtd-mdx"></a>Qtd (MDX)


  從指定的成員，開始第一個同層級，並以指定成員結束，如同受條件約束相同的層級傳回成員的同層級集合*季*Time 維度中的層級。  
  
## <a name="syntax"></a>語法  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果成員 expressionis，未指定，預設值是具有類型層級的第一個階層的目前成員*季*類型的第一個維度*時間*量值群組中。  
  
 **Qtd**功能的捷徑函數[PeriodsToDate &#40;MDX&#41; ](../mdx/periodstodate-mdx.md)函式的層級運算式引數設為*季*。 也就是說，`Qtd(Member_Expression)` 與 `PeriodsToDate(Quarter_Level_Expression, Member_Expression)` 的功能相同。  
  
## <a name="example"></a>範例  
 下列範例會傳回的總和`Measures.[Order Quantity]`成員，在前兩個月 2003年日曆年度第三季中包含彙總`Date`維度中，從**Adventure Works** cube。  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        QTD([Date].[Calendar].[Month].[August 2003])  
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
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
