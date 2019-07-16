---
title: 一般預測函數 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8eff7603fa0d0be0e90af201e524554f5e336ea8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937790"
---
# <a name="general-prediction-functions-dmx"></a>一般預測函數 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  您可以使用**選取**陳述式中的資料採礦延伸模組 (DMX) 建立不同類型的查詢。 查詢可用來傳回有關採礦模型本身的資訊、進行新預測，或藉由使用新資料定型模型來改變模型 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供各種特定函數的查詢中傳回的資訊類型。 藉由將這些函數加入至 DMX 查詢，您可以擷取其他的統計資料或資料行。 不過，每種查詢類型和模型類型都僅支援特定的函數。  
  
## <a name="common-functions"></a>一般函數  
 您可以使用函數來擴充採礦模型傳回的結果。 您可以使用下列函式的任何**選取**傳回資料表運算式的陳述式：  
  
|||  
|-|-|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|  
|[BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)|[TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)|  
|[Predict &#40;DMX&#41;](../dmx/predict-dmx.md)|[TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)|  
|[RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|[TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)||  
  
 此外，幾乎所有模型類型都支援下列函數：  
  
-   [存在&#40;DMX&#41;](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)  
  
-   [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)  
  
-   [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)  
  
-   [Predict &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
-   [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)  
  
-   [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)  
  
-   [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
-   [StructureColumn &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)  
  
 個別演算法可能支援其他函數。 如需每個模型類型所支援的函式的清單，請參閱 <<c0> [ 資料採礦查詢](../analysis-services/data-mining/data-mining-queries.md)。  
  
## <a name="functions-specific-to-select-syntax"></a>SELECT 語法特定的函數  
 下表列出您可以使用每種類型的函式**選取**陳述式。  
  
 如需在 DMX 中的函式的一般資訊，請參閱[資料採礦延伸模組&#40;DMX&#41;函式參考](../dmx/data-mining-extensions-dmx-function-reference.md)。  
  
|查詢類型|支援的函數|備註|  
|----------------|-------------------------|-------------|  
|[SELECT DISTINCT FROM\<模型 >](../dmx/select-distinct-from-model-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)<br /><br /> [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)<br /><br /> [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|這些函數可用來針對包含數值資料類型的任何資料行提供最大值、最小值及平均值，不論資料行是連續的或已離散化。|  
|[SELECT FROM\<模型 >。內容](../dmx/select-from-model-content-dmx.md)<br /><br /> 或<br /><br /> [SELECT FROM\<模型 >。DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|此函數會擷取模型中指定節點的子節點，舉例來說，可用來反覆運算採礦模型內容中的節點。 採礦模型內容中的節點排列相依於模型類型。 每個採礦模型類型結構的相關資訊，請參閱[採礦模型內容&#40;Analysis Services-Data Mining&#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)。<br /><br /> 如果已將採礦模型內容儲存為維度，則您也可以使用可用來查詢屬性階層的其他「多維度運算式」(MDX) 函數。|  
|[SELECT FROM\<模型 >。案例](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)<br /><br /> [ClientSettingsGeneralFlag 類別](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)<br /><br /> [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|Lag 函數只支援時間序列模型。<br /><br /> 建立使用鑑效組選項，來建立測試資料集的結構為基礎的模型支援，IsTestCase 函式。 如果模型並非以具有鑑效組測試集的結構為基礎，則所有案例都會被視為培訓案例。|  
|[SELECT FROM\<模型 >。SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|在此內容中，IsInNode 函式會傳回一組理想化的範例案例所屬的案例。|  
|SELECT FROM\<模型 >。PMML|不適用。 請改用 XML 查詢函數。|PMML 表示法僅可用於下列模型類型：<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] 群集|  
|[SELECT FROM\<模型 > PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)|您用來建立模型之演算法的特定預測函數。|如需每個模型類型的預測函數的清單，請參閱 <<c0> [ 資料採礦查詢](../analysis-services/data-mining/data-mining-queries.md)。|  
|[SELECT FROM\<模型 >](../dmx/select-from-model-dmx.md)|您用來建立模型之演算法的特定預測函數。|如需每個模型類型的預測函數的清單，請參閱 <<c0> [ 資料採礦查詢](../analysis-services/data-mining/data-mining-queries.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;函式參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX 預測查詢的結構和使用方式](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
