---
description: 使用方式 (DMX)
title: 使用量 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e9108fc9bc53361a15d144f1f11afa62f9d5a97
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726039"
---
# <a name="usage-dmx"></a>使用方式 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  當您使用資料採礦延伸模組 (DMX) 在中定義新的資料採礦模型時 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，您必須指定建立模型的資料採礦演算法將如何使用每個資料行。 您可以將資料行指定為下列類型其中之一：  
  
-   **索引鍵**  
  
-   **Key Sequence**  
  
-   **Key Time**  
  
-   **預測**  
  
-   **PredictOnly**  
  
 未在 DMX 中指定的資料行會當成輸入資料行處理。  
  
 若要正確地處理模型，演算法必須知道哪個資料行是唯一識別每個資料列的索引鍵資料行；如果是建立可預測模型，哪個資料行是建立預測的目標資料行；以及使用哪些資料行做為建立預測目標資料行之關聯性的輸入資料行。  
  
 指定為 **預測** 類型的資料行會當做輸入和輸出資料行使用。 以 **PredictOnly** 指定的資料行只會當做輸出資料行使用。 特定的演算法可能會以不同方式處理 Predict 資料行。  
  
 如需有關支援之資料行使用類型的詳細資訊 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，請參閱 [採礦模型資料行](/analysis-services/data-mining/mining-model-columns)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services 資料採礦&#41;](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [&#40;DMX&#41; 參考的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41;的一般預測函數 ](../dmx/general-prediction-functions-dmx.md)   
 [DMX 預測查詢的結構和使用方式](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
