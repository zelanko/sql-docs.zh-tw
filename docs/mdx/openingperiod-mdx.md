---
description: OpeningPeriod (MDX)
title: OpeningPeriod (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1ba59621ba52043dac56a9cfcae5ae1cb8b675f1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471760"
---
# <a name="openingperiod-mdx"></a>OpeningPeriod (MDX)


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
  
-   如果指定了層級運算式， **OpeningPeriod** 函數會使用包含指定層級的階層，並傳回指定層級之預設成員下階之間的第一個同級。  
  
-   如果同時指定了層級運算式和成員運算式， **OpeningPeriod** 函數就會傳回包含指定層級之階層內指定層級之指定成員的子系中的第一個同級。  
  
-   如果沒有指定層級運算式或成員運算式， **OpeningPeriod** 函式會使用維度的預設層級和成員，且具有時間類型。  
  
> [!NOTE]  
>  [ClosingPeriod](../mdx/closingperiod-mdx.md)函式與**OpeningPeriod**函數類似，不同之處在于**ClosingPeriod**函數會傳回最後一個同級，而不是第一個同級。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md)   
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [FirstSibling &#40;MDX&#41;](../mdx/firstsibling-mdx.md)  
  
  
