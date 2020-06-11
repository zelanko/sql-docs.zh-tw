---
title: 資料採礦演算法（Analysis Services 資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- segmentation algorithms [Analysis Services]
- clustering [Data Mining]
- learning algorithms
- data mining [Analysis Services], models
- algorithms [data mining]
- mining models [Analysis Services], algorithms
- inductive learning
- mining models [Analysis Services], creating
- data mining [Analysis Services], algorithms
- machine learning algorithms [Analysis Services]
ms.assetid: ed1fc83b-b98c-437e-bf53-4ff001b92d64
author: minewiskan
ms.author: owend
ms.openlocfilehash: 81d86ba50c76c167e0f6d17cd0dee7e00e6ac938
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84523314"
---
# <a name="data-mining-algorithms-analysis-services---data-mining"></a>資料採礦演算法 (Analysis Services - 資料採礦)
  *資料採礦演算法*是一組啟發學習法和計算，可從資料建立資料採礦模型。 若要建立模型，演算法首先會分析您提供的資料，尋找特定模式和趨勢類型。 此演算法會使用此分析結果來定義用於建立採礦模型的最佳參數。 然後這些參數會套用到整個資料集以擷取可付諸行動的模式與詳細的統計資料。  
  
 演算法從資料建立的採礦模型可以有各種形式，包括：  
  
-   一組叢集，描述資料集的案例如何相關。  
  
-   決策樹，預測結果並描述不同準則如何影響該結果。  
  
-   預測銷售的數學模型。  
  
-   一組規則，描述交易中的產品及購買產品的機率如何群組在一起。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供用於資料採礦解決方案的多種演算法。 這些演算法是資料採礦中所使用之其中一些最常用方法的實作。 所有 Microsoft 資料採礦演算法都可以使用提供的 API，或使用 SQL Server Integration Services 中的資料採礦元件加以自訂及完整程式化。  
  
 您也可以使用符合 OLE DB for Data Mining 規格的協力廠商演算法，或開發可註冊為服務，然後用於 SQL Server 資料採礦架構中的自訂演算法。  
  
## <a name="choosing-the-right-algorithm"></a>選擇正確的演算法  
 選擇特定分析工作最適用的演算法並不容易。 您可以使用不同的演算法來執行相同的業務工作，每一個演算法會產生不同的結果，且部分演算法還會產生一種以上的結果類型。 例如，您可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法，不僅用來預測也可以減少資料集內的資料行數目，因為決策樹可以識別不影響最終採礦模型的資料行。  
  
### <a name="choosing-an-algorithm-by-type"></a>依類型選擇演算法  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包括下列演算法類型：  
  
-   **分類演算法** 會根據資料集內的其他屬性，預測一或多個離散變數。  
  
-   **回歸演算法**會根據資料集內的其他屬性，預測一或多個連續變數，例如利潤或損失。  
  
-   **分割演算法** ：會將項目的資料劃分為具有相似屬性的群組或叢集。  
  
-   **關聯分析演算法** 會尋找資料集內不同屬性之間的相互關聯。 這種演算法最常應用在建立關聯規則，這些規則可以用在購物籃分析。  
  
-   時序**分析演算法**會匯總資料中的頻繁序列或集，例如 Web 路徑流程。  
  
 不過，沒有任何理由限制您在方案中只能使用一種演算法。 有經驗的分析師有時會使用一種演算法來決定最有效的輸入 (亦即變數)，然後套用不同演算法，以根據該資料預測特定結果。 SQL Server 資料採礦可讓您根據單一採礦結構建立多種模型，因此在單一資料採礦方案內，您可以使用叢集演算法、決策樹模型及貝氏機率分類模型，來取得不同的資料檢視。 您也可以在一個方案內使用多種演算法來執行個別的工作：例如，您可以使用迴歸來取得財務預測，以及使用類神經網路演算法來執行影響銷售之因素的分析。  
  
### <a name="choosing-an-algorithm-by-task"></a>依工作選擇演算法  
 為了協助您選取搭配特定工作所使用的演算法，下表提供每種演算法傳統上使用的工作類型建議。  
  
|工作範例|適用的 Microsoft 演算法|  
|-----------------------|---------------------------------|  
|**預測離散屬性**<br /><br /> 將潛在買家清單中的客戶標幟為較佳或較差的潛在客戶。<br /><br /> 計算伺服器在未來 6 個月內失敗的機率。<br /><br /> 分類病人結果並探索相關因素。|[Microsoft 決策樹演算法](microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft 貝氏機率分類演算法](microsoft-naive-bayes-algorithm.md)<br /><br /> [Microsoft 群集演算法](microsoft-clustering-algorithm.md)<br /><br /> [Microsoft 類神經網路演算法](microsoft-neural-network-algorithm.md)|  
|**預測連續屬性**<br /><br /> 預測下一個年度的銷售。<br /><br /> 根據過去歷史和季節性趨勢來預測網站訪客。<br /><br /> 根據人口統計產生風險分數。|[Microsoft 決策樹演算法](microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft 時間序列演算法](microsoft-time-series-algorithm.md)<br /><br /> [Microsoft 線性迴歸演算法](microsoft-linear-regression-algorithm.md)|  
|**預測序列**<br /><br /> 執行公司網站的點選流分析。<br /><br /> 分析導致伺服器失敗的因素。<br /><br /> 擷取及分析看診期間的活動順序，制定出以一般活動為主的最佳作法。|[Microsoft 時序叢集演算法](microsoft-sequence-clustering-algorithm.md)|  
|**在交易中尋找通用專案的群組**<br /><br /> 使用購物籃分析來決定產品位置。<br /><br /> 向客戶建議其他可購買的產品。<br /><br /> 分析參加某事件之訪客的調查資料，以找出相互關聯的活動或攤位，並規劃未來的活動。|[Microsoft Association Algorithm](microsoft-association-algorithm.md)<br /><br /> [Microsoft 決策樹演算法](microsoft-decision-trees-algorithm.md)|  
|**尋找類似專案的群組**<br /><br /> 根據人口統計和行為等屬性，建立病患風險評估群組。<br /><br /> 依瀏覽及購買模式來分析使用者。<br /><br /> 識別具有類似使用特性的伺服器。|[Microsoft 群集演算法](microsoft-clustering-algorithm.md)<br /><br /> [Microsoft 時序叢集演算法](microsoft-sequence-clustering-algorithm.md)|  
  
