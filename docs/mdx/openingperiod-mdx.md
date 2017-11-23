---
title: "OpeningPeriod (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: OPENINGPERIOD
dev_langs: kbMDX
helpviewer_keywords: OpeningPeriod function
ms.assetid: bebf55cf-e5c6-42b1-98f2-1d6e54093d4c
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 338ca8f96edd6204e07786c1b4d10195ce180326
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="openingperiod-mdx"></a>OpeningPeriod (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回屬於指定層級之下階的第一個同層級成員，可選擇性地指定成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
OpeningPeriod( [ Level_Expression [ , Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>引數  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 這個函數主要是使用於 Time 維度，但也可以使用於任何維度。  
  
-   如果指定層級運算式，則**OpeningPeriod**函式會使用階層，其中包含指定層級，並傳回指定層級的預設成員之下階的第一個同層級。  
  
-   如果未指定層級運算式和成員運算式， **OpeningPeriod**函式會傳回指定層級中含有指定的層級之階層的指定成員之下階的第一個同層級成員。  
  
-   如果指定層級運算式或成員運算式， **OpeningPeriod**函式使用 Time 類型的預設層級和成員的維度。  
  
> [!NOTE]  
>  [ClosingPeriod](../mdx/closingperiod-mdx.md)函數很相似**OpeningPeriod**函式中，不同處在於**ClosingPeriod**函式會傳回最後一個同層級，而不是第一個同層級。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 Date 維度 (具有 Time 類型) 之 FY2002 成員的預設量值。 因為 Fiscal Year 層級是 [All] 層級的第一個下階，所以會傳回這個成員，因為 Fiscal 階層是階層集合中的第一個使用者自訂階層，所以 Fiscal 階層是預設階層，而且 FY 2002 成員是該層級上這個階層中的第一個同層級。  
  
```  
SELECT OpeningPeriod() ON 0  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回 Date.Date 屬性階層之 Date.Date.Date 層級 July 1, 2001 成員的預設量值。 這個成員是 Date.Date 屬性階層 [All] 層級之下階的第一個同層級。  
  
```  
SELECT OpeningPeriod([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回 January, 2003 成員的預設量值，該成員是 Calendar 使用者自訂階層中年層級 2003 成員之下階的第一個同層級。  
  
```  
SELECT OpeningPeriod([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回 July, 2002 成員的預設量值，該成員是 Fiscal 使用者自訂階層中，年層級 2003 成員之下階的第一個同層級。  
  
```  
SELECT OpeningPeriod([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>請參閱＜  
 [TopCount &#40;MDX &#41;](../mdx/topcount-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [FirstSibling &#40;MDX &#41;](../mdx/firstsibling-mdx.md)  
  
  
