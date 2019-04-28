---
title: 使用維度、 階層及層級函數 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fb6460ed28c856ef6b5ceea8bf89c7bf33f54f2e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62982194"
---
# <a name="using-dimension-hierarchy-and-level-functions"></a>使用維度、階層及層級函數


  維度、階層及層級函數對於跨越在 Analysis Services 中找到的多維度結構很有幫助。 一般來說，您可以將這類函數與其他函數一起使用，以取得有關維度、階層或層級成員的資訊。  
  
 下列範例示範如何使用 **。維度**， **。階層**，和 **。層級**函式：  
  
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
  
## <a name="see-also"></a>另請參閱  
 [維度&#40;MDX&#41;](../mdx/dimension-mdx.md)   
 [函式&#40;MDX 語法&#41;](../mdx/functions-mdx-syntax.md)   
 [Hierarchy &#40;MDX&#41;](../mdx/hierarchy-mdx.md)   
 [Level &#40;MDX&#41;](../mdx/level-mdx.md)  
  
  
