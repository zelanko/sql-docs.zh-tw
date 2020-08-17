---
description: Unorder (MDX)
title: Unorder (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 192f320ebc5257f2e6829e15fc40b8144208a521
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341175"
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
 **Unorder**函式會移除任何其他函式或語句（例如[Order](../mdx/order-mdx.md)函數）所包含的元組所加諸的任何順序。 **Unorder**函數所傳回之集合中的元組順序不確定。  
  
 **Unorder**函式是用來做為查詢優化的提示，以進行 set 處理。 如果集合內的元組順序對計算或查詢不重要，使用 **Unorder** 函數可以在這類情況下提供效能優勢。 例如，如果提供給此函式的集合未排序，而不是需要保留順序，則非空白 [ (MDX) ](../mdx/nonempty-mdx.md) 函數的執行效能可能會更好 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，不過 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] ，查詢處理器會嘗試為許多函數（例如 **Sum** 和 **Aggregate**）自動執行此函數。 使用 **Unorder** 的效能優勢，只可能在由數百萬個元組組成的大型集合上感到明顯。  
  
## <a name="example"></a>範例  
 下列虛擬程式碼說明這個函數的語法。  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
