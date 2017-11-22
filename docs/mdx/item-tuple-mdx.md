---
title: "項目 (Tuple) (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ITEM
dev_langs: kbMDX
helpviewer_keywords: Item function
ms.assetid: 9ee7af55-d5b5-47c8-a480-ef23878306af
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: df6a2bcfe94dfdbcbb957f2c137e35740879568f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="item-tuple-mdx"></a>Item (Tuple) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從集合傳回一個 Tuple。  
  
## <a name="syntax"></a>語法  
  
```  
  
Index syntax  
Set_Expression.Item(Index)  
  
String expression syntax  
Set_Expression.Item(String_Expression1 [ ,String_Expression2,...n])  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *String_Expression1*  
 一般是以字串表示之 Tuple 的有效字串運算式。  
  
 *String_Expression2*  
 一般是以字串表示之 Tuple 的有效字串運算式。  
  
 *Index*  
 有效的數值運算式，依所要傳回的集合中的位置來指定特定的 Tuple。  
  
## <a name="remarks"></a>備註  
 **項目**函式會傳回 tuple，從指定的集合。 有三種方式，來呼叫**項目**函式：  
  
-   如果指定的單一字串運算式，則**項目**函式會傳回指定的 tuple。 例如，"([2005].Q3, [Store05])"。  
  
-   如果指定多個字串運算式，**項目**函式會傳回指定座標所定義的 tuple。 字串數目必須與座標軸數目相符，而且每個字串必須識別唯一的階層。 例如，"[2005].Q3", "[Store05]"。  
  
-   如果指定一個整數，則**項目**函式會傳回所指定的以零為起始的位置中的 tuple*索引*。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 ([1996],Sales)：  
  
 `{([1996],Sales), ([1997],Sales), ([1998],Sales)}.Item(0)`  
  
 下列範例使用層級運算式，並且會傳回 Australia 每個 State-Province 的 Internet Sales Amount，及其佔 Australia 之 Internet Sales Amount 總計的百分比。 這個範例使用 Item 函數所傳回集合中擷取第一個 （也只有 tuple）**祖系**函式。  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],    
      Ancestors   
      ( [Customer].[Customer Geography].CurrentMember,  
        [Customer].[Customer Geography].[Country]  
      ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{ Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],  
     [Customer].[Customer Geography].[State-Province], SELF   
   )   
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>請參閱＜  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
