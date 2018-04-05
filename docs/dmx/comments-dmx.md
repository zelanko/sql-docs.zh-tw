---
title: 註解 (DMX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- comments [DMX]
- Data Mining Extensions [Analysis Services], comments
- double forward slashes
- commenting characters
- text strings [SQL Server]
- remarks [DMX]
- forward slash-asterisk character pairs
- DMX [Analysis Services], comments
- /*...*/ (comment)
- double hyphens
- // (comment)
- -- (comment character)
ms.assetid: 64d10eb5-4fe8-42c6-b387-eff336315e56
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 86fd2ea716fd0366149937af749c240fe01e486d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="comments-dmx"></a>註解 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  註解中的資料採礦延伸模組 (DMX) 是文字字串在程式中的程式碼的[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]不會執行。 註解也稱為備註。 您可以使用註解提供程式碼說明，或者在診斷程式碼時，暫時停用部份 DMX 陳述式或指令碼。  
  
 使用註解提供程式碼說明，未來維護程式碼會比較容易。 您可以使用註解記錄詳細資料，例如程式的名稱、撰寫程式碼的開發人員名稱，以及主要程式碼變更的日期。 您也可以使用註解描述複雜的計算或設計方法的程式。  
  
 下列是撰寫註解的基本指導方針：  
  
-   您可以在註解中使用任何英數字元或符號。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會忽略註解中的所有字元。  
  
-   陳述式或指令碼中的註解並無長度上限。 一個註解可以由一或多行組成。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支援下列註解字元類型：  
  
-   **（雙斜線）。** 使用這些註解字元在要執行之程式碼的同一行撰寫註解，或者在單獨一行撰寫註解。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會將雙斜線開始到該行結束的所有內容評估為註解的一部分。 若要建立多行註解，請在註解的每一行開頭使用雙斜線。 如需有關這個註解字元的詳細資訊，請參閱[雙斜線 &#40;註解 &#41;&#40; DMX &#41;](../dmx/double-slash-comment-dmx.md).  
  
-   **-（雙連字號）。** 使用這些註解字元在要執行之程式碼的同一行撰寫註解，或者在單獨一行撰寫註解。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會將雙連字號開始到該行結束的所有內容評估為註解的一部分。 若要建立多行註解，請在註解的每一行開頭使用雙連字號。 如需有關這個註解字元的詳細資訊，請參閱[-&#40;註解 &#41;&#40; DMX &#41;摘要](../dmx/comment-dmx-summary.md)。  
  
-   **/\*...\*/ （正斜線-星號字元配對）。** 使用這些註解字元在要執行之程式碼的同一行撰寫註解，或者單獨一行撰寫註解，甚至在可執行程式碼中撰寫註解。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]評估所有內容都將開啟註解配對 (/ *) 到關閉註解配對 (\*/) 做為註解的一部分。 若要建立多行註解，開始註解的註解字元配對 (/\*)，且結尾註解與關閉註解字元配對 (\*/)。 任一行註解中不應包含其他任何註解字元。 如需有關這個註解字元的詳細資訊，請參閱[斜線星狀 &#40;註解 &#41;&#40; DMX &#41;](../dmx/slash-star-comment-dmx.md).  
  
## <a name="see-also"></a>請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40; DMX &#41;語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [資料採礦延伸模組 &#40; DMX &#41;語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [結構和使用方式的 DMX 預測查詢](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
