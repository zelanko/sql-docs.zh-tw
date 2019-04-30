---
title: 這個 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 77db403ee016283a565a6bc86d2f6857de0eff45
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259033"
---
# <a name="this-mdx"></a>This (MDX)


  傳回目前的 Subcube，用於多維度運算式 (MDX) 計算指令碼中的指派。  
  
## <a name="syntax"></a>語法  
  
```  
  
This   
```  
  
## <a name="remarks"></a>備註  
 **這**函式可以取代任何 subcube 運算式用來提供 MDX 計算指令碼中目前的範圍內目前的 subcube。 **這**函數必須用於指派左邊。  
  
## <a name="examples"></a>範例  
 下列 MDX 指令碼片段會示範如何搭配 SCOPE 陳述式使用 This 關鍵字來對 Subcube 進行指派：  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2005],`  
  
 `[Date].[Fiscal].[Fiscal Quarter].Members,`  
  
 `[Measures].[Sales Amount Quota]`  
  
 `) ;`  
  
 `This = ParallelPeriod`  
  
 `(`  
  
 `[Date].[Fiscal].[Fiscal Year], 1,`  
  
 `[Date].[Fiscal].CurrentMember`  
  
 `) * 1.35 ;`  
  
 `/*-- Allocate equally to months in FY 2002 -----------------------------*/`  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2002],`  
  
 `[Date].[Fiscal].[Month].Members`  
  
 `) ;`  
  
 `This = [Date].[Fiscal].CurrentMember.Parent / 3 ;`  
  
 `End Scope ;`  
  
 `End Scope;`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [計算](../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
