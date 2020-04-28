---
title: Qtd （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a8856b28d8eec76d2bc262c4209b007c0a7fa04
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020644"
---
# <a name="qtd-mdx"></a>Qtd (MDX)


  傳回與指定成員相同層級的一組兄弟成員，從第一個兄弟開始，並以指定的成員結束，如同時間維度中的*季*層級所限制。  
  
## <a name="syntax"></a>語法  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果未指定成員 expressionis，預設值為第一個階層的目前成員，其在量值群組中類型*時間*的第一個維度中的類型為*季*。  
  
 **Qtd**函數是[PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md)函數的快捷方式函式，其層級運算式引數設定為*季*。 也就是說，`Qtd(Member_Expression)` 與 `PeriodsToDate(Quarter_Level_Expression, Member_Expression)` 的功能相同。  
  
## <a name="example"></a>範例  
 下列範例會從「**艾德公司**」 `Measures.[Order Quantity]` cube 中傳回成員的總和，這是在`Date`維度所包含之日曆2003年度第三季的前兩個月匯總。  
  
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
  
  
