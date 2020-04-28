---
title: 運算子（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2f03c3152e3144b137c079cbdfddeff5b9cd5156
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68008170"
---
# <a name="operators-dmx"></a>運算子 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  您可以使用資料採礦延伸模組（DMX）運算子，在的查詢中[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]執行算術、比較、串連和邏輯運算。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 使用運算子執行下列動作：  
  
-   搜尋符合特定條件的值或物件。  
  
-   實作值或運算式之間的決策。  
  
 DMX 使用下列區段所描述之數種類別目錄的運算子。 如需個別運算子的詳細資訊，請參閱[資料採礦延伸模組 &#40;DMX&#41; 運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)。  
  
|運算子類別目錄|運算的類型|  
|-----------------------|-----------------------|  
|[&#40;DMX&#41;的算術運算子](../dmx/operators-arithmetic.md)|執行加、減、乘或除。|  
|[&#40;DMX&#41;的比較運算子](../dmx/operators-comparison.md)|以一個值去比較另一個值或運算式。|  
|[&#40;DMX&#41;的邏輯運算子](../dmx/operators-logical.md)|測試條件的真實性，例如 AND、OR 或 NOT。|  
|[&#40;DMX&#41;的一元運算子](../dmx/operators-unary.md)|在單一運算元上執行運算。|  
  
 您可以使用運算子將 DMX 中較小的運算式結合成較複雜的運算式。 在複雜運算式中，會根據 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的運算子優先順序定義依序評估運算子。 優先順序較高的運算子會在優先順序較低的運算子之前執行。 如需運算式的詳細資訊，請參閱[&#40;DMX&#41;的運算式](../dmx/expressions-dmx.md)。  
  
 您結合簡單運算式以形成複雜運算式的時候，會結合運算子的規則與資料類型優先順序的規則來決定產生之運算式的資料類型。 如果結果是字元或 Unicode 值，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會結合運算子的規則與定序優先順序的規則，決定結果的定序。 另外也有一些規則，根據簡單運算式的有效位數、小數位數與長度，決定結果的有效位數、小數位數與長度。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41; 語法元素的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)   
 [DMX 預測查詢的結構和使用方式](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
