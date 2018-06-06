---
title: 維度 (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: af73d6f08432a63a207c06d361354d6e45b6a07d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577930"
---
# <a name="dimension-mdx"></a>Dimension (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [計數&#40;階層層級&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [計數&#40;設定&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [層級&#40;MDX&#41;](../mdx/levels-mdx.md)   
 [成員&#40;設定&#41; &#40;MDX&#41;](../mdx/members-set-mdx.md)   
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
