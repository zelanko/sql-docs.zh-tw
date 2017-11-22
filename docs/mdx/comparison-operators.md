---
title: "比較運算子 |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: comparison operators [MDX]
ms.assetid: 4a4bbc76-c6a2-4b19-ae75-6ac3ac14df01
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 295c21b7af5c4c3d1d6b25db84e58f313f1bcc00
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="comparison-operators"></a>比較運算子
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  您可以使用比較運算子搭配純量資料。 您可以在任何多維度運算式 (MDX) 運算式中使用比較運算子。  
  
 若要檢查是否符合條件，您也可以使用比較運算子在 MDX 陳述式和函式，例如 MDX [IIf](../mdx/iif-mdx.md)函式。 但是，如果您使用比較運算子檢查條件，嘗試要根據該條件來變更資料之前，請確定您已經擁有適當的權限。 只要能夠存取實際資料並可查詢該資料，任何人都可以在額外的查詢中使用比較運算子。 但這不代表這些人也必須擁有變更資料的適當權限。 此外，為了維持資料完整性，請限制有權查詢和變更資料的人數。  
  
 比較運算子會評估為布林資料類型，依照測試條件的結果而傳回 TRUE 或 FALSE。  
  
 MDX 支援下表中列出的比較運算子。  
  
|運算子|Description|  
|--------------|-----------------|  
|[= (等於)](../mdx/equal-to-mdx.md)|對於非 Null 引數，如果左邊的引數等於右邊的引數，就會傳回 TRUE；否則會傳回 FALSE。<br /><br /> 如果這兩個引數其中之一或全部都評估為 Null 值，運算子就會傳回 Null 值，除非進行比較 `0=null`，而這種情況下的布林值會包含 TRUE。|  
|[<> (不等於)](../mdx/not-equal-to-mdx.md)|對於非 Null 引數，如果左邊的引數不等於右邊的引數，就會傳回 TRUE；否則會傳回 FALSE。<br /><br /> 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[> (大於)](../mdx/greater-than-mdx.md)|對於非 Null 引數，如果左邊的引數值大於右邊的引數值，就會傳回 TRUE；否則會傳回 FALSE。<br /><br /> 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[>= (大於或等於)](../mdx/greater-than-or-equal-to-mdx.md)|對於非 Null 引數，如果左邊的引數值大於或等於右邊的引數值，就會傳回 TRUE；否則會傳回 FALSE。<br /><br /> 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[< (小於)](../mdx/less-than-mdx.md)|對於非 Null 引數，如果左邊的引數值小於右邊的引數值，就會傳回 TRUE；否則會傳回 FALSE。<br /><br /> 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[<= (小於或等於)](../mdx/less-than-or-equal-to-mdx.md)|對於非 Null 引數，如果左邊的引數值小於或等於右邊的引數值，就會傳回 TRUE；否則會傳回 FALSE。<br /><br /> 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
  
## <a name="see-also"></a>請參閱＜  
 [MDX 運算子參考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [運算子 &#40;MDX 語法 &#41;](../mdx/operators-mdx-syntax.md)  
  
  
