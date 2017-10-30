---
title: "設定運算子 |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ed67b969d53eeb65009926cade623d2b87b9e175
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="set-operators"></a>設定運算子
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在多維度運算式  (MDX) 中，集合運算子會在成員或集合上執行作業，然後傳回一個集合。 您通常會使用集合運算子，作為 MDX 運算式中數個集合函數的替代項。  
  
 MDX 支援下表中列出的集合運算子。  
  
|運算子|Description|  
|--------------|-----------------|  
|[-（除外）](../mdx/except-mdx-operator.md)|傳回兩個集合間的差異，同時移除重複的成員。<br /><br /> 這個運算子在功能上等於[除了](../mdx/except-mdx-function.md)函式。|  
|[* （交叉聯集）](../mdx/crossjoin-mdx-operator-reference.md)|傳回兩個集合的交叉產品(Cross Product)。<br /><br /> 這個運算子在功能上等於[Crossjoin](../mdx/crossjoin-mdx.md)函式。|  
|[: （範圍)](../mdx/range-mdx.md)|傳回一個自然順序的集合，以兩個指定成員作為端點，而介於這兩個成員之間的所有成員都會被併入為集合的成員。|  
|[+ （聯集）](../mdx/union-mdx-operator-reference.md)|傳回兩個集合的聯集，同時排除重複成員。<br /><br /> 這個運算子在功能上等於[聯集 &#40;MDX &#41;](../mdx/union-mdx.md)函式。|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 運算子參考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [運算子 &#40;MDX 語法 &#41;](../mdx/operators-mdx-syntax.md)  
  
  

