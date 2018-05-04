---
title: 設定運算子 |Microsoft 文件
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
dev_langs:
- kbMDX
helpviewer_keywords:
- set operators [MDX]
ms.assetid: 83500d2e-44b3-49eb-a221-3ce5a58277a5
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 860a95d1e16a2404a13812ca77cf0c0a46ae7ead
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="set-operators"></a>設定運算子
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在多維度運算式  (MDX) 中，集合運算子會在成員或集合上執行作業，然後傳回一個集合。 您通常會使用集合運算子，作為 MDX 運算式中數個集合函數的替代項。  
  
 MDX 支援下表中列出的集合運算子。  
  
|運算子|Description|  
|--------------|-----------------|  
|[- (排除)](../mdx/except-mdx-operator.md)|傳回兩個集合間的差異，同時移除重複的成員。<br /><br /> 這個運算子在功能上等於[除了](../mdx/except-mdx-function.md)函式。|  
|[* (交叉聯結)](../mdx/crossjoin-mdx-operator-reference.md)|傳回兩個集合的交叉產品(Cross Product)。<br /><br /> 這個運算子在功能上等於[Crossjoin](../mdx/crossjoin-mdx.md)函式。|  
|[: (範圍)](../mdx/range-mdx.md)|傳回一個自然順序的集合，以兩個指定成員作為端點，而介於這兩個成員之間的所有成員都會被併入為集合的成員。|  
|[(聯集)](../mdx/union-mdx-operator-reference.md)|傳回兩個集合的聯集，同時排除重複成員。<br /><br /> 這個運算子在功能上等於[Union &#40;MDX&#41; ](../mdx/union-mdx.md)函式。|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 運算子參考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [運算子&#40;MDX 語法&#41;](../mdx/operators-mdx-syntax.md)  
  
  
