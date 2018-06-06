---
title: Qtd (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 218e90b5e43a1603978ba912fccb85ae16b34072
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580920"
---
# <a name="qtd-mdx"></a>Qtd (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  從指定的成員，第一個同層級開始，並以指定成員結束，如同受條件約束相同的層級傳回成員的同層級集合*季*Time 維度中的層級。  
  
## <a name="syntax"></a>語法  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果成員 expressionis，未指定，預設值是類型層級之第一個階層的目前成員*季*類型的第一個維度*時間*量值群組中。  
  
 **Qtd**函式是的捷徑函數[PeriodsToDate &#40;MDX&#41; ](../mdx/periodstodate-mdx.md)函式的層級運算式引數設定為*季*。 也就是說，`Qtd(Member_Expression)` 與 `PeriodsToDate(Quarter_Level_Expression, Member_Expression)` 的功能相同。  
  
## <a name="example"></a>範例  
 下列範例會傳回的 sum`Measures.[Order Quantity]`成員前, 兩個月的第三季 2003年日曆年度中所包含的彙總`Date`維度中，從**Adventure Works** cube。  
  
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
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
