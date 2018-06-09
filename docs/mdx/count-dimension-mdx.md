---
title: Count （維度） (MDX) |Microsoft 文件
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6ee8fe09f7a840d32511d3a208a4621612ee9939
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740147"
---
# <a name="count-dimension-mdx"></a>Count (維度) (MDX)


  傳回 Cube 中的階層數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
Dimensions.Count   
```  
  
## <a name="remarks"></a>備註  
 傳回 Cube 中的階層數目，包括 `[Measures].[Measures]` 階層。  
  
## <a name="example"></a>範例  
 下列範例會傳回 Adventure Works Cube 中的階層數目。  
  
```  
WITH MEMBER measures.X AS  
  dimensions.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [計數&#40;Tuple&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [計數&#40;階層層級&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [計數&#40;設定&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
