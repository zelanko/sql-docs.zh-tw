---
title: 演算法參數 （SQL Server 資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MAXIMUM_STATES
- FORCED_REGRESSOR
- PERIODICITY_HINT
- HOLDOUT_SEED
- MAXIMUM_ITEMSET_SIZE
- HIDDEN_NODE_RATIO
- CLUSTERING_METHOD
- FORECAST_METHOD
- STOPPING_TOLERANCE
- MISSING_VALUE_SUBSTITUTION
- MINIMUM_IMPORTANCE
- HISTORIC_MODEL_COUNT
- SPLIT_METHOD
- MAXIMUM_OUTPUT_ATTRIBUTES
- HOLDOUT_PERCENTAGE
- MINIMUM_PROBABILITY
- SAMPLE_SIZE
- HISTORICAL_MODEL_GAP
- CLUSTER_SEED
- SCORE_METHOD
- INSTABILITY_SENSITIVITY
- AUTO_DETECT_PERIODICITY
- MAXIMUM_SEQUENCE_STATES
- MINIMUM_DEPENDENCY_PROBABILITY
- MINIMUM_SUPPORT
- MAXIMUM_SUPPORT
- MINIMUM_ITEMSET_SIZE
- PREDICTION_SMOOTHING
- algorithm parameters
- MAXIMUM_SERIES_VALUE
- MODELLING_CARDINALITY
- MAXIMUM_INPUT_ATTRIBUTES
- MINIMUM_SERIES_VALUE
- MAXIMUM_ITEMSET_COUNT
- CLUSTER_COUNT
- COMPLEXITY_PENALTY
ms.assetid: fcdc3f85-813d-4279-90b0-16e26edd008d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92ff53ae795fa4d0565ca9b1537a7d12bc8f0b5b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48147608"
---
# <a name="algorithm-parameters-sql-server-data-mining-add-ins"></a>演算法參數 (SQL Server 資料採礦增益集)
  當您使用適用於 Excel 的資料表分析工具來執行資料採礦時，您不需要設定資料採礦演算法或參數；每一個工具都會分析資料，並自動選取最佳參數。 但是，如果您想要修改模型或是從頭開始建立採礦模型，適用於 Excel 的資料採礦用戶端提供了幾個選項供您自訂。  
  
-   手動建立資料採礦模型，依序按一下**進階**，然後按一下**將模型加入結構**。  
  
-   在 資料採礦用戶端，使用任何一個模型精靈，然後按一下**參數**來控制行為的[!INCLUDE[msCoName](../includes/msconame-md.md)]資料採礦演算法。  
  
-   按一下 **查詢**以開啟 查詢模型精靈，然後按一下**進階**以開啟**資料採礦進階查詢編輯器**。 在此編輯器中，您可以使用 DMX 範本建立模型。  
  
 您也可以修改已經建立之採礦模型的行為，或者也可以在採礦模型檢視器中設定參數來篩選結果。  
  
## <a name="list-of-algorithm-parameters"></a>演算法參數的清單  
 所有的 [!INCLUDE[msCoName](../includes/msconame-md.md)] 演算法都可以藉由設定參數來加以自訂。 由於最佳參數設定取決於資料的構成要素而定，所以變更參數之效果的完整說明已超出本主題的範圍。  
  
 下表將列出參數、描述其功能，並提供更多技術性資訊的連結。  
  
