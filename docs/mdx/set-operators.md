---
description: 設定運算子
title: 設定運算子 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb4434c9fe1991e1398baaa9c7bfd9602995652d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341234"
---
# <a name="set-operators"></a>設定運算子


  在多維度運算式  (MDX) 中，集合運算子會在成員或集合上執行作業，然後傳回一個集合。 您通常會使用集合運算子，作為 MDX 運算式中數個集合函數的替代項。  
  
 MDX 支援下表中列出的集合運算子。  
  
|運算子|描述|  
|--------------|-----------------|  
|[- (排除)](../mdx/except-mdx-operator.md)|傳回兩個集合間的差異，同時移除重複的成員。<br /><br /> 這個運算子的功能等同于 [Except](../mdx/except-mdx-function.md) 函數。|  
|[* (交叉聯結)](../mdx/crossjoin-mdx-operator-reference.md)|傳回兩個集合的交叉產品(Cross Product)。<br /><br /> 這個運算子在功能上等同于 [交叉](../mdx/crossjoin-mdx.md) 聯結函數。|  
|[： (範圍) ](../mdx/range-mdx.md)|傳回一個自然順序的集合，以兩個指定成員作為端點，而介於這兩個成員之間的所有成員都會被併入為集合的成員。|  
|[(聯集)](../mdx/union-mdx-operator-reference.md)|傳回兩個集合的聯集，同時排除重複成員。<br /><br /> 這個運算子在功能上等同于 [Union &#40;MDX&#41;](../mdx/union-mdx.md) 函數。|  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [運算子 &#40;MDX 語法&#41;](../mdx/operators-mdx-syntax.md)  
  
  
