---
title: Unorder (MDX) |Microsoft 文件
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
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743447"
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
 **Unorder**函式會移除任何順序在集合中包含由函式或陳述式，例如 tuple[順序](../mdx/order-mdx.md)函式。 所傳回集合中的 tuple 順序**Unorder**函式皆不明確。  
  
 **Unorder**函式作為提示的集合處理查詢最佳化。 如果集合內的 tuple 的順序並不重要的計算或查詢，使用**Unorder**函式可提供效能優勢，在此情況下。 例如， [NonEmpty (MDX)](../mdx/nonempty-mdx.md)函式可能會進一步提供給此函式的集合沒有排序時執行比[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]需要保留順序，雖然與[!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]，查詢處理器會嘗試執行此函式會自動為許多函數，例如**總和**和**彙總**。 使用的效能優勢**Unorder**僅能展現數百萬 tuple 所組成的大型集合。  
  
## <a name="example"></a>範例  
 下列虛擬程式碼說明這個函數的語法。  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