|參數名稱|使用於|描述|  
|--------------------|-------------|-----------------|  
|AUTO_DETECT_PERIODICITY|Microsoft 時間序列演算法|指定 0 和 1 之間的數值，用來偵測週期性。 將這個值設定為愈接近 1，就會探索更多接近週期性的模式，並自動產生週期性提示。 處理大量週期性提示時，可能會造成更長的模型定型時間及更精確的模型。 如果將此值設定為愈接近 0，則只會偵測到週期性很強的資料。<br /><br /> 預設值為 0.6。|  
|CLUSTER_COUNT|Microsoft 群集演算法<br /><br /> Microsoft 時序叢集演算法|指定演算法要建立的大約群集數目。 如果無法從資料建立大約群集數目，則演算法會盡可能建立最多的群集。 將 CLUSTER_COUNT 設定為 0 會造成演算法使用啟發式決定，對於建立的群集數做出最好的決定。<br /><br /> 預設值是 10。|  
|CLUSTER_SEED|Microsoft 群集演算法|指定在模型建立的初始階段，用於隨機產生群集的種子號碼。<br /><br /> 預設值是 0。|  
|CLUSTERING_METHOD|Microsoft 群集演算法|指定演算法要使用的群集方法。 可用的群集方法有：可擴充的 EM (1)、不可擴充的 EM (2)、可擴充的 K-means (3) 和不可擴充的 K-means (4)。<br /><br /> 預設值是 1。|  
|COMPLEXITY_PENALTY|Microsoft 決策樹演算法<br /><br /> Microsoft 時間序列演算法|控制決策樹的成長。 低值會增加分岔數目，而高值會減少分岔數目。 預設值是依據特定模型的屬性數目，如下列清單所述：<br /><br /> 1 到 9 個屬性，預設值為 0.5。<br /><br /> 10 到 99 個屬性，預設值為 0.9。<br /><br /> 100 個以上的屬性，預設值為 0.99。<br /><br /> 注意： 在時間序列模型，此參數僅適用於使用 ARTxp 演算法建立模型或混合模型。|  
|FORCED_REGRESSOR|Microsoft 決策樹演算法<br /><br /> Microsoft 線性迴歸演算法|強制演算法使用指定的資料行作為迴歸輸入變數，不考慮演算法計算出來之資料行的重要性。<br /><br /> 注意： 這個參數只用於預測連續屬性的決策樹。 根據定義，線性迴歸模型是一種特殊案例的決策樹，可預測持續的屬性。 但是，任何決策樹模型都可以包含一個代表線性迴歸公式的節點。|  
|FORECAST_METHOD|Microsoft 時間序列演算法|指示是否應該使用 ARTxp 演算法、ARIMA 演算法或這兩者的組合來進行預測。<br /><br /> 預設值為 MIXED。|  
|HIDDEN_NODE_RATIO|Microsoft Neural Network Algorithm|指定隱藏神經與輸入和輸出神經的比例。 下列公式決定隱藏層中的初始神經數目：<br /><br /> HIDDEN_NODE_RATIO * SQRT(總輸入神經 \* 總輸出神經)<br /><br /> 預設值為 4.0。|  
|HISTORIC_MODEL_COUNT|Microsoft 時間序列演算法|指定要建立的記錄模型數目。<br /><br /> 預設值是 1。|  
|HISTORICAL_MODEL_GAP|Microsoft 時間序列演算法|指定兩個連續記錄模型之間的時間延遲。 例如，將此值設定為 g，會造成要建立記錄模型的資料，依 g、2\*g、3\*g 等等的間隔而遭到時間配量截斷。<br /><br /> 預設值是 10。|  
|HOLDOUT_PERCENTAGE|Microsoft 羅吉斯迴歸演算法<br /><br /> Microsoft Neural Network Algorithm|指定用來計算鑑效組錯誤之定型資料內的案例百分比，這可作為定型採礦模型時停止準則的一部分。<br /><br /> 預設值是 30。<br /><br /> 注意：這個參數與套用到採礦結構的鑑效組百分比值不同。|  
|HOLDOUT_SEED|Microsoft 羅吉斯迴歸演算法<br /><br /> Microsoft Neural Network Algorithm|在演算法隨機決定鑑效組資料時，指定用來植入虛擬隨機產生器的數字。 如果此參數設定為 0，此演算法會依據採礦模型的名稱產生種子，以保證在重新處理期間，模型內容保持不變。<br /><br /> 預設值是 0。<br /><br /> 注意：這個參數與套用到採礦結構的鑑效組種子值不同。|  
|INSTABILITY_SENSITIVITY|Microsoft 時間序列演算法|控制預測變異數超過某個臨界值且 ARTxp 演算法隱藏預測的那個點。 預設值是 1。<br /><br /> 注意： 這個參數只適用於混合式的模型或模型使用 ARTxp 演算法。|  
|MAXIMUM_INPUT_ATTRIBUTES|Microsoft 群集演算法<br /><br /> Microsoft 決策樹演算法<br /><br /> Microsoft 線性迴歸演算法<br /><br /> Microsoft 貝氏機率分類演算法<br /><br /> Microsoft Neural Network Algorithm<br /><br /> Microsoft 羅吉斯迴歸演算法|定義演算法在叫用特徵選取之前，可以處理的輸入屬性數目。 將此值設定為 0 可關閉特徵選取。<br /><br /> 預設值是 255。|  
|MAXIMUM_ITEMSET_COUNT|Microsoft Association Algorithm|指定要產生的最大項目集數目。 如果沒有指定數目，演算法會產生所有可能的項目集。<br /><br /> 預設值是 200000。|  
|MAXIMUM_ITEMSET_SIZE|Microsoft Association Algorithm|指定項目集內所允許的最大項目數。 將此值設定為 0，即代表項目集沒有大小限制。<br /><br /> 預設值是 3。|  
|MAXIMUM_OUTPUT_ATTRIBUTES|Microsoft 決策樹演算法<br /><br /> Microsoft 線性迴歸演算法<br /><br /> Microsoft 羅吉斯迴歸演算法<br /><br /> Microsoft 貝氏機率分類演算法<br /><br /> Microsoft Neural Network Algorithm|定義演算法在叫用特徵選取之前，可以處理的輸出屬性數目。 將此值設定為 0 可關閉特徵選取。<br /><br /> 預設值是 255。|  
|MAXIMUM_SEQUENCE_STATES|Microsoft 時序叢集演算法|指定一個順序可以具有的最大狀態數目。 將此值設定為大於 100 的數字，可能會導致演算法建立一個無法提供有用資訊的模型。<br /><br /> 預設值為 64。|  
|MAXIMUM_SERIES_VALUE|Microsoft 時間序列演算法|指定用於預測的最大值。 這個參數會與 MINIMUM_SERIES_VALUE 一起使用，將預測限制為某個預期的範圍。 例如，您可以指定任何一天的預期銷售數量絕對不能超過存貨產品數。|  
|MAXIMUM_STATES|Microsoft 群集演算法<br /><br /> Microsoft Neural Network Algorithm<br /><br /> Microsoft 時序叢集演算法|指定演算法所支援之屬性狀態的最大數目。 如果屬性的狀態數目大於狀態數目上限，則演算法會使用屬性最常用的狀態，而忽略其餘狀態。<br /><br /> 預設值為 100。|  
|MAXIMUM_SUPPORT|Microsoft Association Algorithm|指定項目集可支援的最大案例數目。 如果此值小於 1，則此值代表總案例數的百分比。 如果這個值大於 1，則這個值會代表可包含項目集的絕對案例數目。<br /><br /> 預設值是 1。|  
|MINIMUM_IMPORTANCE|Microsoft Association Algorithm|指定關聯規則的重要性臨界值。 重要性小於這個值的規則會被篩選掉。|  
|MINIMUM_ITEMSET_SIZE|Microsoft Association Algorithm|指定項目集內所允許的最小項目數目。<br /><br /> 預設值是 1。|  
|MINIMUM_DEPENDENCY_PROBABILITY|Microsoft 貝氏機率分類演算法|指定介於輸入和輸出屬性之間的最小相依機率。 這個值會用來限制演算法所產生之內容的大小。 此屬性可設定為 0 到 1。 越大的值會減少模型內容中的屬性數目。<br /><br /> 預設值是 0.5。|  
|MINIMUM_PROBABILITY|Microsoft Association Algorithm|指定規則成立的最小機率。 例如，將此值設定為 0.5 會指定不產生機率小於 50% 的規則。<br /><br /> 預設值是 0.4。|  
|MINIMUM_SERIES_VALUE|Microsoft 時間序列演算法|指定任何時間序列預測的下限。 預測值絕對不小於此限制。|  
|MINIMUM_SUPPORT|Microsoft Association Algorithm|指定演算法產生規則之前必須包含項目集的最小案例數目。 將此值設定為小於 1，是以總案例數的百分比來指定最小案例數目。 將此值設定為大於 1 的整數，是以必須包含項目集的絕對案例數目來指定最小案例數目。 如果記憶體有限，演算法可增加此參數的值。<br /><br /> 預設值是 0.03。|  
|MINIMUM_SUPPORT|Microsoft 群集演算法|指定每一個群集中的最小案例數目。<br /><br /> 預設值是 1。|  
|MINIMUM_SUPPORT|Microsoft 決策樹演算法|決定要在決策樹中產生分岔所需的最小分葉案例數目。<br /><br /> 預設值是 10。|  
|MINIMUM_SUPPORT|Microsoft 時序叢集演算法|指定每一個群集中的最小案例數目。<br /><br /> 預設值是 10。|  
|MINIMUM_SUPPORT|Microsoft 時間序列演算法|指定要在每一個時間序列樹中產生分割所需之時間配量的最小數目。<br /><br /> 預設值是 10。|  
|MISSING_VALUE_SUBSTITUTION|Microsoft 時間序列演算法|指定用來填滿記錄資料中之間距的方法。 依預設，資料中不允許有不規則的間距或不完全的邊緣。 下列方法可用來填滿不規則間距或邊緣：使用上一個值、使用平均值或使用特定數值常數。|  
|MODELLING_CARDINALITY|Microsoft 群集演算法|指定在叢集處理期間建構的範例模型數目。<br /><br /> 預設值是 10。|  
|PERIODICITY_HINT|Microsoft 時間序列演算法|提供演算法關於資料週期性的提示。 例如，若每年銷售不同，而且數列中的度量單位是月，則週期性是 12。 此參數採用 {n [, n]} 的格式，其中 n 為任意正數。 方括號 [] 內的 n 是選擇性的，可以視需要而重複。<br /><br /> 預設為 {1}。|  
|PREDICTION_SMOOTHING|Microsoft 時間序列演算法|控制 ARTXP 和 ARIMA 時間序列演算法的混合。 只有當 FORECAST_METHOD 參數設定為 MIXED 時，指定的值才有效。 必須介於 0 到 1 之間。 如果值為 0，此模型只會使用 ARTXP。 如果值為 1，模型只會使用 ARIMA。 趨近於 0 的值將偏向於加權 ARTXP。 趨近於 1 的值將偏向於加權 ARIMA。|  
|SAMPLE_SIZE|Microsoft 群集演算法|指定如果 CLUSTERING_METHOD 參數設定為可擴充的其中一個群集方法時，演算法在每個行程上使用的案例數目。 將 SAMPLE_SIZE 參數設定為 0 會導致整個資料集群集在單一行程中。 這樣會造成記憶體和效能的問題。<br /><br /> 預設值是 50000。|  
|SAMPLE_SIZE|Microsoft 羅吉斯迴歸演算法<br /><br /> Microsoft Neural Network Algorithm|指定用來定型模型的案例數目。 此演算法提供者會使用此數字或不包括在鑑效組百分比 (由 HOLDOUT_PERCENTAGE 參數指定) 中的總案例數百分比，以較小者為準。<br /><br /> 換句話說，如果 HOLDOUT_PERCENTAGE 設定為 30，則演算法將使用此參數的值，或等於總案例數 70% 的值，以較小者為準。<br /><br /> 預設值是 10000。|  
|SCORE_METHOD|Microsoft 決策樹演算法|決定用來計算分岔準則的方法。 可用的選項如下：(1) Entropy、(2) Bayesian with K2 Prior 或 (3) Bayesian Dirichlet Equivalent (BDE) Prior。<br /><br /> 預設值是 3。|  
|SPLIT_METHOD|Microsoft 決策樹演算法|決定用來分岔節點的方法。 可用的選項如下：二元分岔 (1)、完整分岔 (2) 或根據演算法判斷 (3)。<br /><br /> 預設值是 3。|  
|STOPPING_TOLERANCE|Microsoft 群集演算法技術參考|指定用來決定何時到達聚合以及演算法完成模型建立的值。 當群集機率的整體變更小於 STOPPING_TOLERANCE 參數除以模型大小的比率時，就到達聚合。<br /><br /> 預設值是 10。|  
  
### <a name="comments"></a>註解  
 如需有關演算法的詳細資料，請參閱《SQL Server 線上叢書》。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法&#40;SQL Server 資料採礦增益集&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md)  
  
  
