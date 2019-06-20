---
title: Microsoft 類神經網路演算法 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- training neural networks
- output neurons [Analysis Services]
- algorithms [data mining]
- neural network algorithms [Analysis Services]
- neurons [Analysis Services]
- classification algorithms [Analysis Services]
- neural networks
- multilayer perceptron network of neurons [Analysis Services]
- hidden neurons
- Back-Propagated Delta Rule network
- input neurons [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 61eb4861-8a6a-4214-a4b8-1dd278ad7a68
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a7330fab8b4c0ecdff296e0daa5e529442fd8b94
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083864"
---
# <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm
  在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，則[!INCLUDE[msCoName](../../includes/msconame-md.md)]類神經網路演算法會將輸入屬性的每個可能狀態與可預測的屬性，每個可能狀態結合，並使用定型資料來計算機率。 稍後您可以使用這些機率來進行分類或迴歸，依據輸入屬性預測該預測屬性的結果。  
  
 以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法建構的採礦模型可包含多個網路，視用於輸入和預測的資料行數目或只用於預測的資料行數目而定。 單一採礦模型包含的網路數目，視採礦模型使用的輸入資料行和可預測資料行所包含的狀態數目而定。  
  
## <a name="example"></a>範例  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法在分析複雜輸入資料 (例如來自製造程序或商業程序的資料) 或商務問題 (有大量培訓資料可用但很難使用其他演算法來衍生規則) 時很有用。  
  
 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法的建議狀況包括下列各項：  
  
-   行銷和促銷分析，例如衡量直接郵寄促銷廣告或電台廣告活動的績效。  
  
-   從記錄資料中預測股價移動、貨幣波動或其他高流動性財務資訊。  
  
-   分析製造和產業流程。  
  
-   文字採礦  
  
-   任何分析許多輸入以及較少輸出之間複雜關聯性的預測模型。  
  
## <a name="how-the-algorithm-works"></a>演算法的運作方式  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法會建立最多由三層神經所組成的網路。 這 3 層分別是輸入層、選擇性隱藏層和輸出層。  
  
 **輸入的層：** 輸入的神經會定義資料採礦模型及其機率的所有輸入的屬性值。  
  
 **隱藏的層：** 隱藏神經會接收來自輸入神經的輸入，並提供輸出給輸出神經。 隱藏層是為輸入的各種機率指派加權之處。 加權會對隱藏神經描述特定輸入的相關性或重要性。 指派給輸入的加權越大，該輸入之值的重要性就越大。 加權可以是負數，這表示輸入可以禁止而非喜好特定結果。  
  
 **輸出層：** 輸出神經代表資料採礦模型的可預測屬性值。  
  
 如需輸入、隱藏和輸出層之建構和計分方式的詳細說明，請參閱 [Microsoft 類神經網路演算法技術參考](microsoft-neural-network-algorithm-technical-reference.md)。  
  
## <a name="data-required-for-neural-network-models"></a>類神經網路模型所需的資料  
 類神經網路模型必須包含一個索引鍵資料行、一或多個輸入資料行，以及一或多個可預測資料行。  
  
 您為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法所提供參數指定的值，對使用該演算法的資料採礦模型會有很大的影響。 這些參數定義資料取樣的方式、如何散發或預測每個資料行所散發的資料，以及何時會叫用功能選擇來限制用於最終模型中的值。  
  
 如需設定參數以自訂模型行為的詳細資訊，請參閱 [Microsoft 類神經網路演算法技術參考](microsoft-neural-network-algorithm-technical-reference.md)。  
  
## <a name="viewing-a-neural-network-model"></a>檢視類神經網路模型  
 若要使用資料並查看模型如何在輸入與輸出之間產生關聯，可以使用 **Microsoft 類神經網路檢視器**。 您可以利用這個自訂的檢視器來篩選輸入屬性及其值，並查看示範這些屬性和值如何影響輸出的圖表。 檢視器中的工具提示會顯示與每個成對輸入和輸出值相關聯的機率與增益。 如需詳細資訊，請參閱 [使用 Microsoft 類神經網路檢視器瀏覽模型](browse-a-model-using-the-microsoft-neural-network-viewer.md)。  
  
 瀏覽模型結構最簡單的方式就是使用 **Microsoft 一般內容樹狀檢視器**。 您可以檢視此模型所建立的輸入、輸出和網路，並可按一下任一節點加以展開，然後查看與輸入、輸出或隱藏層節點相關的統計資料。 如需詳細資訊，請參閱 [使用 Microsoft 一般內容樹狀檢視器瀏覽模型](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)。  
  
## <a name="creating-predictions"></a>建立預測  
 當模型經過處理之後，您就可以使用網路和每個節點內儲存的加權來進行預測。 類神經網路模型支援迴歸、關聯和分類分析，因此每個預測的意義都可能不同。 您也可以查詢模型本身，以檢視找到的關聯性並擷取相關的統計資料。 如需如何針對類神經網路模型建立查詢的範例，請參閱 [類神經網路模型查詢範例](neural-network-model-query-examples.md)。  
  
 如需如何在資料採礦模型上建立查詢的一般資訊，請參閱 [資料採礦查詢](data-mining-queries.md)。  
  
## <a name="remarks"></a>備註  
  
-   不支援鑽研或資料採礦維度。 這是因為採礦模型中的節點結構不一定會直接對應至基礎資料。  
  
-   不支援使用預測模型標記語言 (PMML) 格式來建立模型。  
  
-   支援 OLAP 採礦模型的使用。  
  
-   不支援建立資料採礦維度。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 類神經網路演算法技術參考](microsoft-neural-network-algorithm-technical-reference.md)   
 [類神經網路模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [類神經網路模型查詢範例](neural-network-model-query-examples.md)   
 [Microsoft 羅吉斯迴歸演算法](microsoft-logistic-regression-algorithm.md)  
  
  
