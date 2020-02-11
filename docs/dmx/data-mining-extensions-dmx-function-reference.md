---
title: 資料採礦延伸模組（DMX）函數參考 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 68d57ac2db4149178a61424affef5e8948de0063
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070947"
---
# <a name="data-mining-extensions-dmx-function-reference"></a>資料採礦延伸模組 (DMX) 函數參考
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支援資料採礦延伸模組 (DMX) 語言中的數個函數。 函數會展開預測查詢的結果，以包含更深入描述預測的資訊。 函數也提供如何傳回預測結果的更多控制。 下表提供資源的連結，以協助您了解如何在 DMX 中使用函數。  
  
|函式|描述|  
|--------------|-----------------|  
|[&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)|列出可以搭配所有模型類型使用的函數，並提供關於如何查詢特定採礦模型類型之詳細資訊的連結。|  
|[DMX 預測查詢的結構和使用方式](../dmx/structure-and-usage-of-dmx-prediction-queries.md)|提供關於如何使用 DMX 建構預測查詢的概觀。|  
|[DMX&#41;的 BottomCount &#40;](../dmx/bottomcount-dmx.md)|依據次序運算式，以遞增次序順序傳回資料表，其中包含指定數目的最底部資料列。|  
  
 下表列出 DMX 支援的函數。  
  
|函式|描述|  
|--------------|-----------------|  
|[DMX&#41;的 BottomCount &#40;](../dmx/bottomcount-dmx.md)|依據次序運算式，以遞增次序順序傳回資料表，其中包含資料表運算式的最後 n 個項目資料列。|  
|[DMX&#41;的 BottomPercent &#40;](../dmx/bottompercent-dmx.md)|依據次序運算式，以遞增次序順序傳回資料表，其中包含符合指定百分比運算式之最小數目的最底部資料列。|  
|[DMX&#41;的 BottomSum &#40;](../dmx/bottomsum-dmx.md)|依據次序運算式，以遞增次序順序傳回資料表，其中包含符合指定總和運算式之最小數目的最底部資料列。|  
|[&#40;DMX&#41;的叢集](../dmx/cluster-dmx.md)|傳回最可能包含輸入案例的群集。|  
|[DMX&#41;的 ClusterProbability &#40;](../dmx/clusterprobability-dmx.md)|傳回輸入案例屬於群集的機率。|  
|[存在 &#40;DMX&#41;](../dmx/exists-dmx.md)|如果指定之 SELECT 陳述式傳回的結果集至少包含一個資料列，就會傳回 True。|  
|[DMX&#41;的 IsDescendant &#40;](../dmx/isdescendant-dmx.md)|指出目前的節點是否從指定的節點衍生。|  
|[DMX&#41;的 IsInNode &#40;](../dmx/isinnode-dmx.md)|指出指定的節點是否包含案例。|  
|[DMX&#41;的 IsTestCase &#40;](../dmx/istestcase-dmx.md)|指出某案例是否屬於測試案例集。|  
|[DMX&#41;的 IsTrainingCase &#40;](../dmx/istrainingcase-dmx.md)|指出某案例是否屬於定型案例集。|  
|[DMX&#41;的 Lag &#40;](../dmx/lag-dmx.md)|傳回目前案例之日期、與資料之最後日期之間的時間配量。|  
|[預測 &#40;DMX&#41;](../dmx/predict-dmx.md)|在指定的資料行上執行預測。|  
|[DMX&#41;的 PredictAdjustedProbability &#40;](../dmx/predictadjustedprobability-dmx.md)|傳回指定之可預測資料行的已調整機率。|  
|[DMX&#41;的 PredictAssociation &#40;](../dmx/predictassociation-dmx.md)|在資料行中，預測關聯的成員資格。|  
|[DMX&#41;的 PredictCaseLikelihood &#40;](../dmx/predictcaselikelihood-dmx.md)|傳回輸入案例符合現有模型的可能性。 此函數只能搭配群集模型使用。|  
|[&#40;DMX&#41;的 PredictHistogram](../dmx/predicthistogram-dmx.md)|傳回代表指定資料行之長條圖的資料表。|  
|[DMX&#41;的 PredictNodeId &#40;](../dmx/predictnodeid-dmx.md)|傳回選取之案例的 NodeID。|  
|[DMX&#41;的 [Predictprobability] &#40;](../dmx/predictprobability-dmx.md)|傳回指定資料行的機率。|  
|[DMX&#41;的 PredictSequence &#40;](../dmx/predictsequence-dmx.md)|預測順序中的下一個值。|  
|[DMX&#41;的 PredictStdev &#40;](../dmx/predictstdev-dmx.md)|擷取指定之資料行的標準差值。|  
|[DMX&#41;的 PredictSupport &#40;](../dmx/predictsupport-dmx.md)|傳回資料行的支援值。|  
|[DMX&#41;的 PredictTimeSeries &#40;](../dmx/predicttimeseries-dmx.md)|傳回時間序列的未來值。|  
|[DMX&#41;的 PredictVariance &#40;](../dmx/predictvariance-dmx.md)|傳回指定資料行的變異數值。|  
|[DMX&#41;的 RangeMax &#40;](../dmx/rangemax-dmx.md)|傳回針對指定離散化資料行探索之預測值區的上限數值。|  
|[DMX&#41;的 RangeMid &#40;](../dmx/rangemid-dmx.md)|傳回針對指定離散化資料行探索之預測值區的中點數值。|  
|[DMX&#41;的 RangeMin &#40;](../dmx/rangemin-dmx.md)|傳回針對指定離散化資料行探索之預測值區的下限數值。|  
|[DMX&#41;的 StructureColumn &#40;](../dmx/structurecolumn-dmx.md)|傳回指定之資料表採礦結構資料行的值。|  
|[DMX&#41;的 TopCount &#40;](../dmx/topcount-dmx.md)|依據次序運算式，以遞減次序順序傳回資料表，其中包含指定數目的最頂部資料列。|  
|[DMX&#41;的 TopPercent &#40;](../dmx/toppercent-dmx.md)|依據次序運算式，以遞減次序順序傳回資料表，其中包含符合指定百分比運算式之最小數目的最頂部資料列。|  
|[DMX&#41;的 TopSum &#40;](../dmx/topsum-dmx.md)|依據次序運算式，以遞減次序順序傳回資料表，其中包含符合指定總和運算式之最小數目的最頂部資料列。|  
  
## <a name="see-also"></a>另請參閱  
 [DMX&#41; Operator Reference &#40;的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41; 語法元素的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)   
 [DMX 預測查詢的結構和使用方式](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
