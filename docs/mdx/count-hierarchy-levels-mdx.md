---
title: Count （階層層級） (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 17fe804de8bf2c20581ca5c00bee3a28dbce4d55
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045197"
---
# <a name="count-hierarchy-levels-mdx"></a>Count (階層層級) (MDX)


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
  
## <a name="see-also"></a>另請參閱  
 [計數&#40;維度&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [計數&#40;Tuple&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [Count &#40;集合&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
