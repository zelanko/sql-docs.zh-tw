---
title: 子集 (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- subset
dev_langs:
- kbMDX
helpviewer_keywords:
- Subset function
ms.assetid: 49a7cd28-cd6f-4ae7-8c91-94a8652a97a5
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6f461f979c9d064305b0004fb906673e97f2ab5f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="subset-mdx"></a>Subset (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  從指定集合中傳回 Tuple 的子集。  
  
## <a name="syntax"></a>語法  
  
```  
  
Subset(Set_Expression, Start [ ,Count ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *啟動*  
 有效的數值運算式，會指定要傳回之第一個 Tuple 的位置。  
  
 *計數*  
 有效的數值運算式，會指定要傳回的 Tuple 數目。  
  
## <a name="remarks"></a>備註  
 從指定的集合，**子集**函式會傳回包含指定的 tuple，從指定的開始位置開始數目的子集。 開始位置是根據以零為基底的索引，也就是說，零 (0) 對應至指定集合中的第一個 Tuple，1 對應至第二個，依此類推。  
  
 如果*計數*未指定，則函數會傳回從所有 tuple*啟動*至集合結尾。  
  
## <a name="example"></a>範例  
 下列範例不考慮階層，而根據 Reseller Gross Profit 傳回前五名產品銷售子類別的 Reseller Sales 量值。 **子集**函數用來使用排序結果之後，結果中傳回的前五個集合**順序**函式。  
  
```  
SELECT Subset  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,0  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
