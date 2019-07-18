---
title: OpeningPeriod (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 07f94c3ed850af10120b1de7d95941bc5c90e826
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088226"
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
  
-   如果指定層級運算式，則**OpeningPeriod**函式會使用包含指定的層級，並傳回指定層級的預設成員之下階當中的第一個同層級的階層。  
  
-   如果指定層級運算式和成員運算式，則**OpeningPeriod**函式會傳回含有指定之階層內指定層級的指定成員之下階當中的第一個同層級層級。  
  
-   如果指定層級運算式或成員運算式， **OpeningPeriod**函式會使用預設層級和成員的維度類型的時間。  
  
> [!NOTE]  
>  [ClosingPeriod](../mdx/closingperiod-mdx.md)函數很相似**OpeningPeriod**函式，不同之處在於**ClosingPeriod**函式會傳回最後一個同層級，而不是第一個同層級。  
  
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
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [FirstSibling &#40;MDX&#41;](../mdx/firstsibling-mdx.md)  
  
  
