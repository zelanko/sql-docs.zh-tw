---
title: "使用成員函式 |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- member functions [MDX]
ms.assetid: 094c443f-0daa-4af7-801c-d2e1d686d755
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9354c2e6a83918742f1c2de1dea943be4b21e844
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="using-member-functions"></a>使用成員函數
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>另請參閱  
 [函式 &#40;MDX 語法 &#41;](../mdx/functions-mdx-syntax.md)   
 [使用 Tuple 函數](../mdx/using-tuple-functions.md)   
 [使用 Set 函式](../mdx/using-set-functions.md)  
  
  

