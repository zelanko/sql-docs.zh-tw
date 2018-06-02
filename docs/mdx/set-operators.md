---
title: 設定運算子 |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1388c5ef1f263f4ef326485c662a82ee11c569d0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580950"
---
# <a name="set-operators"></a>設定運算子
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在多維度運算式  (MDX) 中，集合運算子會在成員或集合上執行作業，然後傳回一個集合。 您通常會使用集合運算子，作為 MDX 運算式中數個集合函數的替代項。  
  
 MDX 支援下表中列出的集合運算子。  
  
|運算子|描述|  
|--------------|-----------------|  
|[- (排除)](../mdx/except-mdx-operator.md)|傳回兩個集合間的差異，同時移除重複的成員。<br /><br /> 這個運算子在功能上等於[除了](../mdx/except-mdx-function.md)函式。|  
|[* (交叉聯結)](../mdx/crossjoin-mdx-operator-reference.md)|傳回兩個集合的交叉產品(Cross Product)。<br /><br /> 這個運算子在功能上等於[Crossjoin](../mdx/crossjoin-mdx.md)函式。|  
|[: (範圍)](../mdx/range-mdx.md)|傳回一個自然順序的集合，以兩個指定成員作為端點，而介於這兩個成員之間的所有成員都會被併入為集合的成員。|  
|[(聯集)](../mdx/union-mdx-operator-reference.md)|傳回兩個集合的聯集，同時排除重複成員。<br /><br /> 這個運算子在功能上等於[Union &#40;MDX&#41; ](../mdx/union-mdx.md)函式。|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 運算子參考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [運算子&#40;MDX 語法&#41;](../mdx/operators-mdx-syntax.md)  
  
  
