---
description: 群集 (DMX)
title: 叢集 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0722e53752cfa01ffee086cb8cf1f6a84f82fd4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457840"
---
# <a name="cluster-dmx"></a>群集 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  傳回最可能包含輸入案例的群集。  
  
## <a name="syntax"></a>語法  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>套用至  
 唯有基礎資料採礦模型支援群集時，才能使用這個函數。  
  
## <a name="return-type"></a>傳回類型  
 **Cluster**函數不需要參數。  
  
 **Cluster**函數會傳回叢集名稱的純量值。 但是，如果您使用此函式作為其他函式的引數，您必須將它視為 \<cluster column reference> 。  
  
## <a name="remarks"></a>備註  
 叢集**也可以當做**PredictHistogram 函數的叢集資料 `<` 行參考 `>` 。 **PredictHistogram**  
  
## <a name="examples"></a>範例  
 下列範例會使用具有 [PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md) 和叢集函式的單一查詢，從 TM 叢集的每個叢集採礦模型的每個叢集，以及個別案例存在於每個叢集中的機率傳回個別案例的距離。  
  
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
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數 ](../dmx/general-prediction-functions-dmx.md)  
  
  
