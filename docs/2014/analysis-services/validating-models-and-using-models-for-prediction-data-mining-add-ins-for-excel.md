---
title: 驗證模型及使用模型進行預測（適用于 Excel 的資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- mining models, charting
- validation [data mining]
- mining models, testing
ms.assetid: e245ac1f-1230-48e9-9091-e70b131aa2a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97268dac1fef029bc35ff702ace0d422ee296d65
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66065495"
---
# <a name="validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel"></a>驗證模型及使用模型進行預測 (適用於 Excel 的資料採礦增益集)
  測試並驗證模型是資料採礦處理中的一個重要步驟。 在將模型部署到實際環境之前，您必須了解採礦模型對實際資料的執行效能有多好。  
  
 資料採礦增益集所包含的工具可協助您測試您所建立的模型，以及使用模型來建立預測和建議。  
  
## <a name="accuracy-chart"></a>精確度圖表  
 **精確度圖表**wizard 可協助您建立預測查詢，並藉由建立增益圖或散佈圖來評估資料採礦模型的效能。 增益圖有助於將結構中幾乎相同的模型加以區分，以協助您判斷哪一個模型的預測能力最佳。  
  
 [精確度圖表 &#40;SQL Server 資料採礦增益集&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
## <a name="classification-matrix"></a>分類矩陣  
 [**分類矩陣**] wizard 可協助您建立預測查詢，以評估分類模型的效能。 其輸出是描述由模型所做之精確與不精確預測的摘要圖表。 矩陣是重要的工具，因為它不僅會顯示模型正確地預測值的頻率，也會顯示模型最常預測錯誤的值。  
  
 [SQL Server 資料採礦增益集的分類矩陣 &#40;&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
## <a name="profit-chart"></a>收益圖  
 **收益圖**wizard 可協助您衡量使用資料採礦模型的優點，並評估誤報和誤否定的成本  
  
 此圖表類型會測量模型的預測精確度，並併入您指定的單位和總成本。  
  
 [收益圖 &#40;SQL Server 資料採礦增益集&#41;](profit-chart-sql-server-data-mining-add-ins.md)。  
  
## <a name="cross-validation"></a>交叉驗證  
 交叉驗證是資料採礦社群中早已建立的技術，用於評估資料集的有效性以及該資料集的採礦模型的精確度。 它會將資料集分割為子集，然後反覆地建立、定型及測試每個子集的模型。  
  
 **交叉驗證**嚮導可讓您指定用來分割資料的折迭數目，然後提供交叉驗證報表，以統計方式描述這些交叉區段之間的差異。 根據此報表，您可以判斷模型是否在所有定型資料上都順利執行，或者可能對特定子集有所偏差。  
  
 [SQL Server 資料採礦增益集的交叉驗證 &#40;&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
  
## <a name="query-wizard"></a>查詢精靈  
 **查詢**嚮導是一種互動式工具，可協助您建立預測查詢。 查詢是用來產生建議、未來預測等等的方式。  
  
 在 [**查詢**嚮導] 中，您可以挑選模型，然後提供輸入資料做為單一值或從資料表或範圍中取得，而 wizard 可協助您選取要輸出的資料行。 您也可以將函數加入至查詢，以產生機率分數和其他有用的統計資料。  
  
 [查詢 &#40;SQL Server 資料採礦增益集&#41;](query-sql-server-data-mining-add-ins.md)  
  
## <a name="advanced-query-editor"></a>進階查詢編輯器  
 「**高級查詢編輯器**」是一組互動式的對話方塊，可協助您建立各種 DMX 語句、執行自訂查詢來建立和定型新模型、刪除模型，或建立新的資料集。  
  
 [進階資料採礦查詢編輯器](advanced-data-mining-query-editor.md)  
  
## <a name="see-also"></a>另請參閱  
 [探索和清除資料](exploring-and-cleaning-data.md)   
 [建立資料採礦模型](creating-a-data-mining-model.md)   
 [&#40;適用于 Excel 的資料採礦增益集部署和調整採礦模型&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
