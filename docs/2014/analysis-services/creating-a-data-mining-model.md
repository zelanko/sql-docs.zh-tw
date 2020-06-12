---
title: 建立資料採礦模型 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining models, creating
- forecasting [data mining]
- mining models, creating
- clustering [data mining]
- association [data mining]
- data modeling [data mining]
- estimation
- classification [data mining]
ms.assetid: 804b7db3-1f6a-4f73-a81d-bbe02520d7c6
author: minewiskan
ms.author: owend
ms.openlocfilehash: cce03fab2757b366fbe67dc6c68cb3be1c075e3c
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526427"
---
# <a name="creating-a-data-mining-model"></a>建立資料採礦模型
  資料模型化是資料採礦的步驟，可讓您將*演算法*套用至資料，以建立模式和趨勢。 之後就可以使用這些模式進行分析，或進行預測。  
  
 適用於 Office 的資料採礦增益集會透過精靈支援資料採礦，可讓您輕鬆建立模型。 精靈會分析資料、識別相互關聯性、計算所有變數的統計重要性，以及自動選取最佳模型。  
  
 雖然這項功能與和所提供的資料採礦工具一樣強大，但結合了和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 熟悉的 Excel 介面，讓您可以輕鬆地建立、修改和使用資料採礦。  
  
## <a name="advanced-data-mining"></a>進階 (資料採礦)  
 「高級」程式可讓您使用中的其中一種資料採礦演算法，根據儲存在 Excel 中的資料，建立新的資料採礦模型 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。  
  
