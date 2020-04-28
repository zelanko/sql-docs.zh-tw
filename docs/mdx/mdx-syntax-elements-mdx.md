---
title: MDX 語法元素（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 263238a0d8430928fad99042dfa0ffd06921a33b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68893327"
---
# <a name="mdx-syntax-elements-mdx"></a>MDX 語法元素 (MDX)


  多維度運算式 (MDX) 有大多數陳述式使用或受其影響的幾個語法元素：  
  
|詞彙|定義|  
|----------|----------------|  
|[識別碼](../mdx/identifiers-mdx.md)|識別碼是物件的名稱，例如 Cube、維度、成員及量值。|  
|**資料類型**|定義資料格、成員屬性及資料格屬性包含的資料類型。 MDX 只能支援 OLE VARIANT 資料類型。 如需強制型轉、轉換及操作 VARIANT 資料類型的詳細資訊，請參閱 Platform SDK 文件集中的＜VARIANT 與 VARIANTARG＞。|  
|[MDX&#41;&#40;的運算式](../mdx/expressions-mdx.md)|運算式是 Analysis Services 可以解析成單一（純量）值或物件的語法單位。 運算式包括傳回單一值、集合運算式等等的函數。|  
|[運算子](../mdx/operators-mdx-syntax.md)|運算子是語法元素，可與一個或多個簡單 MDX 運算式一起使用，構成多個複雜 MDX 運算式。|  
|[函式](../mdx/functions-mdx-syntax.md)|函數是語法元素，可接受零個、一個或多個輸入值，然後傳回純量值或物件。 範例包括用於加入數個值的[Sum](../mdx/sum-mdx.md)函數、可從維度或層級傳回成員集合的[members](../mdx/members-set-mdx.md)函數等等。|  
|[註解](../mdx/comments-mdx-syntax.md)|註解是插入 MDX 陳述式中的文字或說明陳述式用途的指令碼。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]不會執行批註。|  
|[保留關鍵字](../mdx/reserved-keywords-mdx-syntax.md)|保留關鍵字是保留起來以供 MDX 使用的單字，而且不應該在 MDX 陳述式中作為物件名稱使用。|  
|[Members, Tuples, and Sets](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx)|成員、Tuple 及集合是多維度資料的核心概念，您必須先了解此概念，然後才能著手建立 MDX 查詢。|  
  
## <a name="see-also"></a>另請參閱  
 [多維度運算式 &#40;MDX&#41 參考](../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
