---
description: Item (Tuple) (MDX)
title: 專案 (元組)  (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1e98e6901c018a6c8be5187024e5462cc8d19547
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483951"
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
 **Item**函數會從指定的集合傳回元組。 有三種可能的方法可以呼叫 **Item** 函數：  
  
-   如果指定了單一字串運算式，則 **Item** 函數會傳回指定的元組。 例如，"([2005].Q3, [Store05])"。  
  
-   如果指定了一個以上的字串運算式， **Item** 函數會傳回指定座標所定義的元組。 字串數目必須與座標軸數目相符，而且每個字串必須識別唯一的階層。 例如，"[2005].Q3", "[Store05]"。  
  
-   如果指定整數， **Item** 函式會傳回在 *索引*所指定之以零為基底的位置的元組。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 ([1996],Sales)：  
  
 `{([1996],Sales), ([1997],Sales), ([1998],Sales)}.Item(0)`  
  
 下列範例使用層級運算式，並且會傳回 Australia 每個 State-Province 的 Internet Sales Amount，及其佔 Australia 之 Internet Sales Amount 總計的百分比。 這個範例會使用 Item 函式，將第一個 (，而只有來自 **祖** 系函數所傳回之集合的元組) 。  
  
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
  
  
