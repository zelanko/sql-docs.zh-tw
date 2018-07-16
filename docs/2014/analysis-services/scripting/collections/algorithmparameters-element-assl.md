---
title: AlgorithmParameters 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- AlgorithmParameters Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AlgorithmParameters
helpviewer_keywords:
- AlgorithmParameters element
ms.assetid: 240cbb60-7fa3-46ef-b5be-cd14c9ec10de
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3ab357b16b8b10b13d3ddb23b2a2bc1e7a32c486
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330428"
---
# <a name="algorithmparameters-element-assl"></a>AlgorithmParameters 元素 (ASSL)
  包含所使用之演算法參數的集合[MiningModel](../objects/miningmodel-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningModel>  
   ...  
   <AlgorithmParameters>  
      <AlgorithmParameter>...</AlgorithmParameter>  
   </AlgorithmParameters>  
   ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無 (集合)|  
|預設值|無 (集合)|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModel](../objects/miningmodel-element-assl.md)|  
|子元素|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 `AlgorithmParameters` 集合包含採礦模型演算法的可擴充參數集合 (以名稱/值組表示)。 適用的參數集合視演算法而定。 如需有關給定演算法之演算法參數的詳細資訊，請參閱該演算法的適當文件。  
  
 您可以從 DMSCHEMA_MINING_SERVICE_PARAMETERS 結構描述資料列中擷取可用的演算法參數，包括驗證和顯示資訊。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.AlgorithmParameterCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [Algorithm 元素&#40;ASSL&#41;](../properties/algorithm-element-assl.md)   
 [DMSCHEMA_MINING_SERVICE_PARAMETERS 資料列集](../../schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
