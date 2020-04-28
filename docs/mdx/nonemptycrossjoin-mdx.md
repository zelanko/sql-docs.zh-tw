---
title: NonEmptyCrossjoin （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2d152b51e0c1c996e0bb3309e554a70683937493
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68088348"
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
  
 *Count*  
 有效的數值運算式，會指定要傳回的集合數目。  
  
## <a name="remarks"></a>備註  
 **NonEmptyCrossjoin**函數會傳回兩個或多個集合的交叉乘積做為集合，但不包括空的元組或元組，而不包含基礎事實資料表所提供的資料。 由於**NonEmptyCrossjoin**函數的運作方式，會自動排除所有匯出成員。  
  
 如果未指定*Count* ，函數會交叉聯結所有指定的集合，並從結果集排除空的成員。 如果指定了集合數目，此函數就會由第一個指定的集合開始，交叉聯結指定的集合數目。 **NonEmptyCrossjoin**函數會使用後續指定集合中指定的任何剩餘集合，但尚未交叉聯結，以判斷產生的交叉聯結集合中哪些成員被視為非空白。 **NonEmptyCrossjoin**函數會遵循匯出量值的**NON_EMPTY_BEHAVIOR**設定。  
  
> [!IMPORTANT]  
>  這個函數已被取代，您不應該使用它；僅供回溯相容性予以保留。 相反地，您應該使用[Exists （MDX）](../mdx/exists-mdx.md)函數搭配量值組名引數或非[空的（mdx）](../mdx/nonempty-mdx.md)函數。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
