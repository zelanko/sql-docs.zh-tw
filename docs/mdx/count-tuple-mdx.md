---
title: 計數 (Tuple) (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 15523d50b928bda0ae32eaa784dad046a4b66d7c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577560"
---
# <a name="count-tuple-mdx"></a>Count (Tuple) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [計數&#40;維度&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [計數&#40;階層層級&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [計數&#40;設定&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
