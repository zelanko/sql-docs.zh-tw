---
description: NonEmptyCrossjoin (MDX)
title: NonEmptyCrossjoin (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6fafaad2f6fa0f46d826bf94b26ceb6fdbe9df55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471800"
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
 **NonEmptyCrossjoin**函式會將兩個或多個集合的交叉乘積傳回為一組，但不含基礎事實資料表所提供之資料的空元組或元組。 由於 **NonEmptyCrossjoin** 函式的運作方式，因此會自動排除所有匯出成員。  
  
 如果未指定 *Count* ，函數會交叉聯結所有指定的集合，並從結果集中排除空的成員。 如果指定了集合數目，此函數就會由第一個指定的集合開始，交叉聯結指定的集合數目。 **NonEmptyCrossjoin**函式會使用後續指定集合中指定的任何其餘集合，但尚未交叉聯結的集合，可決定在產生的交叉聯結集合中，哪些成員被視為非空白。 **NonEmptyCrossjoin**函數會遵循匯出量值的**NON_EMPTY_BEHAVIOR**設定。  
  
> [!IMPORTANT]  
>  這個函數已被取代，您不應該使用它；僅供回溯相容性予以保留。 相反地，您應該搭配量值組名引數或非空白的[ (mdx) ](../mdx/nonempty-mdx.md)函數使用[ (MDX) ](../mdx/exists-mdx.md)函數。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
