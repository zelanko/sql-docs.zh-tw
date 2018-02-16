---
title: "類神經網路模型查詢範例 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- neural network algorithms [Analysis Services]
- content queries [DMX]
- neural network model [Analysis Services]
ms.assetid: 81b06183-620f-4e0c-bc10-532e6a1f0829
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 531380e732ea9e2f390328fe22310ba844a8bc57
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="neural-network-model-query-examples"></a>Neural Network Model Query Examples
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
當您針對資料採礦模型建立查詢時，可以建立內容查詢來提供有關分析期間所發現之模式的詳細資料，或是建立預測查詢來使用模型中的模式，為新的資料進行預測。 例如，類神經網路模型的內容查詢可以擷取模型中繼資料，例如，隱藏層的數目。 或者，預測查詢可以根據輸入建議分類，並選擇性地提供每個分類的機率。  
  
 本節說明如何針對以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法為基礎的模型來建立查詢。  
  
 **內容查詢**  
  
 [使用 DMX 取得模型中繼資料](#bkmk_Query1)  
  
 [從結構描述資料列集擷取模型中繼資料](#bkmk_Query2)  
  
 [擷取模型的輸入屬性](#bkmk_Query3)  
  
 [從隱藏層擷取加權](#bkmk_Query4)  
  
 **預測查詢**  
  
 [建立單一預測](#bkmk_Query5)  
  
## <a name="finding-information-about-a-neural-network-model"></a>尋找有關類神經網路模型的資訊  
 所有的採礦模型都會公開演算法根據標準化結構描述所學習的內容，也就是採礦模型結構描述資料列集。 此資訊提供關於模型的詳細資料，而且包含基本中繼資料、分析期間所發現的結構，以及處理時所使用的參數。 您可以藉由使用資料採礦延伸模組 (DMX) 陳述式來針對模型內容建立查詢。  
  
###  <a name="bkmk_Query1"></a> 範例查詢 1：使用 DMX 取得模型中繼資料  
 下列查詢會傳回使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法建立之模型的相關基本中繼資料。 在類神經網路模型中，模型的父節點僅包含模型的名稱、模型儲存位置所在資料庫的名稱，以及子節點的數目。 不過，臨界統計資料節點 (NODE_TYPE = 24) 會提供關於模型中使用之輸入資料行的這個基本中繼資料，以及一些衍生的統計資料。  
  
 下列範例查詢是以您在＜ [中繼資料採礦教學課程](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b)＞中建立的採礦模型為基礎，名稱為 `Call Center Default NN`。 此模型使用來自撥接中心的資料，探索人員雇用以及電話通數、訂單數與問題數之間可能的關聯。 DMX 陳述式會從類神經網路模型的臨界統計資料節點擷取資料。 此查詢包含 FLATTENED 關鍵字，因為感興趣的輸入屬性統計資料會儲存在 NODE_DISTRIBUTION 巢狀資料表中。 不過，如果您的查詢提供者支援階段式資料列集，您就不需要使用 FLATTENED 關鍵字。  
  
```  
SELECT FLATTENED MODEL_CATALOG, MODEL_NAME,   
(    SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
     [SUPPORT], [PROBABILITY], VALUETYPE   
     FROM NODE_DISTRIBUTION  
) AS t  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 24  
```  
  
> [!NOTE]  
>  您必須將巢狀資料表資料行 SUPPORT 和 PROBABILITY 的名稱括在括弧內，以便與同名的保留關鍵字區別。  
  
 範例結果：  
  
|MODEL_CATALOG|MODEL_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|--------------------|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|Adventure Works DW Multidimensional 2012|撥接中心 NN|每個問題的平均時間|遺漏|0|0|1|  
|Adventure Works DW Multidimensional 2012|撥接中心 NN|每個問題的平均時間|< 64.7094100096|11|0.407407407|5|  
  
 如需結構描述資料列集中的資料行在類神經網路模型環境中代表的定義，請參閱 [類神經網路模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)。  
  
###  <a name="bkmk_Query2"></a> 範例查詢 2：從結構描述資料列集擷取模型中繼資料  
 您可以藉由查詢資料採礦結構描述資料列集，找到與 DMX 內容查詢所傳回的相同資訊。 不過，結構描述資料列集會提供某些額外的資料行。 下列範例查詢會傳回建立模型的日期、修改日期以及上次處理模型的日期。 此查詢也會傳回不易從模型內容取得的可預測資料行，以及建立模型所使用的參數。 這項資訊對於記錄模型可能相當實用。  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center Default NN'  
```  
  
 範例結果：  
  
|||  
|-|-|  
|MODEL_NAME|撥接中心預設 NN|  
|DATE_CREATED|1/10/2008 5:07:38 PM|  
|LAST_PROCESSED|1/10/2008 5:24:02 PM|  
|PREDICTION_ENTITY|每個問題的平均時間，<br /><br /> 服務等級，<br /><br /> 訂單數目|  
|MINING_PARAMETERS|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=0,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100, SAMPLE_SIZE=10000, HIDDEN_NODE_RATIO=4|  
  
###  <a name="bkmk_Query3"></a> 範例查詢 3：擷取模型的輸入屬性  
 您可以查詢輸入層 (NODE_TYPE = 18) 的子節點 (NODE_TYPE = 20)，擷取建立模型所使用的輸入屬性和值的配對。 下列查詢會從節點描述傳回輸入屬性的清單。  
  
```  
SELECT NODE_DESCRIPTION  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 範例結果：  
  
|NODE_DESCRIPTION|  
|-----------------------|  
|每個問題的平均時間=64.7094100096 - 77.4002099712|  
|週中的日=Fri.|  
|層級 1 運算子|  
  
 結果中只有少數代表性的資料列會顯示在此處。 不過，您可以發現，根據輸入屬性的資料類型，NODE_DESCRIPTION 會提供稍微不同的資訊。  
  
-   如果屬性是離散值或離散化的值，則會傳回屬性及其值或其離散化的範圍。  
  
-   如果屬性為連續的數值資料類型，則 NODE_DESCRIPTION contains 僅包含屬性名稱。 不過，您可以擷取 NODE_DISTRIBUTION 巢狀資料表以取得平均值，或傳回 NODE_RULE 以取得數值範圍的最小值與最大值。  
  
 下列查詢顯示如何查詢 NODE_DISTRIBUTION 巢狀資料表，以便在一個資料行中傳回屬性，並在另一個資料行中傳回其值。 若是連續屬性，屬性值會以其平均值表示。  
  
```  
SELECT FLATTENED   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE  
FROM NODE_DISTRIBUTION) as t  
FROM [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 21  
```  
  
 範例結果：  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|-----------------------|------------------------|  
|每個問題的平均時間|64.7094100096 - 77.4002099712|  
|週中的日|Fri.|  
|層級 1 運算子|3.2962962962963|  
  
 最小與最大範圍值會儲存在 NODE_RULE 資料行中，而且會以 XML 片段表示，如下列範例所示：  
  
```  
<NormContinuous field="Level 1 Operators">    
  <LinearNorm orig="2.83967303681711" norm="-1" />    
  <LinearNorm orig="3.75291955577548" norm="1" />    
</NormContinuous>    
```  
  
###  <a name="bkmk_Query4"></a> 範例查詢 4：從隱藏層擷取加權  
 類神經網路模型的模型內容結構化的方式可以讓網路中任何節點之詳細資料的擷取更為容易。 此外，節點識別碼提供的資訊可協助您識別節點類型之間的關聯性。  
  
 下列查詢示範如何擷取儲存在隱藏層特定節點下的係數。 隱藏層由僅包含中繼資料的組合管理節點 (NODE_TYPE = 19)，以及包含各種屬性和值組合之係數的多個子節點 (NODE_TYPE = 22) 所組成。 此查詢僅傳回係數節點。  
  
```  
SELECT FLATTENED TOP 1 NODE_UNIQUE_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM  [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 22  
AND [PARENT_UNIQUE_NAME] = '40000000200000000' FROM [Call Center Default NN].CONTENT  
```  
  
 範例結果：  
  
|NODE_UNIQUE_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|------------------------|-----------------------|------------------------|-----------------|  
|70000000200000000|6000000000000000a|-0.178616518|7|  
|70000000200000000|6000000000000000b|-0.267561918|7|  
|70000000200000000|6000000000000000c|0.11069497|7|  
|70000000200000000|6000000000000000d|0.123757712|7|  
|70000000200000000|6000000000000000e|0.294565343|7|  
|70000000200000000|6000000000000000f|0.22245318|7|  
|70000000200000000||0.188805045|7|  
  
 此處顯示的部分結果示範類神經網路模型內容如何讓隱藏節點與輸入節點相關聯。  
  
-   節點在隱藏層中的唯一名稱永遠以 70000000 做為開頭。  
  
-   節點在輸入層中的唯一名稱永遠以 60000000 做為開頭。  
  
 因此，這些結果會告訴您，已經有六個不同的係數 (VALUETYPE = 7) 傳遞給以識別碼 70000000200000000 表示的節點， 這些係數的值位於 ATTRIBUTE_VALUE 資料行中。 您可以使用 ATTRIBUTE_NAME 資料行中的節點識別碼，正確地判斷此係數用於哪個輸入屬性。 例如，節點識別碼 6000000000000000a 表示輸入屬性及值 `Day of Week = 'Tue.'` 。您可以使用節點識別碼來建立查詢，或者可以使用 [Microsoft 一般內容樹狀檢視器](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)瀏覽到該節點。  
  
 同樣地，如果您在輸出層 layer (NODE_TYPE = 23) 中查詢節點的 NODE_DISTRIBUTION 資料表，您可以看到每個輸出值的係數。 不過，在輸出層中，這些指標會回頭參考隱藏層的節點。 如需詳細資訊，請參閱 [類神經網路模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)。  
  
## <a name="using-a-neural-network-model-to-make-predictions"></a>使用類神經網路模型進行預測  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法同時支援分類與迴歸。 您可以搭配這些模型使用預測函數來提供新的資料，並建立單一或批次預測。  
  
###  <a name="bkmk_Query5"></a> 範例查詢 5：建立單一預測  
 在類神經網路模型上建立預測查詢最簡單的方式就是使用預測查詢產生器 (可在 **和** 中，資料採礦設計師的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [採礦預測] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]索引標籤上取得)。 您可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路檢視器中瀏覽模型來篩選感興趣的屬性並檢視趨勢，然後切換到 **[採礦預測]** 索引標籤來建立查詢，並針對這些趨勢預測新的值。  
  
 例如，您可以瀏覽撥接中心模型來檢視訂單量與其他屬性間的關聯。 若要這樣做，開啟模型，檢視器中，而且**輸入**，選取**\<所有 >**。  接著，為 **[輸出]**選取 **[訂單數目]**。 為 **[值 1]**選取代表最多訂單的範圍，並為 **[值 2]**選取代表最少訂單的範圍。 然後，您可以看一下模型與訂單量關聯的所有屬性。  
  
 透過瀏覽檢視器中的結果，您會發現一週的某幾天訂單量較低，而運算子數目的增加似乎與較高的銷售量互相關聯。 接著，您可以在模型上使用預測查詢來測試 "what if" 假設，並詢問在訂單量低的天數上增加層級 2 運算子的數目是否會增加訂單。 若要這樣做，建立如下的查詢：  
  
```  
SELECT Predict([Call Center Default NN].[Number of Orders]) AS [Predicted Orders],  
PredictProbability([Call Center Default NN].[Number of Orders]) AS [Probability]  
FROM [Call Center Default NN]  
NATURAL PREDICTION JOIN   
(SELECT 'Tue.' AS [Day of Week],  
13 AS [Level 2 Operators]) AS t  
```  
  
 範例結果：  
  
|預測的訂單|機率|  
|----------------------|-----------------|  
|364|0.9532…|  
  
 預測的銷售量高於目前星期二的銷售量範圍，而且預測的機率相當高。 不過，您可能想要使用批次處理測試模型的各種假設，藉以建立多個預測。  
  
> [!NOTE]  
>  適用於 Excel 2007 的資料採礦增益集提供羅吉斯迴歸精靈，讓您輕鬆回應複雜的問題，例如，需要多少位二級操作員，才能將某個排班的服務等級提升至目標等級。 您可以免費下載資料採礦增益集，其中包含類神經網路和/或羅吉斯迴歸演算法的精靈。 如需詳細資訊，請參閱 [適用於 Office 2007 的資料採礦增益集](http://go.microsoft.com/fwlink/?LinkID=117790) 網站。  
  
## <a name="list-of-prediction-functions"></a>預測函數的清單  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法都支援一組常用的函數。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法沒有專用的預測函數，不過，此演算法支援下表所列出的函數。  
  
|||  
|-|-|  
|預測函數|使用方式|  
|[IsDescendant &#40; DMX &#41;](../../dmx/isdescendant-dmx.md)|確定某個節點是否為類神經網路圖中另一個節點的子系。|  
|[PredictAdjustedProbability &#40; DMX &#41;](../../dmx/predictadjustedprobability-dmx.md)|傳回加權機率。|  
|[PredictHistogram &#40; DMX &#41;](../../dmx/predicthistogram-dmx.md)|傳回與目前預測值相關之值的資料表。|  
|[PredictVariance &#40;DMX&#41;](../../dmx/predictvariance-dmx.md)|傳回預測值的變異數。|  
|[[Predictprobability] &#40; DMX &#41;](../../dmx/predictprobability-dmx.md)|傳回預測值的機率。|  
|[PredictStdev &#40; DMX &#41;](../../dmx/predictstdev-dmx.md)|傳回預測值的標準差。|  
|[PredictSupport &#40; DMX &#41;](../../dmx/predictsupport-dmx.md)|若是類神經網路與羅吉斯迴歸模型，則會傳回代表整個模型之定型集大小的單一值。|  
  
 如需所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法共用之函數的清單，請參閱[演算法參考 (Analysis Services - 資料採礦)](https://technet.microsoft.com/library/bb895228\(v=sql.105\).aspx)。 如需特定函數的語法，請參閱[資料採礦延伸模組 &#40;DMX&#41; 函數參考](../../dmx/data-mining-extensions-dmx-function-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 類神經網路演算法](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [Microsoft 類神經網路演算法技術參考](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [類神經網路模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [第 5 課： 建立類神經網路和羅吉斯迴歸模型 &#40; 中繼資料採礦教學課程 &#41;](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b)  
  
  
