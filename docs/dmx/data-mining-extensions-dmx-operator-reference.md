---
title: 資料採礦延伸模組 (DMX) 運算子參考 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7a85644328591f037ee342866ca7dfb5e887ed17
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38006830"
---
# <a name="data-mining-extensions-dmx-operator-reference"></a>資料採礦延伸模組 (DMX) 運算子參考
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  中的資料採礦延伸模組 (DMX) 語言[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]支援算術、 指派、 比較、 邏輯及一元運算子。 下表會列出 DMX 支援的運算子。  
  
|運算子|描述|  
|--------------|-----------------|  
|[+&#40;新增&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|將兩個數目相加的算術運算子。|  
|[-&#40;減去&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|從一個數目減掉另一個數目的算術運算子。|  
|[&#42;&#40;乘以&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|將一個數目乘上另一個數目的算術運算子。|  
|[&#40;將&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|將一個數目除以另一個數目的算術運算子。|  
|[&#60;&#40;小於&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|比較運算子。 針對評估為非 Null 值的引數，如果左邊的引數值小於右邊的引數值，傳回 TRUE；否則傳回 FALSE。 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[&#62;&#40;大於&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|比較運算子。 針對評估為非 Null 值的引數，如果左邊的引數值大於右邊的引數值，傳回 TRUE；否則傳回 FALSE。 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[=&#40;等於&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|比較運算子。 針對評估為非 Null 值的引數，如果左邊的引數值等於右邊的引數值，傳回 TRUE；否則傳回 FALSE。 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[&#60;&#62;&#40;不等於&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|比較運算子。 針對評估為非 Null 值的引數，如果左邊的引數值不等於右邊的引數值，傳回 TRUE；否則傳回 FALSE。 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[&#60;=&#40;小於或等於&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|比較運算子。 針對評估為非 Null 值的引數，如果左邊的引數值小於或等於右邊的引數值，傳回 TRUE；否則傳回 FALSE。 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[&#62;=&#40;大於或等於&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|比較運算子。 針對評估為非 Null 值的引數，如果左邊的引數值大於或等於右邊的引數值，傳回 TRUE；否則傳回 FALSE。 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[和&AMP;#40;DMX&AMP;#41;](../dmx/and-dmx.md)|在兩個數值運算式上執行結合的邏輯運算子。|  
|[不&AMP;#40;DMX&AMP;#41;](../dmx/not-dmx.md)|在數值運算式上執行否定的邏輯運算子。|  
|[或者&AMP;#40;DMX&AMP;#41;](../dmx/or-dmx.md)|在兩個數值運算式上執行分離的邏輯運算子。|  
|[+&#40;正&#41; &#40;DMX&#41;](../dmx/positive-dmx.md)|傳回數值運算式之正值的一元運算子。|  
|[-&#40;負數&#41; &#40;DMX&#41;](../dmx/negative-dmx.md)|傳回數值運算式之負值的一元運算子。|  
|[雙斜線&#40;註解&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)|指出 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不應執行的文字字串。 您可以在 DMX 陳述式內巢狀註解、在程式碼行的尾端包含註解，或者將註解插入單獨的一行。|  
|[-&#40;註解&#41; &#40;DMX&#41;摘要](../dmx/comment-dmx-summary.md)|指出 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不應執行的文字字串。 您可以在 DMX 陳述式內巢狀註解、在程式碼行的尾端包含註解，或者將註解插入單獨的一行。|  
|[斜線星形&#40;註解&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)|指出 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不應執行的文字字串。 您可以在 DMX 陳述式內巢狀註解、在程式碼行的尾端包含註解，或者將註解插入單獨的一行。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;函式參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [運算子&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
