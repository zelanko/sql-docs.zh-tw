---
title: Microsoft 群集演算法技術參考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [Data Mining]
- MAXIMUM_INPUT_ATTRIBUTES parameter
- CLUSTER_SEED parameter
- MODELLING_CARDINALITY parameter
- MINIMUM_SUPPORT parameter
- STOPPING_TOLERANCE parameter
- MAXIMUM_STATES parameter
- SAMPLE_SIZE parameter
- CLUSTERING_METHOD parameter
- soft clustering [Data Mining]
- clustering algorithms [Analysis Services]
- CLUSTER_COUNT parameter
ms.assetid: ec40868a-6dc7-4dfa-aadc-dedf69e555eb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3bf6919230c1621d2b81eb41cd715fc1878a90c5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721881"
---
# <a name="microsoft-clustering-algorithm-technical-reference"></a>Microsoft 群集演算法技術參考
  本節說明 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 叢集演算法的實作，包括可用來控制群集模型行為的參數。 本章節也提供在建立及處理叢集模型時如何改善效能的指南。  
  
 如需有關如何使用叢集模型的詳細資訊，請參閱下列主題：  
  
-   [叢集模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
-   [群集模型查詢範例](clustering-model-query-examples.md)  
  
## <a name="implementation-of-the-microsoft-clustering-algorithm"></a>Microsoft 群集演算法的實作  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法提供兩種方法來建立群集並將資料點指派給群集。 第一種方法是 *K-means* 演算法，這是一種硬式群集方法。 這代表資料點只能屬於一個群集，而且會針對該群集中每個資料點的成員資格而計算單一機率。 第二種方法是 *Expectation Maximization* (EM) 方法，這是一種軟式群集方法。 這代表資料點一定屬於多個群集，而且會針對資料點和群集的每個組合而計算機率。  
  
 您可以設定 *CLUSTERING_METHOD* 參數以選擇要使用的演算法。 預設的群集方法是可擴充的 EM。  
  
### <a name="em-clustering"></a>EM 群集  
 在 EM 群集中，演算法會反覆地精簡初始群集模型以符合資料，並判斷資料點存在於群集內的機率。 演算法會在機率模型符合資料時結束此程序。 用來決定符合度的函數是在模型已知時的資料對數可能性。  
  
 如果在程序期間產生空白的群集，或者如果一或多個群集的成員資格落在指定臨界值之下，則具有低母體的群集會在新的資料點重設種子，然後再重新執行 EM 演算法  
  
 EM 群集方法的結果並非機率式。 這代表每個資料點都屬於所有的群集，但每次指定資料點給群集時都具有不同的機率。 因為此方法允許群集重疊，所以所有群集中的項目總和可能會超過定型集中的項目總數。 在採礦模型結果中會調整代表支援的分數來解決這種情況。  
  
 EM 演算法是用於 Microsoft 群集模型中的預設演算法。 之所以用這個演算法來當做預設值，是因為與 K-means 群集相較，它可提供多項優勢：  
  
-   最多只需要掃描一次資料庫。  
  
-   儘管記憶體 (RAM) 有限仍可運作。  
  
-   能夠使用順向資料指標。  
  
-   執行速度快過取樣方法。  
  
 Microsoft 實作提供兩種選擇：可擴充的 EM 和不可擴充的 EM。 在可擴充的 EM 中，根據預設會使用前 50,000 筆記錄來植入初始掃描。 如果這項作業成功，則模型僅會使用這些資料。 如果無法使用 50,000 筆記錄來找到相符的模型，就會再讀取額外的 50,000 筆記錄。 在不可擴充的 EM 中，則不論資料集的大小，都會讀取整個資料集。 這種方法可能會建立更正確的群集，但記憶體需求可能很高。 因為可擴充的 EM 是以本機緩衝區作業，所以反覆執行資料的速度會快得多，且其演算法運用 CPU 記憶體快取的方法也比不可擴充的 EM 高明許多。 此外，即使所有資料都可放入主記憶體，可擴充的 EM 速度也比不可擴充的 EM 快了三倍。 在大多數的案例中，效能改善並不會導致整個模型的品質降低。  
  
 如需描述以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法實作之 EM 的技術報告，請參閱 [Scaling EM (Expectation Maximization) Clustering to Large Databases](https://go.microsoft.com/fwlink/?LinkId=45964)(將 EM (Expectation Maximization) 群集擴充為大型資料庫)。  
  
### <a name="k-means-clustering"></a>K-means 群集  
 K-means 群集是知名的群集成員資格指派方法，作業方式是將群集中項目之間的差異最小化，並將群集之間的距離最大化。 K-means 中的 "means" 是指群集的「距心」，這是任意選擇的資料點，在選擇後會反覆調整，直到能代表群集中所有資料點的真正平均值為止。 "k" 則是指用來植入群集程序的任意數目的資料點。 K-means 演算法會計算群集中資料記錄之間的歐氏距離平方 (Squared Euclidean Distance) 以及代表群集平均值的向量，然後在總和達到最小值時聚合於最終的一組 K 群集。  
  
 K-means 演算法會將每個資料點剛好指派給一個群集，而不允許成員資格有任何不確定性。 群集中的成員資格會以與距心的距離來表示。  
  
 一般而言，K-means 演算法可用來建立連續屬性的群集，其中與平均值距離的計算相當簡單。 不過， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 實作會使用機率，將 K-means 方法調整為適用於群集離散屬性。  對離散屬性而言，資料點與特定群集的距離計算方法如下：  
  
 1 - P(data point, cluster)  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法不會公開用來計算 K-means 的距離函數，而距離量值則無法用於完成的模型中。 不過，您可以使用預測函數來傳回對應至距離的值，其中距離是計算成屬於群集之資料點的機率。 如需詳細資訊，請參閱 [ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx)。  
  
 K-means 演算法提供兩種資料集取樣的方法：一種是不可擴充的 K-means，這種方法會載入整個資料集，且進行一次群集行程；另一種則是可擴充的 K-means，其中演算法會使用前 50,000 個案例，且只有在需要更多資料才能達到更佳的模型與資料符合度時，才會讀取更多的案例。  
  
### <a name="updates-to-the-microsoft-clustering-algorithm-in-sql-server-2008"></a>SQL Server 2008 中的 Microsoft 群集演算法更新  
 在 SQL Server 2008 中， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法的預設組態已變更為使用內部參數 NORMALIZATION = 1。 正規化是使用 Z-score 統計資料執行，採用常態分佈。 此預設行為變更的意圖是將可能有大範圍和許多極端值之屬性的影響降至最低。 不過，Z-score 正規化可能會在非常態分佈 (例如統一分佈) 上改變群集結果。 若要防止正規化，取得和 SQL Server 2005 中的 K-means 群集演算法相同的行為，您可以使用 [參數設定] 對話方塊加入自訂參數 NORMALIZATION，並將其值設定為 0。  
  
> [!NOTE]  
>  NORMALIZATION 參數是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法的內部屬性，不受支援。 一般而言，建議在群集模型中使用正規化，以改善模型結果。  
  
## <a name="customizing-the-microsoft-clustering-algorithm"></a>自訂 Microsoft 群集演算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 叢集演算法支援數個會影響所產生之採礦模型的行為、效能和精確度的參數。  
  
### <a name="setting-algorithm-parameters"></a>設定演算法參數  
 下表描述可用於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法的參數。 這些參數對於所產生之採礦模型的效能和精確度都有影響。  
  
 CLUSTERING_METHOD  
 指定演算法要使用的群集方法。 可用的群集方法有：  
  
|ID|方法|  
|--------|------------|  
|1|可擴充的 EM|  
|2|不可擴充的 EM (Non-scalable EM)|  
|3|可擴充的 K-means|  
|4|不可擴充的 K-means|  
  
 預設值為 1 (可擴充的 EM)。  
  
 CLUSTER_COUNT  
 指定演算法要建立的大約群集數目。 如果無法從資料建立大約群集數目，則演算法會盡可能建立最多的群集。 將 CLUSTER_COUNT 設定為 0 會造成演算法使用啟發式決定，對於建立的群集數做出最好的決定。  
  
 預設值是 10。  
  
 CLUSTER_SEED  
 指定在模型建立的初始階段，用於隨機產生群集的種子號碼。  
  
 藉由變更此數字，您可以變更建立初始群集的方法，然後比較使用不同的種子而建立的模型。 如果種子已變更，但找到的群集並未大幅變更，則可將模型視為相當穩定。  
  
 預設值是 0。  
  
 MINIMUM_SUPPORT  
 指定建立群集所需的案例最小數目。 如果群集中的案例數目低於此數目，則會將群集視為空白並加以捨棄。  
  
 如果將此數目設得過高，則可能會遺漏有效的群集。  
  
> [!NOTE]  
>  如果您使用預設的群集方法 EM，則某些群集可能會有比指定值低的支援值。 這是因為每個案例都會針對它在所有可能群集中的成員資格進行評估，而某些群集可能只有最少的支援。  
  
 預設值是 1。  
  
 MODELLING_CARDINALITY  
 指定在叢集處理期間建構的範例模型數目。  
  
 減少候選模型的數目可以改善效能，但風險是可能會遺漏某些完善的候選模型。  
  
 預設值是 10。  
  
 STOPPING_TOLERANCE  
 指定用來決定何時到達聚合以及演算法完成模型建立的值。 當群集機率的整體變更小於 STOPPING_TOLERANCE 參數除以模型大小的比率時，就到達聚合。  
  
 預設值是 10。  
  
 SAMPLE_SIZE  
 指定如果 CLUSTERING_METHOD 參數設定為可擴充的其中一個群集方法時，演算法在每個行程上使用的案例數目。 將 SAMPLE_SIZE 參數設定為 0 會導致整個資料集群集在單一行程中。 在單一行程中載入整個資料集可能會導致記憶體和效能的問題。  
  
 預設值是 50000。  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 指定在叫用特徵選取之前，演算法可以處理輸入屬性的最大數目。 將此值設定為 0 即指定屬性數目沒有上限。  
  
 增加屬性數目可能會使效能顯著下降。  
  
 預設值是 255。  
  
 MAXIMUM_STATES  
 指定演算法所支援之屬性狀態的最大數目。 如果屬性擁有的狀態數超過最大值，則演算法會使用最常用的狀態，並忽略其餘的狀態。  
  
 增加狀態數目可能會使效能顯著下降。  
  
 預設值為 100。  
  
### <a name="modeling-flags"></a>模型旗標  
 演算法支援下列模型旗標。 您可以在建立採礦結構或採礦模型時定義模型旗標。 模型旗標會指定在分析期間如何處理每個資料行中的值。  
  
|模型旗標|描述|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|資料會被視為擁有兩個可能狀態：遺失，且現有的。 Null 為遺漏值。<br /><br /> 適用於採礦模型資料行。|  
|NOT NULL|資料行不得包含 Null 值。 如果 Analysis Services 在模型定型期間遇到 Null 值，將會產生錯誤。<br /><br /> 適用於採礦結構資料行。|  
  
## <a name="requirements"></a>需求  
 叢集模型必須包含索引鍵資料行和輸入資料行。 您也可以將輸入資料行定義為可預測的。 設定為 `Predict Only` 的資料行不會用來建立群集。 這些值在群集內的散發是在建立群集之後才計算的。  
  
### <a name="input-and-predictable-columns"></a>輸入和可預測資料行  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法支援下表所列的特定輸入資料行和可預測資料行。 如需內容類型用於採礦模型時所代表意義的詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](content-types-data-mining.md)。  
  
|「資料行」|內容類型|  
|------------|-------------------|  
|輸入屬性|Continuous、Cyclical、Discrete、Discretized、Key、Table 和 Ordered|  
|可預測屬性|Continuous、Cyclical、Discrete、Discretized、Table 和 Ordered|  
  
> [!NOTE]  
>  系統支援 Cyclical 和 Ordered 內容類型，但是演算法將它們視為離散值，因此不會執行特殊處理。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 群集演算法](microsoft-clustering-algorithm.md)   
 [叢集模型查詢範例](clustering-model-query-examples.md)   
 [叢集模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
  
