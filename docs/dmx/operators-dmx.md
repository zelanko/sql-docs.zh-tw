---
title: 運算子 (DMX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- operators [DMX]
- DMX [Analysis Services], operators
- Data Mining Extensions [Analysis Services], operators
ms.assetid: e453e570-1ad1-4604-892f-6130308936ac
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: d55ce9059ddee559ae6c9d214f5a8b05457abb86
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="operators-dmx"></a>運算子 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  您可以使用資料採礦延伸模組 (DMX) 運算子在查詢中執行算術、 比較、 串連和邏輯運算[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 使用運算子執行下列動作：  
  
-   搜尋符合特定條件的值或物件。  
  
-   實作值或運算式之間的決策。  
  
 DMX 使用下列區段所描述之數種類別目錄的運算子。 如需有關個別運算子的詳細資訊，請參閱[資料採礦延伸模組&#40;DMX&#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)。  
  
|運算子類別目錄|運算的類型|  
|-----------------------|-----------------------|  
|[算術運算子&#40;DMX&#41;](../dmx/operators-arithmetic.md)|執行加、減、乘或除。|  
|[比較運算子&#40;DMX&#41;](../dmx/operators-comparison.md)|以一個值去比較另一個值或運算式。|  
|[邏輯運算子&#40;DMX&#41;](../dmx/operators-logical.md)|測試條件的真實性，例如 AND、OR 或 NOT。|  
|[一元運算子&#40;DMX&#41;](../dmx/operators-unary.md)|在單一運算元上執行運算。|  
  
 您可以使用運算子將 DMX 中較小的運算式結合成較複雜的運算式。 在複雜運算式中，會根據 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的運算子優先順序定義依序評估運算子。 優先順序較高的運算子會在優先順序較低的運算子之前執行。 如需有關運算式的詳細資訊，請參閱[運算式&#40;DMX&#41;](../dmx/expressions-dmx.md)。  
  
 您結合簡單運算式以形成複雜運算式的時候，會結合運算子的規則與資料類型優先順序的規則來決定產生之運算式的資料類型。 如果結果是字元或 Unicode 值，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會結合運算子的規則與定序優先順序的規則，決定結果的定序。 另外也有一些規則，根據簡單運算式的有效位數、小數位數與長度，決定結果的有效位數、小數位數與長度。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 & #40; DMX & #41;參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組 & #40; DMX & #41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [結構和使用方式的 DMX 預測查詢](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