### <a name="create-mining-structure"></a>建立採礦結構  
 建立採礦結構精靈會協助您建立新的資料採礦結構，此結構可當做多個採礦模型的基礎。 此精靈提供選項讓您將資料的某部分擱置在一旁當做測試集使用，好讓您可以根據一致的測試標準來評估使用相同資料的所有模型。  
  
 [建立 &#40;SQL Server 資料採礦增益集的採礦結構&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
### <a name="add-model-to-structure"></a>將模型加入結構  
 將模型加入結構精靈讓您選擇現有的資料採礦結構，並為其建立新的資料採礦模型。 您可以將多個採礦模型加入結構中，變更參數或選擇不同的資料採礦演算法及自訂輸出。  
  
 [將模型加入結構 &#40;適用于 Excel 的資料採礦增益集&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)  
  
## <a name="analyze-key-influencers-analyze"></a>分析關鍵影響因數 (分析)  
 您選擇感興趣的資料行或輸出值，然後演算法就會分析所有輸入資料以識別對目標有最大影響的因素。 或者，您可以建立會比較任何兩個值的報表，這樣就可以查看影響因數如何變更。  
  
 [**分析關鍵影響**因數] 工具會使用 Microsoft 的簡單貝氏機率分類演算法。  
  
 [&#40;適用于 Excel 的資料表分析工具分析關鍵影響因數&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
  
## <a name="associate-data-mining"></a>關聯 (資料採礦)  
 [**關聯**] 嚮導會建立關聯模型，以偵測出現在多筆交易中之專案之間的關聯：例如，在購物籃分析中。  
  
 [&#40;適用于 Excel&#41;的資料採礦用戶端相關聯的 Wizard](associate-wizard-data-mining-client-for-excel.md)  
  
## <a name="classify-data-mining"></a>分類 (資料採礦)  
 **分類**嚮導會建立分類模型，以分析提供給目標結果的因素。 您可以搭配此精靈使用多種演算法，包括決策樹、貝氏機率分類與類神經網路。  
  
 [適用于 Excel 的資料採礦增益集&#41;的分類嚮導 &#40;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="cluster-data-mining"></a>叢集 (資料採礦)  
 叢集**嚮導會**建立叢集模型，以偵測共用相似特性的資料列群組。 群集（有時稱為*分割*）是一種不受監督學習技術，在嘗試瞭解新資料的模式和群組時非常有用。  
  
 Microsoft 叢集演算法支援數種 K-means 和 Expectation Maximization (EM) 叢集  
  
 [Cluster Wizard &#40;適用于 Excel&#41;的資料採礦增益集](cluster-wizard-data-mining-add-ins-for-excel.md)。  
  
## <a name="detect-categories-analyze"></a>偵測類別目錄 (分析)  
 [偵測**類別目錄**] 工具可讓您新增任何資料集，並套用叢集以尋找資料的群組。 這適用于尋找相似之處，以及建立群組以進一步分析。  
  
 [偵測**類別目錄**] 工具會使用 Microsoft 群集演算法。  
  
 [偵測適用于 Excel&#41;&#40;資料表分析工具的分類](detect-categories-table-analysis-tools-for-excel.md)  
  
## <a name="estimate-data-mining"></a>估計 (資料採礦)  
 [估計] 精靈會建立估計模型，該模型會擷取資料模式並使用樣式來預測連續的數字、日期或時間值。 此精靈使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹演算法。  
  
 [評估 Wizard &#40;適用于 Excel 的資料採礦增益集&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="fill-from-example-analyze"></a>根據範例填滿 (分析)  
 [**根據範例填滿**] 工具可協助您插補遺漏值。 您要提供遺漏值應該會是什麼的一些範例，此工具就會依據資料表中的所有資料來建立模式，然後依據資料模式建議新的值。  
  
 [**根據範例填滿**] 工具會使用 Microsoft 羅吉斯回歸演算法。  
  
 [&#40;適用于 Excel 的資料表分析工具&#41;的範例填滿](fill-from-example-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-analyze"></a>預測 (分析)  
 「**預測**」工具會採用隨著時間而變更的資料，並預測未來的值。  
  
 「**預測**」工具會使用 Microsoft 時間序列演算法。  
  
 [適用于 Excel&#41;的預測 &#40;資料表分析工具](forecast-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-data-mining"></a>預測 (資料採礦)  
 「**預測**」 wizard 會建立一個預測模型，它會偵測一系列資料格中的模式，然後再預測其他的值。  
  
 [&#40;適用于 Excel 的資料採礦增益集&#41;的預測 Wizard](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="highlight-exceptions-analyze"></a>反白顯示例外狀況 (分析)  
 [**反白顯示例外**狀況] 工具會分析資料表中的模式，並尋找不符合模式的資料列和值。 接著您就可以檢閱這些值並加以更正，然後重新執行模型或標記這些值以供稍後採取動作。  
  
 [**反白顯示例外**狀況] 工具會使用 Microsoft 群集演算法。  
  
 [反白顯示 &#40;適用于 Excel 的資料表分析工具的例外狀況&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
  
## <a name="prediction-calculator-analyze"></a>預測計算器 (分析)  
 此工具會建立模型以分析可導致目標結果的因數，並根據衍生自這些模式的準則來預測任何新輸入的結果。此外，它也會產生一個互動式決策工作表，讓您輕鬆地為新輸入計分。 您還可以建立計分工作表的列印版本，以供離線使用。  
  
 **預測計算器**工具會使用 Microsoft 羅吉斯回歸演算法。  
  
 [預測計算器 &#40;適用于 Excel 的資料表分析工具&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-goal-seek-analyze"></a>狀況：搜尋目標 (分析)  
 在 [**搜尋目標**] 工具中，您可以指定目標值，而此工具會識別必須變更以符合該目標的基礎因數。 例如，如果您知道必須增加通話滿意度 20%，就可以要求模型預測應該要變更才能達到目標的因數。  
  
 [**搜尋目標**] 工具使用 Microsoft 羅吉斯回歸演算法。  
  
 詳細資料  
  
 [&#40;適用于 Excel&#41;的資料表分析工具的目標搜尋案例](goal-seek-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-what-if-scenario-analyze"></a>狀況：假設狀況 (分析)  
 [**假設分析**] 工具會補充 [**搜尋目標**] 工具。 使用此工具時，您要輸入您想要變更的值，模型就會預測該變更是否足以達到所要的結果。 例如，您可以要求模型推測若額外增加一個話務員是否能將客戶滿意度提高一個積分點。  
  
 **假設**工具會使用 Microsoft 羅吉斯回歸演算法。  
  
 [適用于 Excel 的資料表分析工具 &#40;假設案例&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="shopping-basket-analysis-analyze"></a>購物籃分析 (分析)  
 [**購物籃分析**] 工具會建立經常一起購買的產品群組，以識別可用於交叉銷售或向上銷售的模式。 它也會根據相關產品組合的價格和成本來產生報表，以輔助您做決策。  
  
 您也可以將此工具用於經常一起發生的事件、會導致診斷的因素，或任何其他可能的原因集和結果集。  
  
 [**購物籃分析**] 工具使用 Microsoft 關聯演算法。  
  
 [適用于 Excel&#41;的購物籃分析 &#40;資料表 AnalysisTools](shopping-basket-analysis-table-analysistools-for-excel.md)  
  
## <a name="see-also"></a>另請參閱  
 [探索和清除資料](exploring-and-cleaning-data.md)   
 [驗證模型及使用模型進行預測 &#40;適用于 Excel 的資料採礦增益集&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [&#40;適用于 Excel 的資料採礦增益集部署和調整採礦模型&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
