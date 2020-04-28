---
title: 使用成員函式 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 54f600eb020472f93067f7b9fe1e867f2730d670
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097103"
---
# <a name="using-member-functions"></a>使用成員函數


  成員函數是一種會傳回成員的多維度運算式 (MDX) 函數。 成員函數跟 tuple 函數和 set 函數一樣，對於交涉 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中找到的多維度結構而言不可或缺。  
  
 在 MDX 中的許多成員函式中，最重要的是**CurrentMember**函數，用來判斷階層上的目前成員。 下列查詢說明如何使用它，以及**Parent**、**祖系**和**Prevmember**函式：  
  
 `WITH`  
  
 `//Returns the name of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[CurrentMemberDemo] AS [Date].[Calendar].CurrentMember.Name`  
  
 `//Returns the name of the parent of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[ParentDemo] AS [Date].[Calendar].CurrentMember.Parent.Name`  
  
 `//Returns the name of the ancestor of the currentmember on the Calendar hierarchy at the Year level`  
  
 `MEMBER MEASURES.[AncestorDemo] AS ANCESTOR([Date].[Calendar].CurrentMember, [Date].[Calendar].[Calendar Year]).Name`  
  
 `//Returns the name of the member before the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[PrevMemberDemo] AS [Date].[Calendar].CurrentMember.Prevmember.Name`  
  
 `SELECT{MEASURES.[CurrentMemberDemo],MEASURES.[ParentDemo],MEASURES.[AncestorDemo],MEASURES.[PrevMemberDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [函數 &#40;MDX 語法&#41;](../mdx/functions-mdx-syntax.md)   
 [使用元組函數](../mdx/using-tuple-functions.md)   
 [使用集合函式](../mdx/using-set-functions.md)  
  
  
