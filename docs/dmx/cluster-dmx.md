---
title: 叢集（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fa7df2782b8102e386c70d5e874a25f7868dbb1c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68071084"
---
# <a name="cluster-dmx"></a>群集 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回最可能包含輸入案例的群集。  
  
## <a name="syntax"></a>語法  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>套用至  
 唯有基礎資料採礦模型支援群集時，才能使用這個函數。  
  
## <a name="return-type"></a>傳回類型  
 **Cluster**函數不需要參數。  
  
 叢集**函數會**傳回純量值的叢集名稱。 不過，如果您使用此函數做為另一個函式的引數，則必須將\<它視為叢集資料行參考>。  
  
## <a name="remarks"></a>備註  
 叢集**也可以當做**PredictHistogram 函數的`<`叢集資料行`>`參考使用**PredictHistogram** 。  
  
## <a name="examples"></a>範例  
 下列範例會使用具有[PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md)和叢集函式的單一查詢，從 TM 叢集處理模型的每個叢集傳回個別案例的距離，以及在每個叢集中存在個別案例的機率。  
  
```  
SELECT  
  PredictHistogram(Cluster())  
FROM  
  [TM Clustering]  
  NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>另請參閱  
 [DMX&#41;的 ClusterProbability &#40;](../dmx/clusterprobability-dmx.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;的函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)  
  
  
