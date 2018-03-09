---
title: ": （範圍) (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ':'
dev_langs: kbMDX
helpviewer_keywords:
- ': (range operator)'
- range operator (:)
ms.assetid: f9b36aca-4efd-49b4-9e4f-12914c1b24a6
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e9ca2a16a74ce772ce7737c6c30581522d6d30f1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="-range-mdx"></a>: (範圍) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  執行傳回一個自然順序集合的集合運算，其中會以兩個指定成員做為結束點，並將介於這兩個指定成員之間的所有成員當做集合的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression : Member_Expression      
```  
  
#### <a name="parameters"></a>參數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="return-value"></a>傳回值  
 包含指定成員以及指定成員間所有成員的集合。  
  
## <a name="remarks"></a>備註  
 兩個參數指定的成員，都必須在指定維度的相同層級與階層內。 如果這兩個參數指定相同的成員， **: （範圍）**運算子會傳回一個集合，包含指定的成員。 如果第一個參數為 Null，則集合會包含從第二個參數內指定之成員的層級開始的所有成員，一直到包含該成員為止。 如果第二個參數為 Null，則集合會包含從第一個參數內指定之成員開始的所有成員，一直到包含相同層級上的最後一個成員為止。  
  
 此集合運算在 MDX 中無相等函數。  
  
## <a name="examples"></a>範例  
 以下範例示範此運算子的用法。  
  
```  
-- This query returns the freight cost per user  
-- for products, averaged by month, for the first quarter.  
With Member [Measures].[Freight Per Customer] as  
 (  
     [Measures].[Internet Freight Cost]  
     /   
     [Measures].[Customer Count]  
)  
  
SELECT   
    {[Ship Date].[Calendar].[Month].&[2004]&[1] : [Ship Date].[Calendar].[Month].&[2004]&[3]} ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
## <a name="see-also"></a>請參閱  
 [MDX 運算子參考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
