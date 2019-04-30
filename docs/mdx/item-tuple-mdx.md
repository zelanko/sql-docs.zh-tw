---
title: 項目 (Tuple) (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 58cb48c467bbd3ca1c929da1fdff4881086d2e1d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273083"
---
# <a name="item-tuple-mdx"></a>Item (Tuple) (MDX)


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
 **項目**函數會傳回 tuple，從指定的集合。 有三種方式，來呼叫**項目**函式：  
  
-   如果指定的單一字串運算式，則**項目**函式會傳回指定的 tuple。 例如，"([2005].Q3, [Store05])"。  
  
-   如果指定多個字串運算式，則**項目**函式會傳回指定的座標所定義的 tuple。 字串數目必須與座標軸數目相符，而且每個字串必須識別唯一的階層。 例如，"[2005].Q3", "[Store05]"。  
  
-   如果指定一個整數，則**項目**函式會傳回以零為起始的位置所指定的 tuple *Index*。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 ([1996],Sales)：  
  
 `{([1996],Sales), ([1997],Sales), ([1998],Sales)}.Item(0)`  
  
 下列範例使用層級運算式，並且會傳回 Australia 每個 State-Province 的 Internet Sales Amount，及其佔 Australia 之 Internet Sales Amount 總計的百分比。 此範例使用 Item 函數來擷取所傳回的集合中的第一個 （也只有 tuple）**祖系**函式。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
