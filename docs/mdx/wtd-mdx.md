---
title: "Wtd (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: WTD
dev_langs: kbMDX
helpviewer_keywords: Wtd function
ms.assetid: 41066e1b-e802-4582-be4b-3ed7807b033e
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ef274decb624474873e3efa3f0a8860dfdbfff80
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="wtd-mdx"></a>Wtd (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回與指定成員層級相同的同層級成員集合，以第一個同層級成員開始，以指定的成員結束，如同受 Time 維度中的 Week 層級條件約束。  
  
## <a name="syntax"></a>語法  
  
```  
  
Wtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果未指定成員運算式，預設值是類型層級之第一個階層的目前成員中 Time 類型之第一個維度的週 (**Time.CurrentMember**) 量值群組中。  
  
 **Wtd**函式是的捷徑函數[PeriodsToDate](../mdx/periodstodate-mdx.md)函式之層級設定為*週*。 也就是說，`Wtd(Member_Expression)` 相當於 `PeriodsToDate(Week_Level_Expression,Member_Expression)`。  
  
## <a name="see-also"></a>請參閱＜  
 [Qtd &#40;MDX &#41;](../mdx/qtd-mdx.md)   
 [Mtd &#40;MDX &#41;](../mdx/mtd-mdx.md)   
 [Ytd &#40;MDX &#41;](../mdx/ytd-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
