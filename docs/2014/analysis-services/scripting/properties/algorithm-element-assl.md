---
title: Algorithm 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Algorithm Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Algorithm
helpviewer_keywords:
- Algorithm element
ms.assetid: 188bf7ce-c5c9-406a-af75-5a026c92a569
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9fb2ab30f6abd753f0c954ef41ad26d0af9dcda8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149778"
---
# <a name="algorithm-element-assl"></a>Algorithm 元素 (ASSL)
  定義所使用的演算法[MiningModel](../objects/miningmodel-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningModel>  
      ...  
   <Algorithm>...</Algorithm>  
      ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModel](../objects/miningmodel-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `Algorithm` 元素的值是可識別演算法的字串。 例如，此字串可能是*Microsoft_Naive_Bayes*， *Microsoft_Decision_Trees*，或*Microsoft_Clustering。* 此字串會識別所提供的演算法[!INCLUDE[msCoName](../../../includes/msconame-md.md)]和自訂的使用者所提供的演算法。 可用的值，如`Algorithm`項目可以擷取從的 SERVICE_NAME 資料行[DMSCHEMA_MINING_SERVICES](../../schema-rowsets/data-mining/dmschema-mining-services-rowset.md)結構描述資料列。  
  
 對應至父系的元素`Algorithm`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.MiningModel>。 在 AMO 物件模型中緊密相關的元素是 <xref:Microsoft.AnalysisServices.MiningModelAlgorithms>。  
  
## <a name="see-also"></a>另請參閱  
 [AlgorithmParameter 元素&#40;ASSL&#41;](../objects/algorithmparameter-element-assl.md)   
 [AlgorithmParameters 元素&#40;ASSL&#41;](../collections/algorithmparameters-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
