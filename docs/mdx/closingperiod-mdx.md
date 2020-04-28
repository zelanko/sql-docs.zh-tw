---
title: ClosingPeriod （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 102485ede0e52389d43bdb64742a2564aaa71419
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68016787"
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
  
-   如果指定了層級運算式， **ClosingPeriod**函數會使用包含指定之層級的維度，並傳回位於指定層級之預設成員子系中的最後一個兄弟。  
  
-   如果同時指定了層級運算式和成員運算式，則**ClosingPeriod**函數會傳回指定層級上指定成員子系中的最後一個兄弟。  
  
-   如果沒有指定層級運算式或成員運算式，則**ClosingPeriod**函數會在 cube 中使用具有時間類型之維度的預設層級和成員（如果有的話）。  
  
 **ClosingPeriod**函數相當於下列 MDX 語句：  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)`.  
  
> [!NOTE]  
>  [OpeningPeriod](../mdx/openingperiod-mdx.md)函數與**ClosingPeriod**函數相似，不同之處在于**OpeningPeriod**函數會傳回第一個兄弟，而不是最後一個兄弟。  
  
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
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [LastSibling &#40;MDX&#41;](../mdx/lastsibling-mdx.md)  
  
  
