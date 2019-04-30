---
title: 子集合 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 07d813587dc530924becbb187a970f78022e5476
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63136086"
---
# <a name="subset-mdx"></a>Subset (MDX)


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
 從指定的集合**子集**函式會傳回包含指定的 tuple，開始於指定的起始位置數目的子集。 開始位置是根據以零為基底的索引，也就是說，零 (0) 對應至指定集合中的第一個 Tuple，1 對應至第二個，依此類推。  
  
 如果*計數*未指定，則函數會傳回所有來自 tuple*開始*至集合結尾。  
  
## <a name="example"></a>範例  
 下列範例不考慮階層，而根據 Reseller Gross Profit 傳回前五名產品銷售子類別的 Reseller Sales 量值。 **子集**函數用來在結果中傳回的前五個集合，使用排序結果之後**順序**函式。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
