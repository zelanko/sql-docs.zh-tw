---
title: 使用邏輯函式 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a63d8cb22a8533cf352acb690f87916e2e9d568d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63249830"
---
# <a name="using-logical-functions"></a>使用邏輯函數


  邏輯函數可對物件及運算式執行邏輯作業或比較，然後傳回布林值。 多維度運算式 (MDX) 中必須要有邏輯函數，才能判斷成員的位置。  
  
 最常使用的邏輯函式**IsEmpty**函式。 如需有關如何使用**IsEmpty**函式中，請參閱[使用空白值](../mdx/working-with-empty-values.md)。  
  
 下列查詢會示範如何使用**IsLeaf**並**IsAncestor**函式：  
  
 `WITH`  
  
 `//Returns true if the CurrentMember on Calendar is a leaf member, ie it has no children`  
  
 `MEMBER MEASURES.[IsLeafDemo] AS IsLeaf([Date].[Calendar].CurrentMember)`  
  
 `//Returns true if the CurrentMember on Calendar is an Ancestor of July 1st 2001`  
  
 `MEMBER MEASURES.[IsAncestorDemo] AS IsAncestor([Date].[Calendar].CurrentMember, [Date].[Calendar].[Date].&[1])`  
  
 `SELECT{MEASURES.[IsLeafDemo],MEASURES.[IsAncestorDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [函式&#40;MDX 語法&#41;](../mdx/functions-mdx-syntax.md)  
  
  
