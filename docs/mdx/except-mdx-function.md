---
title: 除了 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 03d9b5140eb0cbf9d868e43c65213efe917994a9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62690875"
---
# <a name="except-mdx-function"></a>Except 函數 (MDX)


  評估兩個集合並且從第一個集合中移除同時存在於第二個集合中的 Tuple，選擇性地保留重複項。  
  
## <a name="syntax"></a>語法  
  
```  
  
Except(Set_Expression1, Set_Expression2 [, ALL ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression1*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Set_Expression2*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果**所有**是指定函式會保留第一個集合中找到的重複項目; 在第二個集合中找到的重複項目仍然會被移除。 成員依第一個集合中的出現順序傳回。  
  
## <a name="examples"></a>範例  
 以下範例示範此函數的用法。  
  
```  
   //This query shows the quantity of orders for all products,  
   //with the exception of Components, which are not  
   //sold.  
SELECT   
   [Date].[Month of Year].Children  ON COLUMNS,  
   Except  
      ([Product].[Product Categories].[All].Children ,  
         {[Product].[Product Categories].[Components]}  
      ) ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   ([Measures].[Order Quantity])  
```  
  
## <a name="see-also"></a>另請參閱  
 [- &#40;Except&#41; &#40;MDX&#41;](../mdx/except-mdx-operator.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
