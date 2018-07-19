---
title: Lag (MDX) |Microsoft 文件
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3c5479aa3ce855b554f34f72c5c86aa86eb04b9f
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740877"
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
  
 如果指定的落後是零，**延隔**函式會傳回指定的成員本身。  
  
 如果指定的落後是負數，**延隔**函式會傳回後續成員。  
  
 `Lag(1)` 相當於[PrevMember](../mdx/prevmember-mdx.md)函式。 `Lag(-1)` 相當於[NextMember](../mdx/nextmember-mdx.md)函式。  
  
 **延隔**函數很相似[導致](../mdx/lead-mdx.md)函式中，不同處在於**導致**函式會以相反的方向，以尋找**延隔**函式。 也就是說，`Lag(n)` 相當於 `Lead(-n)`。  
  
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
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
