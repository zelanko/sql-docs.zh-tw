---
title: "群集 (DMX) |Microsoft 文件"
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
- Cluster
dev_langs:
- DMX
helpviewer_keywords:
- Cluster function
ms.assetid: 14b2942a-6dec-4dfa-98a6-697a3c89036a
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 65e0d6942d48657f99d5cff3365a80d4853c66d4
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="cluster-dmx"></a>群集 (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 下列範例會使用單一查詢及[PredictHistogram &#40; DMX &#41;](../dmx/predicthistogram-dmx.md)和叢集函式來傳回 TM Clustering 採礦模型和個別的案例會存在於每個群集的機率的每一個叢集中的個別案例的距離。  
  
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
 [ClusterProbability &#40; DMX &#41;](../dmx/clusterprobability-dmx.md)   
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

