---
title: NonEmptyCrossjoin (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7da56ac658f57d6eb664762f9dd94351df39fe0f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63456563"
---
# <a name="nonemptycrossjoin-mdx"></a>NonEmptyCrossjoin (MDX)


  傳回包含了一或多個集合之交叉乘積的集合，排除空的 Tuple 與沒有相關事實資料表資料的 Tuple。  
  
## <a name="syntax"></a>語法  
  
```  
  
NonEmptyCrossjoin(Set_Expression1 [ ,Set_Expression2,...] [,Count ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression1*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Set_Expression2*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *計數*  
 有效的數值運算式，會指定要傳回的集合數目。  
  
## <a name="remarks"></a>備註  
 **NonEmptyCrossjoin**函式會傳回兩個或多個集合的交叉乘積的集合，排除空的 tuple，但不含基礎事實資料表所提供的資料。 因為如何**NonEmptyCrossjoin**函式的運作，所有導出成員會自動排除。  
  
 如果*計數*未指定，函式交叉聯結所有指定的集合，並從結果集排除空白成員。 如果指定了集合數目，此函數就會由第一個指定的集合開始，交叉聯結指定的集合數目。 **NonEmptyCrossjoin**函式會使用任何剩餘的集合，後續指定集合中指定，但尚未進行交叉聯結以判斷哪些成員被視為非空白交叉聯結結果集中。 **NonEmptyCrossjoin**運作方面**NON_EMPTY_BEHAVIOR**導出量值的設定。  
  
> [!IMPORTANT]  
>  這個函數已被取代，您不應該使用它；僅供回溯相容性予以保留。 因此，您應該改用[Exists (MDX)](../mdx/exists-mdx.md)量值群組名稱引數的函式或[NonEmpty (MDX)](../mdx/nonempty-mdx.md)函式。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
