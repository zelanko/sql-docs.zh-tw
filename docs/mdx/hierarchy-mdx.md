---
title: "階層 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: Hierarchy
dev_langs: kbMDX
helpviewer_keywords: Hierarchy function
ms.assetid: 5ddf354f-8cae-4e3a-8803-0055fa86bad1
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c825c5444cd69d7c66f9f7a44cddbf8bbd6b3491
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="hierarchy-mdx"></a>Hierarchy (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回含有特定成員或層級的階層式架構。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member expression syntax  
Member_Expression.Hierarchy  
  
Level expression syntax  
Level_Expression.Hierarchy  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
### <a name="examples"></a>範例  
 下列範例會傳回 AdventureWorks cube 中 Date 維度中 Calendar 階層的名稱。  
  
 `WITH`  
  
 `MEMBER Measures.HierarchyName as`  
  
 `[Date].[Calendar].Currentmember.Hierarchy.Name`  
  
 `SELECT {Measures.HierarchyName}  ON 0,`  
  
 `{[Date].[Calendar].[All Periods]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
