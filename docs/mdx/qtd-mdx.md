---
title: "Qtd (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: QTD
dev_langs: kbMDX
helpviewer_keywords: Qtd function
ms.assetid: c1fe47e0-9c2b-466f-8d6d-e2b1c16a69cb
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: cabe908f3d78082d6af113a60f105ba4f4e4f5c0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="qtd-mdx"></a>Qtd (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
 **Qtd**函式是的捷徑函數[PeriodsToDate &#40;MDX &#41;](../mdx/periodstodate-mdx.md)函式的層級運算式引數設定為*季*。 也就是說，`Qtd(Member_Expression)` 與 `PeriodsToDate(Quarter_Level_Expression, Member_Expression)` 的功能相同。  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
