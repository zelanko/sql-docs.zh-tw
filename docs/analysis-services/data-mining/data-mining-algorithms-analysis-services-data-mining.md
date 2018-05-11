---
title: 資料採礦演算法 (Analysis Services-資料採礦) |Microsoft 文件
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: abe09c03977d5002636b14d674ed5a0167b2c672
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="data-mining-algorithms-analysis-services---data-mining"></a>資料採礦演算法 (Analysis Services - 資料採礦)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  資料採礦中的「演算法」(或機器學習服務) 是一組可從資料建立模型的啟發學習法和計算。 若要建立模型，演算法首先會分析您提供的資料，尋找特定模式和趨勢類型。 此演算法會使用此分析的結果進行反覆運算，以尋找建立採礦模型的最佳參數。 然後這些參數會套用到整個資料集以擷取可付諸行動的模式與詳細的統計資料。  
  
 演算法從資料建立的採礦模型可以有各種形式，包括：  
  
-   一組叢集，描述資料集的案例如何相關。  
  
-   決策樹，預測結果並描述不同準則如何影響該結果。  
  
-   預測銷售的數學模型。  
  
-   一組規則，描述交易中的產品及購買產品的機率如何群組在一起。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦中提供的演算法，是資料中最受歡迎、研究最透徹之衍生模式的方法。 舉例而言，K-means 叢集是其中一種最舊的群集演算法，而且可廣泛地在許多不同的工具中使用，並具有許多不同的實作與選項。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦中使用的 K-means 叢集特定實作是由 Microsoft Research 所開發，並且使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]來最佳化效能。 所有的 Microsoft 資料採礦演算法可以使用提供的 API 廣泛地自訂，而且為完整可程式化。 您也可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中的資料採礦元件，來自動化模型的建立、定型和重新定型。  
  
 您也可以使用符合 OLE DB for Data Mining 規格的協力廠商演算法，或開發可註冊為服務，然後用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦架構中的自訂演算法。  
  
## <a name="choosing-the-right-algorithm"></a>選擇正確的演算法  
 選擇特定分析工作最適用的演算法並不容易。 您可以使用不同的演算法來執行相同的業務工作，每一個演算法會產生不同的結果，且部分演算法還會產生一種以上的結果類型。 例如，您可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法，不僅用來預測也可以減少資料集內的資料行數目，因為決策樹可以識別不影響最終採礦模型的資料行。  
  
### <a name="choosing-an-algorithm-by-type"></a>依類型選擇演算法  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦包括下列演算法類型：  
  
-   **分類演算法** 會根據資料集內的其他屬性，預測一或多個離散變數。  
  
-   **迴歸演算法** ：會根據資料集內的其他屬性，預測一或多個連續數值變數，例如利潤或損失。  
  
-   **分割演算法** ：會將項目的資料劃分為具有相似屬性的群組或叢集。  
  
-   **關聯分析演算法** 會尋找資料集內不同屬性之間的相互關聯。 這種演算法最常應用在建立關聯規則，這些規則可以用在購物籃分析。  
  
-   **時序分析演算法** ：會對資料中的時序或事件進行摘要，例如網站中的一系列點擊，或在機器維護之前的一系列記錄事件。  
  
 不過，沒有任何理由限制您在方案中只能使用一種演算法。 有經驗的分析師有時會使用一種演算法來決定最有效的輸入 (亦即變數)，然後套用不同演算法，以根據該資料預測特定結果。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦可讓您根據單一採礦結構建立多種模型，因此在單一資料採礦方案內，您可以使用叢集演算法、決策樹模型及貝氏機率分類模型，來取得不同的資料檢視。 您也可以在一個方案內使用多種演算法來執行個別的工作：例如，您可以使用迴歸來取得財務預測，以及使用類神經網路演算法來執行影響預測之因素的分析。  
  
### <a name="choosing-an-algorithm-by-task"></a>依工作選擇演算法  
 為了協助您選取搭配特定工作所使用的演算法，下表提供每種演算法傳統上使用的工作類型建議。  
  
|工作範例|適用的 Microsoft 演算法|  
|-----------------------|---------------------------------|  
|**預測離散屬性：**<br /><br /> 將潛在買家清單中的客戶標幟為較佳或較差的潛在客戶。<br /><br /> 計算伺服器在未來 6 個月內失敗的機率。<br /><br /> 分類病人結果並探索相關因素。|[Microsoft 決策樹演算法](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft 貝氏機率分類演算法](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)<br /><br /> [Microsoft 群集演算法](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Microsoft 類神經網路演算法](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)|  
|**預測連續屬性：**<br /><br /> 預測下一個年度的銷售。<br /><br /> 根據過去歷史和季節性趨勢來預測網站訪客。<br /><br /> 根據人口統計產生風險分數。|[Microsoft 決策樹演算法](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft 時間序列演算法](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)<br /><br /> [Microsoft 線性迴歸演算法](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)|  
|**預測順序：**<br /><br /> 執行公司網站的點選流分析。<br /><br /> 分析導致伺服器失敗的因素。<br /><br /> 擷取及分析看診期間的活動順序，制定出以一般活動為主的最佳作法。|[Microsoft 時序群集演算法](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)|  
|**在交易中尋找通用項目的群組：**<br /><br /> 使用購物籃分析來決定產品位置。<br /><br /> 向客戶建議其他可購買的產品。<br /><br /> 分析參加某事件之訪客的調查資料，以找出相互關聯的活動或攤位，並規劃未來的活動。|[Microsoft 關聯分析演算法](../../analysis-services/data-mining/microsoft-association-algorithm.md)<br /><br /> [Microsoft 決策樹演算法](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)|  
|**尋找相似項目的群組：**<br /><br /> 根據人口統計和行為等屬性，建立病患風險評估群組。<br /><br /> 依瀏覽及購買模式來分析使用者。<br /><br /> 識別具有類似使用特性的伺服器。|[Microsoft 群集演算法](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Microsoft 時序群集演算法](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)|  
  
