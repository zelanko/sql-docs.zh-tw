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
ms.openlocfilehash: fdc63d1c93d1290c701233cb94f71f157c771182
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893854"
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
 長條圖產生統計資料行。 傳回之長條圖的資料行結構, 取決於搭配**PredictHistogram**函數使用的資料行參考類型。  
  
## <a name="scalar-columns"></a>純量資料行  
 如需純量資料行參考 >, PredictHistogram 函數傳回的長條圖包含下列資料行: \<  
  
-   所預測的值。  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]資料採礦演算法不支援 **$ProbabilityVariance**。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 演算法的這個資料行一律包含 0。  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]資料採礦演算法不支援 **$ProbabilityStdev**。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 演算法的這個資料行一律包含 0。  
  
-   **$AdjustedProbability**  
  
     [ **$AdjustedProbability** ] 資料行[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]是適用于[!INCLUDE[msCoName](../includes/msconame-md.md)]資料採礦規格之 OLE DB 的延伸模組。  
  
## <a name="cluster-columns"></a>群集資料行  
 **PredictHistogram**函數針對\<叢集資料行參考所傳回的長條圖 > 由下列資料行所組成:  
  
-   **$Cluster**(代表叢集名稱)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>範例  
 下列範例在單一查詢中傳回 Bike Buyer 資料行的預測狀態。 此查詢也會根據使用**PredictHistogram**函數所取得的調整機率, 傳回自行車購買者屬性的前兩個最可能狀態。  
  
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
 [[Predictprobability] &#40;DMX&#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)   
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [資料採礦延伸&#40;模組&#41; DMX 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函數&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