## <a name="related-content"></a>相關內容  
 下表提供 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 隨附之每種資料採礦演算法的學習資源連結：  
  
|||  
|-|-|  
|**基本演算法描述**|說明演算法的用途與運作方式，並概要說明演算法可能相當實用的商務案例。|  
||[Microsoft Association Algorithm](microsoft-association-algorithm.md)<br /><br /> [Microsoft 群集演算法](microsoft-clustering-algorithm.md)<br /><br /> [Microsoft 決策樹演算法](microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft 線性迴歸演算法](microsoft-linear-regression-algorithm.md)<br /><br /> [Microsoft 羅吉斯迴歸演算法](microsoft-logistic-regression-algorithm.md)<br /><br /> [Microsoft 貝氏機率分類演算法](microsoft-naive-bayes-algorithm.md)<br /><br /> [Microsoft 類神經網路演算法](microsoft-neural-network-algorithm.md)<br /><br /> [Microsoft 時序叢集演算法](microsoft-sequence-clustering-algorithm.md)<br /><br /> [Microsoft 時間序列演算法](microsoft-time-series-algorithm.md)|  
|**技術參考**|提供有關演算法實作的技術詳細資料，並視需要提供學術參考。 列出您可以設定的參數，用於控制演算法的行為，並自訂模型中的結果。 描述資料需求，並盡可能提供效能提示。|  
||[Microsoft 關聯分析演算法技術參考](microsoft-association-algorithm-technical-reference.md)<br /><br /> [Microsoft 群集演算法技術參考](microsoft-clustering-algorithm-technical-reference.md)<br /><br /> [Microsoft 決策樹演算法技術參考](microsoft-decision-trees-algorithm-technical-reference.md)<br /><br /> [Microsoft 線性迴歸演算法技術參考](microsoft-linear-regression-algorithm-technical-reference.md)<br /><br /> [Microsoft 羅吉斯迴歸演算法技術參考](microsoft-logistic-regression-algorithm-technical-reference.md)<br /><br /> [Microsoft 貝氏機率分類演算法技術參考](microsoft-naive-bayes-algorithm-technical-reference.md)<br /><br /> [Microsoft 類神經網路演算法技術參考資料](microsoft-neural-network-algorithm-technical-reference.md)<br /><br /> [Microsoft 時序群集演算法技術參考](microsoft-sequence-clustering-algorithm-technical-reference.md)<br /><br /> [Microsoft 時間序列演算法技術參考](microsoft-time-series-algorithm-technical-reference.md)|  
|**模型內容**|說明每種資料採礦模型類型中的資訊結構化方式，並說明如何解譯儲存在每個節點中的資訊。|  
||[關聯模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md)<br /><br /> [叢集模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)<br /><br /> [決策樹模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)<br /><br /> [線性迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)<br /><br /> [羅吉斯迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-logistic-regression-models.md)<br /><br /> [貝氏機率分類模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)<br /><br /> [類神經網路模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)<br /><br /> [時序叢集模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-sequence-clustering-models.md)<br /><br /> [時間序列模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)|  
|**資料採礦查詢**|提供多項可用於每種模型類型的查詢。 例如，可讓您深入了解模型中模式的內容查詢，以及可協助您根據這些模式建立預測的預測查詢。|  
||[關聯模型查詢範例](association-model-query-examples.md)<br /><br /> [叢集模型查詢範例](clustering-model-query-examples.md)<br /><br /> [決策樹模型查詢範例](decision-trees-model-query-examples.md)<br /><br /> [線性迴歸模型查詢範例](linear-regression-model-query-examples.md)<br /><br /> [羅吉斯迴歸模型查詢範例](logistic-regression-model-query-examples.md)<br /><br /> [貝式機率分類模型查詢範例](naive-bayes-model-query-examples.md)<br /><br /> [類神經網路模型查詢範例](neural-network-model-query-examples.md)<br /><br /> [時序叢集模型查詢範例](sequence-clustering-model-query-examples.md)<br /><br /> [時間序列模型查詢範例](time-series-model-query-examples.md)|  
  
## <a name="related-tasks"></a>相關工作  
  
|**主題**|**描述**|  
|---------------|---------------------|  
|確定資料採礦模型所使用的演算法。|[查詢用於建立採礦模型的參數](query-the-parameters-used-to-create-a-mining-model.md)|  
|建立自訂外掛程式演算法|[外掛程式演算法](plugin-algorithms.md)|  
|使用演算法特定的檢視器瀏覽模型|[資料採礦模型檢視器](data-mining-model-viewers.md)|  
|檢視使用一般資料表格式的模型內容|[使用 Microsoft 一般內容樹狀檢視器瀏覽模型](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)|  
|了解如何設定資料及使用演算法來建立模型|[採礦結構 &#40;Analysis Services - 資料採礦&#41;](mining-structures-analysis-services-data-mining.md)<br /><br /> [採礦模型 &#40;Analysis Services - 資料採礦&#41;](mining-models-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦工具。](data-mining-tools.md)  
  
  
