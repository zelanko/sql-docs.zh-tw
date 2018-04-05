---
title: ClusterDistance (DMX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ClusterDistance
dev_langs:
- DMX
helpviewer_keywords:
- ClusterDistance function
ms.assetid: a13152b3-4cd1-4c79-8a3e-207624198330
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 0a3f0d8b9167a399249cce2183b5a03ae0995473
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="clusterdistance-dmx"></a>ClusterDistance (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **ClusterDistance**函式會傳回輸入案例的距離，從指定的叢集，或如果沒有指定任何群集，輸入案例與最可能的群集的距離。  
  
## <a name="syntax"></a>語法  
  
```  
  
ClusterDistance([<ClusterID expression>])  
```  
  
## <a name="applies-to"></a>適用於  
 唯有基礎資料採礦模型支援群集時，才能使用這個函數。 此函數可以搭配任何種類的群集模型 (EM、K-Means 等等) 使用，但是結果會隨著演算法而有所不同。  
  
## <a name="return-type"></a>傳回類型  
 純量值。  
  
## <a name="remarks"></a>備註  
 **ClusterDistance**函式會傳回輸入的案例與輸入案例機率最高的叢集之間的距離。  
  
 如果是 K-Means 群集，由於任何案例都可能僅屬於一個群集，而且成員資格加權為 1.0，則群集距離永遠為 0。 不過，在 K-Means 中，系統會假設每個群集都有一個距心。 您可以在採礦模型內容中，查詢或瀏覽 NODE_DISTRIBUTION 巢狀資料表來取得距心的值。 如需詳細資訊，請參閱[叢集模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)。  
  
 如果是預設的 EM 群集方法，群集內部所有的點都會被視為可能性相等，因此，根據設計，沒有用於群集的距心。 值**ClusterDistance**特定案例與特定群集之間*N*的計算方式如下：  
  
 ClusterDistance(N) =1–(membershipWeight(N))  
  
 或：  
  
 ClusterDistance(N) = 1 – ClusterProbability (N))  
  
## <a name="related-prediction-functions"></a>相關的預測函數  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供下列額外的函數來查詢群集模型：  
  
-   使用[叢集 &#40; DMX &#41;](../dmx/cluster-dmx.md)函數來傳回最可能的群集。  
  
-   使用[ClusterProbability &#40; DMX &#41;](../dmx/clusterprobability-dmx.md)函式可取得案例屬於特定群集的機率。 這個值會當做群集距離的反向。  
  
-   使用[PredictHistogram &#40; DMX &#41;](../dmx/predicthistogram-dmx.md)函數來傳回輸入案例存在於每個模型的群集的可能性的長條圖。  
  
-   使用[PredictCaseLikelihood &#40; DMX &#41;](../dmx/predictcaselikelihood-dmx.md)函式傳回 0 到 1 表示輸入的案例可能性的量值為模型存在於透過演算法取得。  
  
## <a name="example1-obtaining-cluster-distance-to-the-most-likely-cluster"></a>範例 1：取得最可能之群集的群集距離  
 下列範例會傳回指定之案例與該案力最可能所屬之群集間的距離。  
  
```  
SELECT  
    ClusterDistance()  
FROM  
    [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 範例結果：  
  
|運算式|  
|----------------|  
|0.0477390930705145|  
  
 若要找出這是哪個群集，您可以將 `Cluster` 替代為先前範例中的 `ClusterDistance`。  
  
 範例結果：  
  
|$CLUSTER|  
|--------------|  
|叢集 6|  
  
## <a name="example2-obtaining-distance-to-a-specified-cluster"></a>範例 2：取得指定之群集的距離  
 下列語法使用採礦模型內容結構描述資料列集，傳回節點識別碼的清單，以及採礦模型中之群集的節點標題。 然後您可以使用節點標題中的群集識別碼引數為**ClusterDistance**函式。  
  
```  
SELECT NODE_UNIQUE_NAME, NODE_CAPTION   
FROM <model>.CONTENT   
WHERE NODE_TYPE = 5  
```  
  
 範例結果：  
  
|NODE_UNIQUE_NAME|NODE_CAPTION|  
|------------------------|-------------------|  
|001|叢集 1|  
|002|群集 2|  
  
 下列語法範例會傳回指定之案例與標示為 Cluster 2 之叢集間的距離。  
  
```  
SELECT  
    ClusterDistance('Cluster 2')  
AS [Cluster 2 Distance]  
FROM [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 範例結果：  
  
|Cluster 2 Distance|  
|------------------------|  
|0.97008209236394|  
  
## <a name="see-also"></a>請參閱  
 [叢集 &#40; DMX &#41;](../dmx/cluster-dmx.md)   
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [叢集模型 &#40; 採礦模型內容Analysis Services-資料採礦 &#41;](../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
  
