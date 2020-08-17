---
description: Members (集合) (MDX)
title: 成員 (設定)  (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0358f20d0aeba0e4d455fabadb6dc1e4361081e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341394"
---
# <a name="members-set-mdx"></a>Members (集合) (MDX)


  傳回維度、層級或階層架構中成員的集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Hierarchy expression syntax  
Hierarchy_Expression.Members  
  
Level expression Syntax  
Level_Expression.Members  
```  
  
## <a name="arguments"></a>引數  
 *Hierarchy_Expression*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果指定了階層運算式， ** (設定) ** 函數的成員會傳回指定階層內所有成員的集合，而不包含匯出成員。 若要取得階層中所有成員的集合（已計算或其他），請使用 [AllMembers &#40;MDX&#41;](../mdx/allmembers-mdx.md) 函數  
  
 如果指定了層級運算式， ** (設定) ** 函數的成員會傳回指定層級內所有成員的集合。  
  
> [!IMPORTANT]  
>  當維度只包含單一可見的階層，該階層可由維度名稱或階層名稱參考，因為此狀況下維度名稱會解析成其唯一可見的階層。 例如，Measures.Members 是有效 MDX 運算式，因為它會解析成 Measures 維度中的唯一階層。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 Adventure Works Cube 中 Calendar Year 階層之所有成員的集合。  
  
```  
SELECT   
   [Date].[Calendar].[Calendar Year].Members ON 0  
FROM  
   [Adventure Works]  
  
```  
  
 下列範例會傳回 `[Product].[Products].[Product Line]` 層級中每個成員的 2003 年訂單數量。 **Members**函數會傳回一個集合，代表層級中的所有成員。  
  
```  
SELECT   
   {Measures.[Order Quantity]} ON COLUMNS,  
   [Product].[Product Line].[Product Line].Members ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
