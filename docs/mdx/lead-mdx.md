---
description: Lead (MDX)
title: 潛在客戶 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ca78bdeca6103758d5d102ed8b85eb00b3138e18
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387324"
---
# <a name="lead-mdx"></a>Lead (MDX)


  傳回成員層級中，在特定成員之後特定幾個位置的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.Lead( Index )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Index*  
 指定成員位置數目的有效數值運算式。  
  
## <a name="remarks"></a>備註  
 層級內的成員位置是由屬性階層的自然順序決定。 位置的編號是以零為基底。  
  
 如果指定的 lead 是零 (0) ，則 **潛在客戶** 函數會傳回指定的成員。  
  
 如果指定的潛在客戶為負數，則 **潛在客戶** 函數會傳回先前的成員。  
  
 `Lead(1)` 相當於 [NextMember](../mdx/nextmember-mdx.md) 函數。 `Lead(-1)` 相當於 [PrevMember](../mdx/prevmember-mdx.md) 函數。  
  
 **Lead**函數與[lag](../mdx/lag-mdx.md)函數類似，但**lag**函式與**Lead**函數的方向相反。 也就是說，`Lead(n)` 相當於 `Lag(-n)`。  
  
## <a name="example"></a>範例  
 下列範例會傳回 2001 年 12 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(-2) ON 0  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回 2002 年 3 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
