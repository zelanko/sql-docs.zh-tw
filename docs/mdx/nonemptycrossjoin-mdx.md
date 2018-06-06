---
title: NonEmptyCrossjoin (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5d77262ce3f6cf4f9e9cb1720d42b1bcbd85f31f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580680"
---
# <a name="nonemptycrossjoin-mdx"></a>NonEmptyCrossjoin (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 **NonEmptyCrossjoin**函式會傳回兩個或多個集合的交叉乘積所得的集合，但不含基礎事實資料表所提供的資料，排除空的 tuple。 因為如何**NonEmptyCrossjoin**函數的運作，所有導出成員會自動排除。  
  
 如果*計數*未指定，函數就會交叉聯結所有指定的集合，並從結果集排除空的成員。 如果指定了集合數目，此函數就會由第一個指定的集合開始，交叉聯結指定的集合數目。 **NonEmptyCrossjoin**函式會使用後續的指定集合中指定，但尚未進行交叉聯結以判斷哪些成員被視為非空白交叉聯結結果集中任何剩餘集。 **NonEmptyCrossjoin**函式方面**NON_EMPTY_BEHAVIOR**導出量值的設定。  
  
> [!IMPORTANT]  
>  這個函數已被取代，您不應該使用它；僅供回溯相容性予以保留。 相反地，您應該使用[Exists (MDX)](../mdx/exists-mdx.md)與量值群組名稱引數的函式或[NonEmpty (MDX)](../mdx/nonempty-mdx.md)函式。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
