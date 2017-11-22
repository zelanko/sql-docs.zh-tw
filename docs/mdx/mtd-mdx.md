---
title: "Mtd (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: MTD
dev_langs: kbMDX
helpviewer_keywords: Mtd function
ms.assetid: 07d8fd65-f9e6-42d4-868d-fccfac6bdb70
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 56358755a2a1baeae336e071cd017f299401ec89
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="mtd-mdx"></a>Mtd (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回與指定成員層級相同的同層級成員集合，以第一個同層級成員開始，以指定的成員結束，如同受 Time 維度中的 Year 層級條件約束。  
  
## <a name="syntax"></a>語法  
  
```  
  
Mtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果未指定成員運算式，預設值是類型層級之第一個階層的目前成員*月*類型的第一個維度*時間*量值群組中。  
  
 **Mtd**函式是的捷徑函數[PeriodsToDate](../mdx/periodstodate-mdx.md)函式時所依據的層級的屬性階層的 Type 屬性設定為*月*。 也就是說，`Mtd(Member_Expression)` 相當於 `PeriodsToDate(Month_Level_Expression,Member_Expression)`。  
  
## <a name="example"></a>範例  
 下列範例會傳回 2002 年 7 月初至 7 月 20 日當月網際網路銷售的月運費成本總和。  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>請參閱＜  
 [Sum &#40;MDX &#41;](../mdx/sum-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
