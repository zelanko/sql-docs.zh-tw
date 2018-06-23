---
title: Algorithm 元素 (ASSL) |Microsoft 文件
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
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 86e44cf8069d9ed78a414cad5ac5079f8f2faa22
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135485"
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
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModel](../objects/miningmodel-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `Algorithm` 元素的值是可識別演算法的字串。 例如，此字串可能是*Microsoft_Naive_Bayes*， *Microsoft_Decision_Trees*，或*Microsoft_Clustering。* 此字串會識別所提供的演算法[!INCLUDE[msCoName](../../../includes/msconame-md.md)]和自訂的使用者所提供的演算法。 可用的值`Algorithm`可從的 SERVICE_NAME 資料行擷取的項目[DMSCHEMA_MINING_SERVICES](../../schema-rowsets/data-mining/dmschema-mining-services-rowset.md)結構描述資料列。  
  
 對應目的父代的項目`Algorithm`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.MiningModel>。 在 AMO 物件模型中緊密相關的元素是 <xref:Microsoft.AnalysisServices.MiningModelAlgorithms>。  
  
## <a name="see-also"></a>另請參閱  
 [AlgorithmParameter 元素&#40;ASSL&#41;](../objects/algorithmparameter-element-assl.md)   
 [AlgorithmParameters 元素&#40;ASSL&#41;](../collections/algorithmparameters-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  