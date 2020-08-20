---
description: 一元運算子
title: 一元運算子 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 32f5084190642bd4237d225404c92f0c4754da7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466470"
---
# <a name="unary-operators"></a>一元運算子


  在多維度運算式 (MDX) 中，一元運算子在單一運算元上執行作業，例如傳回數值運算式的負或正值。  
  
 MDX 支援下表中列出的一元運算子。  
  
|運算子|描述|  
|--------------|-----------------|  
|[- (負) ](../mdx/negative-mdx.md)|傳回數值運算式的負值。|  
|[+ (正)](../mdx/positive-mdx.md)|傳回數值運算式的正值。|  
  
 以下範例示範使用一元運算子傳回量值的負值：  
  
```  
WITH   
   MEMBER [Measures].[NegDiscountAmount] AS  
   -[Measures].[Discount Amount]  
SELECT   
   {[Measures].[Discount Amount],[Measures].[NegDiscountAmount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 此外，MDX 使用特殊的一元運算子來判斷 [RollupChildren](../mdx/rollupchildren-mdx.md) 函數所執行的匯總作業。 如需有關這些特殊一元運算子的詳細資訊，請參閱 [將自訂匯總加入至維度](https://docs.microsoft.com/analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension)。  
  
## <a name="see-also"></a>另請參閱  
 [運算子 &#40;MDX 語法&#41;](../mdx/operators-mdx-syntax.md)  
  
  
