---
title: "一元運算子 |Microsoft 文件"
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
dev_langs: kbMDX
helpviewer_keywords: unary operators
ms.assetid: bf1b5518-6040-4484-9ce8-79c0eb4373a9
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a2dd50160dbe0185056988cfd866f119d7e330c4
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="unary-operators"></a>一元運算子
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在多維度運算式 (MDX) 中，一元運算子在單一運算元上執行作業，例如傳回數值運算式的負或正值。  
  
 MDX 支援下表中列出的一元運算子。  
  
|運算子|Description|  
|--------------|-----------------|  
|[- (負)](../mdx/negative-mdx.md)|傳回數值運算式的負值。|  
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
  
 此外，MDX 使用特殊的一元運算子來判斷所執行的彙總作業[RollupChildren](../mdx/rollupchildren-mdx.md)函式。 如需有關這些特殊一元運算子的詳細資訊，請參閱[將自訂彙總加入維度](../analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension.md)。  
  
## <a name="see-also"></a>請參閱  
 [運算子 &#40;MDX 語法 &#41;](../mdx/operators-mdx-syntax.md)  
  
  
