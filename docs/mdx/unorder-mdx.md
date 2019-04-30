---
title: Unorder (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3b5e360c8f15eafba2b4565ca41a557c9e1ceda9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63297919"
---
# <a name="unorder-mdx"></a>Unorder (MDX)


  移除指定集合中的任何強制排序。  
  
## <a name="syntax"></a>語法  
  
```  
  
Unorder(Set_Expression)   
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **Unorder**函式會移除任何順序在集合中包含的任何其他函式或陳述式，這類 tuple[順序](../mdx/order-mdx.md)函式。 排序所傳回集合中 tuple **Unorder**函式為不定。  
  
 **Unorder**函式用於以做為提示的集合處理的查詢最佳化。 如果集合內的 tuple 順序在計算或查詢並不重要，使用**Unorder**函式可提供在此情況下提升效能。 例如， [NonEmpty (MDX)](../mdx/nonempty-mdx.md)函式可能會進一步提供給此函式的集合沒有排序時執行比[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]需要保留順序，雖然使用[!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]，查詢處理器會嘗試執行這個函式會自動供許多函式，例如**總和**並**彙總**。 使用的效能優勢**Unorder**僅能展現數百萬 tuple 所組成的大型集合。  
  
## <a name="example"></a>範例  
 下列虛擬程式碼說明這個函數的語法。  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
