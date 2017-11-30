---
title: "計數 (Tuple) (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: COUNT
dev_langs: kbMDX
helpviewer_keywords: Count function [MDX]
ms.assetid: c8f4a570-54a8-4c00-ac4b-eef0ebdb353c
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fedac649113ec0e062d3b9697bf46c0e006e20b3
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
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
  
## <a name="see-also"></a>請參閱  
 [計數 &#40; 維度 &#41;&#40;MDX &#41;](../mdx/count-dimension-mdx.md)   
 [計數 &#40;階層層級 &#41;&#40;MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [計數 &#40;設定 &#41;&#40;MDX &#41;](../mdx/count-set-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
