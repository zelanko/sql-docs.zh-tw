---
title: "資料採礦延伸模組 (DMX) 運算子參考 |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- operators [DMX]
- DMX [Analysis Services], operators
- Data Mining Extensions [Analysis Services], operators
ms.assetid: a6d747c0-9ff0-475f-86cd-34bebd79c21a
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d4958e829a3b857d9aff25dff8d38e49b88f9b3c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="data-mining-extensions-dmx-operator-reference"></a>資料採礦延伸模組 (DMX) 運算子參考
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  中的資料採礦延伸模組 (DMX) 語言[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]支援算術、 指派、 比較、 邏輯及一元運算子。 下表會列出 DMX 支援的運算子。  
  
|運算子|Description|  
|--------------|-----------------|  
|[+ &#40;新增 &#41;&#40; DMX &#41;](../dmx/add-dmx.md)|將兩個數目相加的算術運算子。|  
|[-&#40;減去 &#41;&#40; DMX &#41;](../dmx/subtract-dmx.md)|從一個數目減掉另一個數目的算術運算子。|  
|[&#42;&#40;Multiply &#41;&#40; DMX &#41;](../dmx/multiply-dmx.md)|將一個數目乘上另一個數目的算術運算子。|  
|[&#40; 除以 &#41;&#40; DMX &#41;](../dmx/divide-dmx.md)|將一個數目除以另一個數目的算術運算子。|  
|[&#60;&#40;小於 &#41;&#40; DMX &#41;](../dmx/less-than-dmx.md)|比較運算子。 針對評估為非 Null 值的引數，如果左邊的引數值小於右邊的引數值，傳回 TRUE；否則傳回 FALSE。 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[&#62;&#40;大於 &#41;&#40; DMX &#41;](../dmx/greater-than-dmx.md)|比較運算子。 針對評估為非 Null 值的引數，如果左邊的引數值大於右邊的引數值，傳回 TRUE；否則傳回 FALSE。 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[= &#40;等於 &#41;&#40; DMX &#41;](../dmx/equal-to-dmx.md)|比較運算子。 針對評估為非 Null 值的引數，如果左邊的引數值等於右邊的引數值，傳回 TRUE；否則傳回 FALSE。 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[&#60; &#62;&#40;不等於 &#41;&#40; DMX &#41;](../dmx/not-equal-to-dmx.md)|比較運算子。 針對評估為非 Null 值的引數，如果左邊的引數值不等於右邊的引數值，傳回 TRUE；否則傳回 FALSE。 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[&#60; = &#40;小於或等於 &#41;&#40; DMX &#41;](../dmx/less-than-or-equal-to-dmx.md)|比較運算子。 針對評估為非 Null 值的引數，如果左邊的引數值小於或等於右邊的引數值，傳回 TRUE；否則傳回 FALSE。 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[&#62; = &#40;大於或等於 &#41;&#40; DMX &#41;](../dmx/greater-than-or-equal-to-dmx.md)|比較運算子。 針對評估為非 Null 值的引數，如果左邊的引數值大於或等於右邊的引數值，傳回 TRUE；否則傳回 FALSE。 如果任一個引數或兩個引數都評估為 Null 值，則運算子會傳回 Null 值。|  
|[和 &#40; DMX &#41;](../dmx/and-dmx.md)|在兩個數值運算式上執行結合的邏輯運算子。|  
|[不 &#40; DMX &#41;](../dmx/not-dmx.md)|在數值運算式上執行否定的邏輯運算子。|  
|[或者 &#40; DMX &#41;](../dmx/or-dmx.md)|在兩個數值運算式上執行分離的邏輯運算子。|  
|[+ &#40;正 &#41;&#40; DMX &#41;](../dmx/positive-dmx.md)|傳回數值運算式之正值的一元運算子。|  
|[-&#40;負數 &#41;&#40; DMX &#41;](../dmx/negative-dmx.md)|傳回數值運算式之負值的一元運算子。|  
|[雙斜線 &#40;註解 &#41;&#40; DMX &#41;](../dmx/double-slash-comment-dmx.md)|指出 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不應執行的文字字串。 您可以在 DMX 陳述式內巢狀註解、在程式碼行的尾端包含註解，或者將註解插入單獨的一行。|  
|[-&#40;註解 &#41;&#40; DMX &#41;摘要](../dmx/comment-dmx-summary.md)|指出 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不應執行的文字字串。 您可以在 DMX 陳述式內巢狀註解、在程式碼行的尾端包含註解，或者將註解插入單獨的一行。|  
|[斜線星狀 &#40;註解 &#41;&#40; DMX &#41;](../dmx/slash-star-comment-dmx.md)|指出 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不應執行的文字字串。 您可以在 DMX 陳述式內巢狀註解、在程式碼行的尾端包含註解，或者將註解插入單獨的一行。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40; DMX &#41;語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [資料採礦延伸模組 &#40; DMX &#41;語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [運算子 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

