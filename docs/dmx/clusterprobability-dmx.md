---
title: "ClusterProbability (DMX) |Microsoft 文件"
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
- ClusterProbability
dev_langs:
- DMX
helpviewer_keywords:
- ClusterProbability function
ms.assetid: a6447b3c-94ce-4122-a3eb-6f3827598d8f
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b7f68000caa8fd90dd2a2396ff17f0fd701b96d2
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="clusterprobability-dmx"></a>ClusterProbability (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回輸入案例屬於指定之群集的機率。  
  
## <a name="syntax"></a>語法  
  
```  
  
ClusterProbability([<Node_Caption>])  
```  
  
## <a name="applies-to"></a>適用於  
 唯有基礎資料採礦模型支援群集時，才能使用這個函數。  
  
## <a name="return-type"></a>傳回類型  
 純量值。  
  
## <a name="remarks"></a>備註  
 下列語法使用採礦模型內容結構描述資料列集，傳回採礦模型中存在的節點標題。  
  
```  
SELECT NODE_CAPTION FROM <model>.CONTENT  
```  
  
 如需有關使用此語法的詳細資訊，請參閱[SELECT FROM &#60; 模式 &#62;。內容 &#40; DMX &#41;](../dmx/select-from-model-content-dmx.md). 如需有關採礦模型內容結構描述資料列集的詳細資訊，請參閱[DMSCHEMA_MINING_MODEL_CONTENT 資料列集](../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)。  
  
 如果\<節點標題 > 未指定，則函數會傳回輸入的案例屬於最可能的群集的機率。 使用**叢集**函數來傳回最可能的群集。  
  
## <a name="examples"></a>範例  
 下列範例傳回指定的案例存在標示為 Cluster 2 之叢集內的機率。  
  
```  
SELECT  
  ClusterProbability('Cluster 2')  
From  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>另請參閱  
 [叢集 &#40; DMX &#41;](../dmx/cluster-dmx.md)   
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