## <a name="related-content"></a>相關內容  
 下表提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦隨附之每種資料採礦演算法的學習資源連結：  
  
|||  
|-|-|  
|**基本演算法描述**|說明演算法的用途與運作方式，並概要說明演算法可能相當實用的商務案例。|  
||[Microsoft 關聯分析演算法](../../analysis-services/data-mining/microsoft-association-algorithm.md)<br /><br /> [Microsoft 群集演算法](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Microsoft 決策樹演算法](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft 線性迴歸演算法](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)<br /><br /> [Microsoft 羅吉斯迴歸演算法](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)<br /><br /> [Microsoft 貝氏機率分類演算法](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)<br /><br /> [Microsoft 類神經網路演算法](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)<br /><br /> [Microsoft 時序群集演算法](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)<br /><br /> [Microsoft 時間序列演算法](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)|  
|**技術參考**|提供有關演算法實作的技術詳細資料，並視需要提供學術參考。 列出您可以設定的參數，用於控制演算法的行為，並自訂模型中的結果。 描述資料需求，並盡可能提供效能提示。|  
||[Microsoft 關聯分析演算法技術參考](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)<br /><br /> [Microsoft 群集演算法技術參考](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)<br /><br /> [Microsoft 決策樹演算法技術參考](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)<br /><br /> [Microsoft 線性迴歸演算法技術參考](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)<br /><br /> [Microsoft 羅吉斯迴歸演算法技術參考](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)<br /><br /> [Microsoft 貝氏機率分類演算法技術參考](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)<br /><br /> [Microsoft 類神經網路演算法技術參考](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)<br /><br /> [Microsoft 時序群集演算法技術參考](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)<br /><br /> [Microsoft 時間序列演算法技術參考](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)|  
|**模型內容**|說明每種資料採礦模型類型中的資訊結構化方式，並說明如何解譯儲存在每個節點中的資訊。|  
||[關聯模型 & #40; 的採礦模型內容Analysis Services-資料採礦 & #41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)<br /><br /> [叢集模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)<br /><br /> [決策樹模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)<br /><br /> [線性迴歸模型 & #40; 的採礦模型內容Analysis Services-資料採礦 & #41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)<br /><br /> [羅吉斯迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)<br /><br /> [貝氏機率分類模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)<br /><br /> [類神經網路模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)<br /><br /> [時序群集模型 & #40; 的採礦模型內容Analysis Services-資料採礦 & #41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)<br /><br /> [時間序列模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)|  
|**資料採礦查詢**|提供多項可用於每種模型類型的查詢。 例如，可讓您深入了解模型中模式的內容查詢，以及可協助您根據這些模式建立預測的預測查詢。|  
||[關聯模型查詢範例](../../analysis-services/data-mining/association-model-query-examples.md)<br /><br /> [群集模型查詢範例](../../analysis-services/data-mining/clustering-model-query-examples.md)<br /><br /> [決策樹模型查詢範例](../../analysis-services/data-mining/decision-trees-model-query-examples.md)<br /><br /> [線性迴歸模型查詢範例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)<br /><br /> [羅吉斯迴歸模型查詢範例](../../analysis-services/data-mining/logistic-regression-model-query-examples.md)<br /><br /> [貝式機率分類模型查詢範例](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)<br /><br /> [類神經網路模型查詢範例](../../analysis-services/data-mining/neural-network-model-query-examples.md)<br /><br /> [時序群集模型查詢範例](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)<br /><br /> [Time Series Model Query Examples](../../analysis-services/data-mining/time-series-model-query-examples.md)|  
  
## <a name="related-tasks"></a>相關工作  
  
|**主題**|**說明**|  
|---------------|---------------------|  
|確定資料採礦模型所使用的演算法。|[查詢用於建立採礦模型的參數](../../analysis-services/data-mining/query-the-parameters-used-to-create-a-mining-model.md)|  
|建立自訂外掛程式演算法|[外掛程式演算法](../../analysis-services/data-mining/plugin-algorithms.md)|  
|使用演算法特定的檢視器瀏覽模型|[資料採礦模型檢視器](../../analysis-services/data-mining/data-mining-model-viewers.md)|  
|檢視使用一般資料表格式的模型內容|[使用 Microsoft 一般內容樹狀檢視器瀏覽模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)|  
|了解如何設定資料及使用演算法來建立模型|[採礦結構 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)<br /><br /> [採礦模型 & #40;Analysis Services-資料採礦 & #41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦工具。](../../analysis-services/data-mining/data-mining-tools.md)  
  
  
