---
title: "Algorithm 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Algorithm Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Algorithm
helpviewer_keywords:
- Algorithm element
ms.assetid: 188bf7ce-c5c9-406a-af75-5a026c92a569
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1fe1a9caffdff1de0dc62c4ddd696e1ec8b829bd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="algorithm-element-assl"></a>Algorithm 元素 (ASSL)
  定義所使用的演算法[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningModel>  
      ...  
   <Algorithm>...</Algorithm>  
      ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值**演算法**項目是可識別演算法的字串。 例如，此字串可能是*Microsoft_Naive_Bayes*， *Microsoft_Decision_Trees*，或*Microsoft_Clustering。* 此字串會識別所提供的演算法[!INCLUDE[msCoName](../../../includes/msconame-md.md)]和自訂的使用者所提供的演算法。 可用的值**演算法**可從的 SERVICE_NAME 資料行擷取的項目[DMSCHEMA_MINING_SERVICES](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)結構描述資料列。  
  
 對應目的父代的項目**演算法**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.MiningModel>。 在 AMO 物件模型中緊密相關的元素是 <xref:Microsoft.AnalysisServices.MiningModelAlgorithms>。  
  
## <a name="see-also"></a>另請參閱  
 [AlgorithmParameter 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)   
 [AlgorithmParameters 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/algorithmparameters-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

