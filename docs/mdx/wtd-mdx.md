---
title: Wtd （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eee40829c72394bf95a1bc06540a434a1c74e166
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125806"
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
 如果未指定成員運算式，預設值為第一個階層的目前成員，其在量值群組中類型為 Time （**CurrentMember**）的第一個維度中，類型為周。  
  
 **Wtd**函式是[PeriodsToDate](../mdx/periodstodate-mdx.md)函數的快捷方式函式，其層級設定為*周*。 也就是說，`Wtd(Member_Expression)` 相當於 `PeriodsToDate(Week_Level_Expression,Member_Expression)`。  
  
## <a name="see-also"></a>另請參閱  
 [Qtd &#40;MDX&#41;](../mdx/qtd-mdx.md)   
 [Mtd &#40;MDX&#41;](../mdx/mtd-mdx.md)   
 [年初迄今 &#40;MDX&#41;](../mdx/ytd-mdx.md)   
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
