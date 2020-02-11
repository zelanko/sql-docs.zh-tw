---
title: Count （維度）（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b84c5a1902e80f8abe3828f4be1b5d570ec026ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104816"
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
 [計算 &#40;元組&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [&#40;&#41; &#40;MDX 的階層層級計數&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [&#40;&#41; &#40;MDX&#41;設定計數](../mdx/count-set-mdx.md)   
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
