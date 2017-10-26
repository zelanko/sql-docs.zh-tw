---
title: "PredictHistogram (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PredictHistogram
dev_langs:
- DMX
helpviewer_keywords:
- PredictHistogram function
ms.assetid: 85ffc542-96e7-4f58-aaa3-34d76befcedf
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2e0d45b8169d567bbdc69a916f242b2707f6570
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="predicthistogram-dmx"></a>PredictHistogram (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 長條圖產生統計資料行。 傳回之長條圖的資料行結構相依於搭配使用的資料行參考的型別**PredictHistogram**函式。  
  
## <a name="scalar-columns"></a>純量資料行  
 如\<純量資料行參考 >，長條圖， **PredictHistogram**函式會傳回下列資料行所組成：  
  
-   所預測的值。  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]不支援資料採礦演算法**$ProbabilityVariance**。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 演算法的這個資料行一律包含 0。  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]不支援資料採礦演算法**$ProbabilityStdev**。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 演算法的這個資料行一律包含 0。  
  
-   **$AdjustedProbability**  
  
     **$AdjustedProbability**資料行是[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]延伸[!INCLUDE[msCoName](../includes/msconame-md.md)]OLE DB for Data Mining 規格。  
  
## <a name="cluster-columns"></a>群集資料行  
 長條圖， **PredictHistogram**函式會傳回\<叢集資料行參考 > 包含下列資料行：  
  
-   **$Cluster** （代表群集名稱）  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>範例  
 下列範例在單一查詢中傳回 Bike Buyer 資料行的預測狀態。 此查詢也會傳回 Bike Buyer 屬性，根據使用取得的已調整機率的前兩個最可能狀態**PredictHistogram**函式。  
  
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
 [叢集 &#40; DMX &#41;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40; DMX &#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40; DMX &#41;](../dmx/predictadjustedprobability-dmx.md)   
 [[Predictprobability] &#40; DMX &#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40; DMX &#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40; DMX &#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40; DMX &#41;](../dmx/predictvariance-dmx.md)   
 [資料採礦演算法 &#40;Analysis Services-資料採礦 &#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

