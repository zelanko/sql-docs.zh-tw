---
title: ClosingPeriod (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c6c9dea03a4b09ae4dcbe66e6712a542b1920ce0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63181579"
---
# <a name="closingperiod-mdx"></a>ClosingPeriod (MDX)


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
  
-   如果指定層級運算式，則**ClosingPeriod**函式會使用包含指定的層級，並傳回指定層級的預設成員之下階當中的最後一個同層級的維度。  
  
-   如果指定層級運算式和成員運算式，則**ClosingPeriod**函式會傳回指定層級的指定成員之下階當中的最後一個同層級。  
  
-   如果指定層級運算式或成員運算式都不是， **ClosingPeriod**函式會使用預設層級和維度的成員 （如果有的話） 在 cube 中 Time 類型。  
  
 **ClosingPeriod**函式相當於以下的 MDX 陳述式：  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)`.  
  
> [!NOTE]  
>  [OpeningPeriod](../mdx/openingperiod-mdx.md)函數很相似**ClosingPeriod**函式，不同之處在於**OpeningPeriod**函式會傳回第一個同層級，而不是最後一個同層級。  
  
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
 [OpeningPeriod &#40;MDX&#41;](../mdx/openingperiod-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [LastSibling &#40;MDX&#41;](../mdx/lastsibling-mdx.md)  
  
  
