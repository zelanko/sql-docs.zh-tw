---
title: 採礦模型檢視器（資料採礦模型設計工具） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.viewers.f1
ms.assetid: 4ba391d5-c97b-4848-ba7c-7d096fa4b7dd
author: minewiskan
ms.author: owend
ms.openlocfilehash: a08f7fbccf1192f946043ebe932020d0fe5d3409
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84537570"
---
# <a name="mining-model-viewers-data-mining-model-designer"></a>採礦模型檢視器 (資料採礦模型設計師)
  使用 **[採礦模型檢視器]** 索引標籤，即可瀏覽採礦結構所包含的採礦模型。

 您要先選取採礦模型，然後再選取檢視器。 每一個模型一定都有兩個可用的檢視器：自訂檢視器 (可包含多個索引標籤) 和一般檢視器。

 如需如何使用每個檢視器的逐步解說，請參閱 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)。

## <a name="common-options"></a>一般選項
 **重新整理檢視器內容** 在檢視器中重新載入採礦模型。

 **採礦模型** 選擇包含在目前採礦結構中，您要檢視的採礦模型。 採礦模型將會先在其關聯的自訂檢視器中開啟。

 **檢視器** 選擇用來瀏覽選取之採礦模型的檢視器。 這份清單包含 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 為每個採礦模型提供的查看 [!INCLUDE[msCoName](../includes/msconame-md.md)] 器、挖掘內容檢視器，以及任何外掛程式檢視器。

 下圖顯示相同模型的自訂檢視器和一般檢視器。

-   上方圖表顯示以 Microsoft 時間序列演算法為基礎之採礦模型的檢視器。 這個特定自訂檢視器會自動建立時間序列的圖形，並提供五個預測。

