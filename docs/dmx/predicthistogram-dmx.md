---
title: PredictHistogram (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7e7129985eac09d741ea9d00c551a9507ee92c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62659170"
---
# <a name="predicthistogram-dmx"></a>PredictHistogram (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回表示給定資料行的預測長條圖的資料表。  
  
## <a name="syntax"></a>語法  
  
```  
  
PredictHistogram(<scalar column reference> | <cluster column reference>)  
```  
  
## <a name="applies-to"></a>適用於  
 純量資料行參考或群集資料行參考。 可以搭配 [!INCLUDE[msCoName](../includes/msconame-md.md)] 關聯分析演算法之外的所有演算法使用。  
  
## <a name="return-type"></a>傳回類型  
 資料表。  
  
## <a name="remarks"></a>備註  
 長條圖產生統計資料行。 傳回之長條圖的資料行結構而定，可搭配資料行參考的型別**PredictHistogram**函式。  
  
## <a name="scalar-columns"></a>純量資料行  
 針對\<純量資料行參考 >，長條圖， **PredictHistogram**函式會傳回包含下列資料行：  
  
-   所預測的值。  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] 不支援資料採礦演算法 **$ProbabilityVariance**。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 演算法的這個資料行一律包含 0。  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] 不支援資料採礦演算法 **$ProbabilityStdev**。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 演算法的這個資料行一律包含 0。  
  
-   **$AdjustedProbability**  
  
     **$AdjustedProbability**資料行是[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]擴充功能來[!INCLUDE[msCoName](../includes/msconame-md.md)]OLE DB for Data Mining 規格。  
  
## <a name="cluster-columns"></a>群集資料行  
 長條圖可**PredictHistogram**函式會傳回\<叢集資料行參考 > 包含下列資料行：  
  
-   **$Cluster** （代表叢集名稱）  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>範例  
 下列範例在單一查詢中傳回 Bike Buyer 資料行的預測狀態。 此查詢也會傳回 Bike Buyer 屬性，以取得使用的已調整機率的前兩個最可能狀態**PredictHistogram**函式。  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  TopCount(PredictHistogram([Bike Buyer]),$AdjustedProbability,3)  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>另請參閱  
 [叢集&#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)   
 [PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)   
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [資料採礦延伸模組&#40;DMX&#41;函式參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
