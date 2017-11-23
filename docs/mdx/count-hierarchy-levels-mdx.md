---
title: "Count （階層層級） (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: COUNT
dev_langs: kbMDX
helpviewer_keywords: Count function [MDX]
ms.assetid: 3de6a824-2ff3-47ac-9ceb-e3369a04f35d
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ca18ec4161db5405055a3732007170167afc123c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="count-hierarchy-levels-mdx"></a>Count (階層層級) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回階層中的層級數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
Hierarchy_Expression.Levels.Count  
```  
  
## <a name="arguments"></a>引數  
 *Hierarchy_Expression*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 傳回階層中的層級數目，包括 `[All]` 層級 (若有的話)。  
  
> [!IMPORTANT]  
>  當維度只包含單一可見的階層，該階層可由維度名稱或階層名稱參考，因為維度名稱會解析成其唯一可見的階層。 例如，`Measures.Levels.Count` 即是有效的 MDX 運算式，因為它解析成量值維度上唯一的階層。  
  
## <a name="example"></a>範例  
 下列範例會傳回 Adventure Works Cube 中 Product Categories 使用者自訂階層的層級數目。  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Product Categories].Levels.Count   
Select Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>請參閱＜  
 [計數 &#40; 維度 &#41;&#40;MDX &#41;](../mdx/count-dimension-mdx.md)   
 [計數 &#40;Tuple &#41;&#40;MDX &#41;](../mdx/count-tuple-mdx.md)   
 [計數 &#40;設定 &#41;&#40;MDX &#41;](../mdx/count-set-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
