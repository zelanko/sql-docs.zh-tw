---
description: Wtd (MDX)
title: Wtd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b45e583da6f7fc18712e432a0c504c3bc813141e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421882"
---
# <a name="wtd-mdx"></a>Wtd (MDX)


  傳回與指定成員層級相同的同層級成員集合，以第一個同層級成員開始，以指定的成員結束，如同受 Time 維度中的 Week 層級條件約束。  
  
## <a name="syntax"></a>語法  
  
```  
  
Wtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果沒有指定成員運算式，預設值就是在量值群組中的第一個維度中，第一個維度中的第一個維度層級為 [星期] (**CurrentMember**) 的第一個階層的目前成員。  
  
 **Wtd**函式是[PeriodsToDate](../mdx/periodstodate-mdx.md)函數的快捷方式函式，其中層級設定為*周*。 也就是說，`Wtd(Member_Expression)` 相當於 `PeriodsToDate(Week_Level_Expression,Member_Expression)`。  
  
## <a name="see-also"></a>另請參閱  
 [Qtd &#40;MDX&#41;](../mdx/qtd-mdx.md)   
 [Mtd &#40;MDX&#41;](../mdx/mtd-mdx.md)   
 [Ytd &#40;MDX&#41;](../mdx/ytd-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
