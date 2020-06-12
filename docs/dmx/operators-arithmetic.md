---
title: 算術運算子（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 149cd67594cac64fc8ad315b2fca9bb1cda373d5
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669310"
---
# <a name="operators---arithmetic"></a>運算子 - 算數
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  您可以使用資料採礦延伸模組（DMX）中的算術運算子進行中的算數運算 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，包括加法、減法、乘法和除法。  
  
 下表會識別 DMX 支援的算術運算子。  
  
|運算子|描述|  
|--------------|-----------------|  
|[+ &#40;新增&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|將兩個數目相加。|  
|[-&#40;減去&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|從一個數目減掉另一個數目。|  
|[&#42; &#40;乘&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|以一個數目乘上另一個數目。|  
|[&#40;除以&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|以一個數目除以另一個數目。|  
  
 下列規則決定算術運算子在 DMX 運算式中的優先順序：  
  
-   運算式中的算術運算子如果不止一個，就會先計算乘法與除法，然後再計算減法與加法。  
  
-   如果運算式中所有算術運算子的優先順序層級相同，則執行的順序是由左至右。  
  
-   括號中的運算式優先於其他所有運算。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; Operator Reference &#40;的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41; 語法元素的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;&#40;的運算式](../dmx/expressions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)   
 [DMX&#41;&#40;的運算子](../dmx/operators-dmx.md)   
 [DMX 預測查詢的結構和使用方式](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
