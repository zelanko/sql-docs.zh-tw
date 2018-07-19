---
title: 群集 (DMX) |Microsoft 文件
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 41f835a93e5976945281b6b04258c516b0322236
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841301"
---
# <a name="cluster-dmx"></a>群集 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回最可能包含輸入案例的群集。  
  
## <a name="syntax"></a>語法  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>適用於  
 唯有基礎資料採礦模型支援群集時，才能使用這個函數。  
  
## <a name="return-type"></a>傳回類型  
 **叢集**函式不需要參數。  
  
 **叢集**函式會傳回純量值的叢集名稱。 不過，如果您使用此函式為另一個函式的引數時，您必須將它做為\<叢集資料行參考 >。  
  
## <a name="remarks"></a>備註  
 **叢集**也可用來當作`<`叢集資料行參考`>`如**PredictHistogram**函式。  
  
## <a name="examples"></a>範例  
 下列範例會使用單一查詢及[PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md)和叢集函式來傳回 TM Clustering 採礦模型的每一個叢集中的個別案例的距離，個別的案例會存在於每個群集的機率。  
  
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
 [資料採礦延伸模組&#40;DMX&#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
