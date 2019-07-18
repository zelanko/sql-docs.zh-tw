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
manager: craigg
ms.openlocfilehash: 1a8893960b5177563ccf98dbd21cb528ce399ea3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086731"
---
# <a name="creating-a-data-mining-model"></a>建立資料採礦模型
  資料模型化是資料採礦的步驟，藉由套用建立模式和趨勢*演算法*資料。 之後就可以使用這些模式進行分析，或進行預測。  
  
 適用於 Office 的資料採礦增益集會透過精靈支援資料採礦，可讓您輕鬆建立模型。 精靈會分析資料、識別相互關聯性、計算所有變數的統計重要性，以及自動選取最佳模型。  
  
 雖然這項功能的資料採礦所提供的工具一樣強大[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]和[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、 精靈和熟悉的 Excel 介面的組合可讓您輕鬆地建立、 修改及使用資料採礦。  
  
## <a name="advanced-data-mining"></a>進階 (資料採礦)  
 進階的精靈可讓您建立新的資料採礦模型，根據資料儲存在 Excel 中，使用其中一種在資料採礦演算法[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
### <a name="create-mining-structure"></a>建立採礦結構  
 建立採礦結構精靈會協助您建立新的資料採礦結構，此結構可當做多個採礦模型的基礎。 此精靈提供選項讓您將資料的某部分擱置在一旁當做測試集使用，好讓您可以根據一致的測試標準來評估使用相同資料的所有模型。  
  
 [建立採礦結構&#40;SQL Server 資料採礦增益集&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
### <a name="add-model-to-structure"></a>將模型加入結構  
 將模型加入結構精靈讓您選擇現有的資料採礦結構，並為其建立新的資料採礦模型。 您可以將多個採礦模型加入結構中，變更參數或選擇不同的資料採礦演算法及自訂輸出。  
  
 [將模型加入結構&#40;資料採礦適用於 Excel 的增益集&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)  
  
## <a name="analyze-key-influencers-analyze"></a>分析關鍵影響因數 (分析)  
 您選擇感興趣的資料行或輸出值，然後演算法就會分析所有輸入資料以識別對目標有最大影響的因素。 或者，您可以建立會比較任何兩個值的報表，這樣就可以查看影響因數如何變更。  
  
 **分析關鍵影響因數**工具使用 Microsoft 貝氏機率分類演算法。  
  
 [分析關鍵影響因數&#40;適用於 Excel 的資料表分析工具&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
  
## <a name="associate-data-mining"></a>關聯 (資料採礦)  
 **產生關聯**精靈會建立關聯模型會偵測出現在多個交易中的項目之間的關聯： 例如，在購物籃分析。  
  
 [關聯精靈&#40;適用於 Excel 的資料採礦用戶端&#41;](associate-wizard-data-mining-client-for-excel.md)  
  
## <a name="classify-data-mining"></a>分類 (資料採礦)  
 **分類**精靈會建立分類模型，可分析構成目標結果的因素。 您可以搭配此精靈使用多種演算法，包括決策樹、貝氏機率分類與類神經網路。  
  
 [分類精靈&#40;資料採礦適用於 Excel 的增益集&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="cluster-data-mining"></a>叢集 (資料採礦)  
 **叢集**精靈會建立群集模型以偵測共用類似特性的資料列群組。 叢集 (有時稱為*區隔*) 是一種非監督式的學習的技巧，嘗試了解模式和新的資料中的群組時，是非常有用。  
  
 Microsoft 叢集演算法支援數種 K-means 和 Expectation Maximization (EM) 叢集  
  
 [叢集精靈&#40;資料採礦適用於 Excel 的增益集&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)。  
  
## <a name="detect-categories-analyze"></a>偵測類別目錄 (分析)  
 **偵測類別目錄**工具可讓您新增任何資料集和套用叢集以尋找資料的群組。 它適合用來尋找相似度及建立群組，以進一步分析。  
  
 **偵測類別目錄**」 工具採用 Microsoft 群集演算法。  
  
 [偵測類別目錄&#40;適用於 Excel 的資料表分析工具&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
## <a name="estimate-data-mining"></a>估計 (資料採礦)  
 [估計] 精靈會建立估計模型，該模型會擷取資料模式並使用樣式來預測連續的數字、日期或時間值。 此精靈使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹演算法。  
  
 [估計精靈&#40;資料採礦適用於 Excel 的增益集&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="fill-from-example-analyze"></a>根據範例填滿 (分析)  
 **根據範例填滿**工具可協助您推算遺漏值。 您要提供遺漏值應該會是什麼的一些範例，此工具就會依據資料表中的所有資料來建立模式，然後依據資料模式建議新的值。  
  
 **根據範例填滿**」 工具採用 Microsoft 羅吉斯迴歸演算法。  
  
 [根據範例填滿&#40;適用於 Excel 的資料表分析工具&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-analyze"></a>預測 (分析)  
 **預測**工具會採用隨著時間變更，然後預測未來值的資料。  
  
 **預測**」 工具採用 Microsoft 時間序列演算法。  
  
 [預測&#40;適用於 Excel 的資料表分析工具&#41;](forecast-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-data-mining"></a>預測 (資料採礦)  
 **預測**精靈會建立預測模型，偵測模式中的一連串儲存格，然後再預測其他的值。  
  
 [預測精靈&#40;資料採礦適用於 Excel 的增益集&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="highlight-exceptions-analyze"></a>反白顯示例外狀況 (分析)  
 **反白顯示例外狀況**工具會分析資料的資料表中的模式，並尋找資料列和不符合模式的值。 接著您就可以檢閱這些值並加以更正，然後重新執行模型或標記這些值以供稍後採取動作。  
  
 **反白顯示例外狀況**」 工具採用 Microsoft 群集演算法。  
  
 [反白顯示例外狀況&#40;適用於 Excel 的資料表分析工具&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
  
## <a name="prediction-calculator-analyze"></a>預測計算器 (分析)  
 此工具會建立模型以分析可導致目標結果的因數，並根據衍生自這些模式的準則來預測任何新輸入的結果。此外，它也會產生一個互動式決策工作表，讓您輕鬆地為新輸入計分。 您還可以建立計分工作表的列印版本，以供離線使用。  
  
 **預測計算器**」 工具採用 Microsoft 羅吉斯迴歸演算法。  
  
 [預測計算器&#40;適用於 Excel 的資料表分析工具&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-goal-seek-analyze"></a>案例：搜尋目標 （分析）  
 在 **搜尋目標**您工具，指定目標值，而此工具會識別必須變更為符合該目標的基礎因數。 例如，如果您知道必須增加通話滿意度 20%，就可以要求模型預測應該要變更才能達到目標的因數。  
  
 **搜尋目標**」 工具採用 Microsoft 羅吉斯迴歸演算法。  
  
 詳細資料  
  
 [搜尋目標狀況&#40;適用於 Excel 的資料表分析工具&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-what-if-scenario-analyze"></a>案例：假設狀況 （分析）  
 **模擬 Analysis**工具互補**搜尋目標**工具。 使用此工具時，您要輸入您想要變更的值，模型就會預測該變更是否足以達到所要的結果。 例如，您可以要求模型推測若額外增加一個話務員是否能將客戶滿意度提高一個積分點。  
  
 **What-if** 」 工具採用 Microsoft 羅吉斯迴歸演算法。  
  
 [假設狀況&#40;適用於 Excel 的資料表分析工具&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="shopping-basket-analysis-analyze"></a>購物籃分析 (分析)  
 **購物籃分析**工具會建立經常購買的產品群組在一起，來識別模式，可用於交叉銷售或向上銷售。 它也會根據相關產品組合的價格和成本來產生報表，以輔助您做決策。  
  
 您也可以將此工具用於經常一起發生的事件、會導致診斷的因素，或任何其他可能的原因集和結果集。  
  
 **購物籃分析**」 工具採用 Microsoft 關聯分析演算法。  
  
 [購物籃分析&#40;AnalysisTools 適用於 Excel 的資料表&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
  
## <a name="see-also"></a>另請參閱  
 [瀏覽和清除資料](exploring-and-cleaning-data.md)   
 [驗證模型及使用模型進行預測&#40;資料採礦適用於 Excel 的增益集&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [部署及調整採礦模型&#40;資料採礦適用於 Excel 的增益集&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