-   下方圖表顯示使用 **[Microsoft 一般內容樹狀檢視器]** 時所顯示的相同模型。 此檢視器會根據標準化結構描述呈現採礦模型的內容。 如需詳細資訊，請參閱 [Microsoft 一般內容樹狀檢視器 &#40;資料採礦&#41;](microsoft-generic-content-tree-viewer-data-mining.md)。

 ![採礦模型設計工具的概觀](media/generic-mining-model-tab1.gif "採礦模型設計工具的概觀")

## <a name="viewers-and-their-components"></a>檢視器及其元件
 根據您所選取的模型，將會看見不同的自訂檢視器，而且它會依照您用來建立選定資料採礦模型的演算法而訂製。 每一個自訂檢視器都有各種工具和對話方塊，可幫助您瀏覽模型中的統計資料和模式。

 下列清單描述的是每個自訂檢視器中的選項。

### <a name="microsoft-association-rules-algorithm"></a>Microsoft 關聯規則演算法

-   [使用 Microsoft 關聯規則檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)

    -   [專案集索引標籤 &#40;&#41;的 [採礦模型檢視器]](itemsets-tab-mining-model-viewer.md)

    -   [[規則] 索引標籤 &#40;&#41;的採礦模型檢視器](rules-tab-mining-model-viewer.md)

    -   [[相依性網路] 索引標籤 &#40;&#41;的採礦模型檢視器](dependency-network-tab-mining-model-viewer.md)

### <a name="microsoft-clustering-algorithm"></a>Microsoft 群集演算法

-   [使用 Microsoft 叢集檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)

    -   [[叢集圖表] 索引標籤 &#40;[採礦模型檢視器]&#41;](cluster-diagram-tab-mining-model-viewer.md)

    -   [[叢集設定檔] 索引標籤 &#40;&#41;的採礦模型檢視器](cluster-profiles-tab-mining-model-viewer.md)

    -   [[叢集特性] 索引標籤 &#40;[採礦模型檢視器]&#41;](cluster-characteristics-tab-mining-model-viewer.md)

    -   [&#40;採礦模型檢視器&#41;的 [叢集辨識] 索引標籤](cluster-discrimination-tab-mining-model-viewer.md)

    -   [[挖掘圖例] 對話方塊 &#40;[採礦模型檢視器]&#41;](mining-legend-dialog-box-mining-model-viewer.md)

### <a name="microsoft-decision-tree-algorithm"></a>Microsoft 決策樹演算法

-   [使用 Microsoft 樹狀檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)

    -   [[決策樹] 索引標籤 &#40;[採礦模型檢視器]&#41;](decision-tree-tab-mining-model-viewer.md)

    -   [[相依性網路] 索引標籤 &#40;&#41;的採礦模型檢視器](dependency-network-tab-mining-model-viewer.md)

    -   [[挖掘圖例] 對話方塊 &#40;[採礦模型檢視器]&#41;](mining-legend-dialog-box-mining-model-viewer.md)

### <a name="microsoft-linear-regression-algorithm"></a>Microsoft 線性迴歸演算法

-   [使用 Microsoft 類神經網路檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)

    -   [[決策樹] 索引標籤 &#40;[採礦模型檢視器]&#41;](decision-tree-tab-mining-model-viewer.md)

    -   [[相依性網路] 索引標籤 &#40;&#41;的採礦模型檢視器](dependency-network-tab-mining-model-viewer.md)

    -   [[挖掘圖例] 對話方塊 &#40;[採礦模型檢視器]&#41;](mining-legend-dialog-box-mining-model-viewer.md)

### <a name="microsoft-logistic-regression-algorithm"></a>Microsoft 羅吉斯迴歸演算法

-   [使用 Microsoft 類神經網路檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)

### <a name="microsoft-nave-bayes-algorithm"></a>Microsoft 貝氏機率分類演算法

-   [使用 Microsoft 貝氏機率分類檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)

    -   [[相依性網路] 索引標籤 &#40;&#41;的採礦模型檢視器](dependency-network-tab-mining-model-viewer.md)

    -   [[屬性設定檔] 索引標籤 &#40;[採礦模型檢視器&#41;](attribute-profiles-tab-mining-model-viewer.md)

    -   [[屬性特性] 索引標籤 &#40;[採礦模型檢視器]&#41;](attribute-characteristics-tab-mining-model-viewer.md)

    -   [[屬性辨識] 索引標籤 &#40;[採礦模型檢視器]&#41;](attribute-discrimination-tab-mining-model-viewer.md)

### <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm

-   [使用 Microsoft 類神經網路檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)

    -   [[相依性網路] 索引標籤 &#40;&#41;的採礦模型檢視器](dependency-network-tab-mining-model-viewer.md)

    -   [類神經網路 &#40;採礦模型檢視器&#41;](neural-network-mining-model-viewer.md)

    -   [[尋找節點] 對話方塊 &#40;[採礦模型檢視器]&#41;](find-node-dialog-box-mining-model-viewer.md)

### <a name="microsoft-sequence-clustering-algorithm"></a>Microsoft 時序叢集演算法

-   [使用 Microsoft 時序叢集檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)

    -   [時序群集叢集圖表索引標籤 &#40;[採礦模型檢視器]](sequence-clustering-cluster-diagram-tab-mining-model-viewer.md)

    -   [時序群集 [叢集設定檔] 索引標籤 &#40;[採礦模型檢視器]](sequence-clustering-cluster-profiles-tab-mining-model-viewer.md)

    -   [時序群集叢集特性索引標籤 &#40;採礦模型檢視器&#41;](sequence-clustering-cluster-characteristics-tab-mining-model-viewer.md)

    -   [時序群集叢集辨識索引標籤 &#40;採礦模型檢視器&#41;](sequence-clustering-cluster-discrimination-tab-mining-model-viewer.md)

    -   [時序群集 [叢集轉換] 索引標籤 &#40;&#41;的採礦模型檢視器](sequence-clustering-cluster-transition-tab-mining-model-viewer.md)

### <a name="microsoft-time-series-algorithm"></a>Microsoft 時間序列演算法

-   [使用 Microsoft 時間序列檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)

    -   [模型索引標籤 &#40;採礦模型檢視器&#41;](model-tab-mining-model-viewers.md)

    -   [[圖表] 索引標籤 &#40;採礦模型檢視器&#41;](chart-tab-mining-model-viewers.md)

    -   [[挖掘圖例] 對話方塊 &#40;[採礦模型檢視器]&#41;](mining-legend-dialog-box-mining-model-viewer.md)

## <a name="see-also"></a>另請參閱
 [採礦模型 view &#40;資料採礦模型設計工具&#41;](mining-models-view-data-mining-model-designer.md) [&#40;資料採礦模型設計工具&#41;](mining-structure-view-data-mining-model-designer.md) [挖掘精確度圖表設計工具 &#40;資料採礦&#41;](mining-accuracy-chart-designer-data-mining.md) [預測查詢產生器 &#40;資料採礦&#41;](prediction-query-builder-data-mining.md)


