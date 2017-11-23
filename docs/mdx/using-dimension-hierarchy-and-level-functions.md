---
title: "使用維度、 階層和層級函數 |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- dimensions [Analysis Services], functions
- level functions [MDX]
- hierarchy functions [MDX]
ms.assetid: e730f65a-1798-4094-9acf-2739e2505d52
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 0138b030823990b0bb5ec052ab8791f7ac3e5879
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="using-dimension-hierarchy-and-level-functions"></a>使用維度、階層及層級函數
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  維度、階層及層級函數對於跨越在 Analysis Services 中找到的多維度結構很有幫助。 一般來說，您可以將這類函數與其他函數一起使用，以取得有關維度、階層或層級成員的資訊。  
  
 下列範例示範如何使用**。維度**， **。階層**，和**。層級**函式：  
  
 `WITH`  
  
 `MEMBER MEASURES.DIMENSIONNAME AS [Date].[Calendar].CURRENTMEMBER.DIMENSION.NAME`  
  
 `MEMBER MEASURES.HIERARCHYNAME AS [Date].[Calendar].CURRENTMEMBER.HIERARCHY.NAME`  
  
 `MEMBER MEASURES.LEVELNAME AS [Date].[Calendar].LEVEL.NAME`  
  
 `SELECT`  
  
 `{MEASURES.DIMENSIONNAME, MEASURES.HIERARCHYNAME, MEASURES.LEVELNAME}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>請參閱＜  
 [維度 &#40;MDX &#41;](../mdx/dimension-mdx.md)   
 [函式 &#40;MDX 語法 &#41;](../mdx/functions-mdx-syntax.md)   
 [階層 &#40;MDX &#41;](../mdx/hierarchy-mdx.md)   
 [層級 &#40;MDX &#41;](../mdx/level-mdx.md)  
  
  
