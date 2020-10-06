---
description: 一般預測函數 (DMX)
title: " (DMX) 的一般預測函數 |Microsoft Docs"
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 22fe85d0e51de59d0b25b6a3eb89d29edf655ee4
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726179"
---
# <a name="general-prediction-functions-dmx"></a>一般預測函數 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  您可以在資料採礦延伸模組 (DMX) 中使用 **SELECT** 語句，以建立不同類型的查詢。 查詢可用來傳回有關採礦模型本身的資訊、進行新預測，或藉由使用新資料定型模型來改變模型 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供各種特製化函數，可控制查詢中所傳回的資訊類型。 藉由將這些函數加入至 DMX 查詢，您可以擷取其他的統計資料或資料行。 不過，每種查詢類型和模型類型都僅支援特定的函數。  
  
## <a name="common-functions"></a>一般函數  
 您可以使用函數來擴充採礦模型傳回的結果。 您可以針對任何傳回資料表運算式的 **SELECT** 語句使用下列函數：  

:::row:::
    :::column:::
        [BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)  
        [BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)  
        [Predict &#40;DMX&#41;](../dmx/predict-dmx.md)  
        [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)  
        [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)  
    :::column-end:::
    :::column:::
        [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
        [TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)  
        [TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)  
        [TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)  
    :::column-end:::
:::row-end:::

 此外，幾乎所有模型類型都支援下列函數：  
  
-   [存在於 DMX&#41;&#40;](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)  
  
-   [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)  
  
-   [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)  
  
-   [Predict &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
-   [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)  
  
-   [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)  
  
-   [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
-   [StructureColumn &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)  
  
 個別演算法可能支援其他函數。 如需每個模型類型支援的函式清單，請參閱 [資料採礦查詢](/analysis-services/data-mining/data-mining-queries)。  
  
## <a name="functions-specific-to-select-syntax"></a>SELECT 語法特定的函數  
 下表列出可用於每個 **SELECT** 語句類型的函數。  
  
 如需 DMX 中函式的一般資訊，請參閱 [&#40;dmx&#41; 函數參考中的資料採礦擴充](../dmx/data-mining-extensions-dmx-function-reference.md)功能。  
  
|查詢類型|支援的函數|備註|  
|----------------|-------------------------|-------------|  
|[SELECT DISTINCT FROM \<model>](../dmx/select-distinct-from-model-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)<br /><br /> [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)<br /><br /> [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|這些函數可用來針對包含數值資料類型的任何資料行提供最大值、最小值及平均值，不論資料行是連續的或已離散化。|  
|[SELECT FROM \<model>.CONTENT](../dmx/select-from-model-content-dmx.md)<br /><br /> 或<br /><br /> [SELECT FROM \<model>.DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|此函數會擷取模型中指定節點的子節點，舉例來說，可用來反覆運算採礦模型內容中的節點。 採礦模型內容中的節點排列相依於模型類型。 如需每個採礦模型類型之結構的相關資訊，請參閱 [&#40;Analysis Services 資料採礦&#41;的「採礦模型內容 ](/analysis-services/data-mining/mining-model-content-analysis-services-data-mining)」。<br /><br /> 如果您已將「採礦模型」內容儲存為維度，您也可以使用其他多維度運算式 (可用於查詢屬性階層的 MDX) 函數。|  
|[SELECT FROM \<model>.CASES](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)<br /><br /> [ClientSettingsGeneralFlag 類別](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)<br /><br /> [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|只有時間序列模型支援 Lag 函數。<br /><br /> 以使用維持選項建立的結構為基礎的模型支援 IsTestCase 函數，以建立測試資料集。 如果模型並非以具有鑑效組測試集的結構為基礎，則所有案例都會被視為培訓案例。|  
|[SELECT FROM \<model>.SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|在此內容中，IsInNode 函數會傳回屬於一組理想化範例案例的案例。|  
|選取 [來源] \<model> 。Pmml|不適用。 請改用 XML 查詢函數。|PMML 表示法僅可用於下列模型類型：<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹<br /><br />  群集|  
|[SELECT FROM \<model> PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)|您用來建立模型之演算法的特定預測函數。|如需每個模型類型的預測函數清單，請參閱 [資料採礦查詢](/analysis-services/data-mining/data-mining-queries)。|  
|[選取來源 \<model>](../dmx/select-from-model-dmx.md)|您用來建立模型之演算法的特定預測函數。|如需每個模型類型的預測函數清單，請參閱 [資料採礦查詢](/analysis-services/data-mining/data-mining-queries)。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;DMX&#41; 參考的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX 預測查詢的結構和使用方式](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
