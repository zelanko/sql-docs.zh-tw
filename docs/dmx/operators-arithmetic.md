---
title: "算術運算子 (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- arithmetic operators
ms.assetid: befe4f0c-e5dd-4ae1-b88e-6ac7aab2181a
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 032f285a3f9df3f63f85ad7b2e01122f25964dd3
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="operators---arithmetic"></a>運算子的算術運算
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  您可以使用算術運算子在資料採礦延伸模組 (DMX) 中的算術計算[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，包括加法、 減法、 乘法和除法。  
  
 下表會識別 DMX 支援的算術運算子。  
  
|運算子|Description|  
|--------------|-----------------|  
|[+ &#40;新增 &#41;&#40; DMX &#41;](../dmx/add-dmx.md)|將兩個數目相加。|  
|[-&#40;減去 &#41;&#40; DMX &#41;](../dmx/subtract-dmx.md)|從一個數目減掉另一個數目。|  
|[&#42;&#40;Multiply &#41;&#40; DMX &#41;](../dmx/multiply-dmx.md)|以一個數目乘上另一個數目。|  
|[&#40; 除以 &#41;&#40; DMX &#41;](../dmx/divide-dmx.md)|以一個數目除以另一個數目。|  
  
 下列規則決定算術運算子在 DMX 運算式中的優先順序：  
  
-   運算式中的算術運算子如果不止一個，就會先計算乘法與除法，然後再計算減法與加法。  
  
-   如果運算式中所有算術運算子的優先順序層級相同，則執行的順序是由左至右。  
  
-   括號中的運算式優先於其他所有運算。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40; DMX &#41;語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [資料採礦延伸模組 &#40; DMX &#41;語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [運算式 &#40; DMX &#41;](../dmx/expressions-dmx.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [運算子 &#40; DMX &#41;](../dmx/operators-dmx.md)   
 [結構和使用方式的 DMX 預測查詢](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  

