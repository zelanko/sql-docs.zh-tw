---
title: 比較運算子 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e3aa00334d98af02521005679174feb3b28c55f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68001519"
---
# <a name="comparison-operators"></a>比較運算子


  您可以使用比較運算子搭配純量資料。 您可以在任何多維度運算式 (MDX) 運算式中使用比較運算子。  
  
 若要檢查條件，您也可以在 MDX 語句和函數中使用比較運算子，例如 MDX [IIf](../mdx/iif-mdx.md)函數。 但是，如果您使用比較運算子檢查條件，嘗試要根據該條件來變更資料之前，請確定您已經擁有適當的權限。 只要能夠存取實際資料並可查詢該資料，任何人都可以在額外的查詢中使用比較運算子。 但這不代表這些人也必須擁有變更資料的適當權限。 此外，為了維持資料完整性，請限制有權查詢和變更資料的人數。  
  
 比較運算子會評估為布林資料類型，依照測試條件的結果而傳回 TRUE 或 FALSE。  
  
 MDX 支援下表中列出的比較運算子。  
  
|運算子|描述|  
|--------------|-----------------|  
|[= (等於)](../mdx/equal-to-mdx.md)|對於非 Null 引數，如果左邊的引數等於右邊的引數，就會傳回 TRUE；否則會傳回 FALSE。<br /><br /> 如果這兩個引數其中之一或全部都評估為 Null 值，運算子就會傳回 Null 值，除非進行比較 `0=null`，而這種情況下的布林值會包含 TRUE。|  
|[<>  （不等於）](../mdx/not-equal-to-mdx.md)|對於非 Null 引數，如果左邊的引數不等於右邊的引數，就會傳回 TRUE；否則會傳回 FALSE。<br /><br /> 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[> （大於）](../mdx/greater-than-mdx.md)|對於非 Null 引數，如果左邊的引數值大於右邊的引數值，就會傳回 TRUE；否則會傳回 FALSE。<br /><br /> 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[>= （大於或等於）](../mdx/greater-than-or-equal-to-mdx.md)|對於非 Null 引數，如果左邊的引數值大於或等於右邊的引數值，就會傳回 TRUE；否則會傳回 FALSE。<br /><br /> 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[< （小於）](../mdx/less-than-mdx.md)|對於非 null 引數，如果左邊的引數具有小於右引數的值，則會傳回 TRUE;否則為 FALSE。<br /><br /> 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[<= （小於或等於）](../mdx/less-than-or-equal-to-mdx.md)|對於非 Null 引數，如果左邊的引數值小於或等於右邊的引數值，就會傳回 TRUE；否則會傳回 FALSE。<br /><br /> 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [運算子 &#40;MDX 語法&#41;](../mdx/operators-mdx-syntax.md)  
  
  
