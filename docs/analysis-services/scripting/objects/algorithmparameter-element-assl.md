---
title: "AlgorithmParameter 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AlgorithmParameter Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AlgorithmParameter
helpviewer_keywords: AlgorithmParameter element
ms.assetid: 73211495-065c-43c6-a486-be6044617263
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 73fd9b4b96ea774eaf352bddf7bab1fb143f1bf4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="algorithmparameter-element-assl"></a>AlgorithmParameter 元素 (ASSL)
  定義所使用之演算法參數[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AlgorithmParameters>  
   <AlgorithmParameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </AlgorithmParameter>  
</AlgorithmParameters>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AlgorithmParameters](../../../analysis-services/scripting/collections/algorithmparameters-element-assl.md)|  
|子元素|[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)，[值](../../../analysis-services/scripting/properties/value-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 **AlgorithmParameter**是採礦模型演算法的參數。 **AlgorithmParameter**這個參數表示成名稱/值組。 適用的參數集合的**AlgorithmParameter**可以代表會視演算法而定。 如需有關給定演算法之演算法參數的詳細資訊，請參閱該演算法的適當文件。  
  
 可用的演算法參數，包括驗證和顯示的資訊，可以從擷取[DMSCHEMA_MINING_SERVICE_PARAMETERS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)結構描述資料列。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.AlgorithmParameter>。  
  
## <a name="see-also"></a>請參閱＜  
 [MiningModel 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)   
 [Algorithm 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/algorithm-element-assl.md)   
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
