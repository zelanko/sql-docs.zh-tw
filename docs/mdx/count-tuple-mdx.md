---
description: Count (Tuple) (MDX)
title: 計算 (元組)  (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4212e3ed86d10035793cecd45ab071feb57e5abf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500551"
---
# <a name="count-tuple-mdx"></a>Count (Tuple) (MDX)


  傳回 Tuple 中的維度數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
Tuple_Expression.Count  
```  
  
## <a name="arguments"></a>引數  
 *Tuple_Expression*  
 傳回 Tuple 的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 傳回 Tuple 中的維度數目。  
  
## <a name="example"></a>範例  
 下列查詢中的導出量值會傳回值 2，這是出現在 Tuple `([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001])` 中的階層數目：  
  
```  
WITH MEMBER MEASURES.COUNTTUPLE AS  
COUNT(([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001]))  
SELECT MEASURES.COUNTTUPLE ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;維度的計數&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [&#40;階層層級的計數&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [&#40;設定&#41; &#40;MDX&#41;的計數 ](../mdx/count-set-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
