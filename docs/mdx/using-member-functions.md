---
title: "使用成員函式 |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: member functions [MDX]
ms.assetid: 094c443f-0daa-4af7-801c-d2e1d686d755
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 933242defcbaa9583298d8f6a7b0e5e4a8be4da8
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="using-member-functions"></a>使用成員函數
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  成員函數是一種會傳回成員的多維度運算式 (MDX) 函數。 成員函數跟 tuple 函數和 set 函數一樣，對於交涉 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中找到的多維度結構而言不可或缺。  
  
 最重要的是在 MDX 中的許多成員函式， **CurrentMember**函式，以用來判斷階層上的目前成員。 下列查詢說明如何使用它，連同**父**，**祖系**，和**Prevmember**函式：  
  
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
  
## <a name="see-also"></a>請參閱  
 [函式 &#40;MDX 語法 &#41;](../mdx/functions-mdx-syntax.md)   
 [使用 Tuple 函數](../mdx/using-tuple-functions.md)   
 [使用集合函式](../mdx/using-set-functions.md)  
  
  
