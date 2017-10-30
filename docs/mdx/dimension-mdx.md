---
title: "維度 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Dimension
dev_langs:
- kbMDX
helpviewer_keywords:
- Dimension function
ms.assetid: 0e3ce539-1d34-45ca-8342-67796e11b730
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4d8bbf0f22d1a2370c167f2569ae388742836933
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="dimension-mdx"></a>Dimension (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回含有特定成員、層級或階層的階層。  
  
## <a name="syntax"></a>語法  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.Dimension  
  
Level syntax  
Level_Expression.Dimension  
  
Member syntax  
Member_Expression.Dimension  
  
```  
  
## <a name="arguments"></a>引數  
 *Hierarchy_Expression*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
### <a name="examples"></a>範例  
 下列範例會使用**維度**函數搭配**名稱**函式，以傳回指定成員的階層名稱。  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Name  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 下列範例使用 Dimension 函數搭配 Levels 和 Count 函數，來傳回含有特定成員之階層中的層級數目。  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 下列範例會使用**維度**函數搭配**成員**和**計數**函數，來傳回含有特定的成員在階層中的成員數目。  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [計數 &#40;階層層級 &#41;&#40;MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [計數 &#40;設定 &#41;&#40;MDX &#41;](../mdx/count-set-mdx.md)   
 [層級 &#40;MDX &#41;](../mdx/levels-mdx.md)   
 [成員 &#40;設定 &#41;&#40;MDX &#41;](../mdx/members-set-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

