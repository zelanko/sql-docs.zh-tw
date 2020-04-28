---
title: Unorder （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 954a71c8ca2e96d905892d77ff12b7270deded5f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097263"
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
 **Unorder**函數會移除任何其他函式或語句（例如[Order](../mdx/order-mdx.md)函式）包含在集合中的元組上的任何順序。 **Unorder**函數所傳回之集合中的元組順序不確定。  
  
 **Unorder**函數是用來做為設定處理之查詢優化的提示。 如果集合中的元組順序對於計算或查詢而言不重要，使用**Unorder**函數可在這種情況下提供效能優勢。 例如，當提供給這個函式的集合未排序時，非空白[（MDX）](../mdx/nonempty-mdx.md)函數的執行效能[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]可能會比需要保留順序更[!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]好，不過，查詢處理器會嘗試為許多函數（例如**Sum**和**Aggregate**）自動執行此函數。 使用**Unorder**的效能優勢，只有在由數百萬個元組組成的極大型集合上才有可能明顯。  
  
## <a name="example"></a>範例  
 下列虛擬程式碼說明這個函數的語法。  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
