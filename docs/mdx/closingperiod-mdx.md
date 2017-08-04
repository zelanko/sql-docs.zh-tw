---
title: "ClosingPeriod (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CLOSINGPERIOD
dev_langs:
- kbMDX
helpviewer_keywords:
- ClosingPeriod function
ms.assetid: ae709017-219d-43e1-a98a-a85bd365b4cd
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 921c058bf83cb8e3b54b310dcc9e65bc8202d569
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="closingperiod-mdx"></a>ClosingPeriod (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回成員，該成員是指定層級上已指定之成員的下階中最後一個同層級。  
  
## <a name="syntax"></a>語法  
  
```  
  
ClosingPeriod( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>引數  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 這個函數主要是使用於 Time 類型的維度，但也可以使用於任何維度。  
  
-   如果指定層級運算式，則**ClosingPeriod**函式會使用維度，其中包含指定層級，並傳回指定層級的預設成員之下階的最後一個同層級。  
  
-   如果未指定層級運算式和成員運算式， **ClosingPeriod**函式會傳回指定層級的指定成員之下階的最後一個同層級成員。  
  
-   如果指定層級運算式或成員運算式， **ClosingPeriod**函式使用預設層級和成員的維度 （如果有的話） 中 Time 類型的 cube。  
  
 **ClosingPeriod**函數即相當於以下 MDX 陳述式：  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)`。  
  
> [!NOTE]  
>  [OpeningPeriod](../mdx/openingperiod-mdx.md)函數很相似**ClosingPeriod**函式中，不同處在於**OpeningPeriod**函式會傳回第一個同層級，而不是最後一個同層級。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 Date 維度 (具有 Time 語意類型) 之 FY2007 成員的預設量值。 之所以會傳回這個成員是因為 Fiscal Year 層級是 [All] 層級的第一個下階；因為 Fiscal 階層是階層集合中的第一個使用者自訂階層，所以 Fiscal 階層是預設階層；因為 FY 2007 成員是該層級該階層中的最後一個同層級。  
  
```  
SELECT ClosingPeriod() ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會傳回 Date.Date 屬性階層之 Date.Date.Date 層級 November 30, 2006 成員的預設量值。 這個成員是 Date.Date 屬性階層 [All] 層級之下階的最後一個同層級。  
  
```  
SELECT ClosingPeriod ([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會傳回 December, 2003 成員的預設量值，該成員是 Calendar 使用者自訂階層年層級 2003 成員之下階的最後一個同層級。  
  
```  
SELECT ClosingPeriod ([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會傳回 June, 2003 成員的預設量值，該成員是 Fiscal 使用者自訂階層年層級 2003 成員之下階的最後一個同層級。  
  
```  
SELECT ClosingPeriod ([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [OpeningPeriod &#40;MDX &#41;](../mdx/openingperiod-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [LastSibling &#40;MDX &#41;](../mdx/lastsibling-mdx.md)  
  
  

