---
description: Lag (MDX)
title: Lag (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bc9beb8215d8d690f2d4ccdf43c3aaf03096b9d8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477040"
---
# <a name="lag-mdx"></a>Lag (MDX)


  傳回成員層級中，在特定成員之前特定幾個位置的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.Lag(Index)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Index*  
 指定落後的成員位置數目之有效數值運算式。  
  
## <a name="remarks"></a>備註  
 層級內的成員位置是由屬性階層的自然順序決定。 位置的編號是以零為基底。  
  
 如果指定的延隔時間為零，則 **lag** 函數會傳回指定的成員本身。  
  
 如果指定的延隔是負數， **lag** 函數會傳回後續的成員。  
  
 `Lag(1)` 相當於 [PrevMember](../mdx/prevmember-mdx.md) 函數。 `Lag(-1)` 相當於 [NextMember](../mdx/nextmember-mdx.md) 函數。  
  
 **Lag**函數類似于[潛在客戶](../mdx/lead-mdx.md)函式，不同之處在于**潛在客戶**函數會與**Lag**函數的方向相反。 也就是說，`Lag(n)` 相當於 `Lead(-n)`。  
  
## <a name="example"></a>範例  
 下列範例會傳回 2001 年 12 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(2) ON 0  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回 2002 年 3 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(-1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
