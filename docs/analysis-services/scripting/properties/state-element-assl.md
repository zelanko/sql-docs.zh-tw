---
title: 狀態元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- State Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- State
helpviewer_keywords:
- State element
ms.assetid: b6ee1144-89f7-4ced-bc87-c2e33ca25f73
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 56010f212dff770de216c9632fdd302fa7de0910
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="state-element-assl"></a>State 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含描述父元素的目前處理狀態的唯讀值。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, MiningModel, MiningStructure, Partition -->  
      ...  
   <State>...</State>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)，[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)， [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)，[磁碟分割](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*處理*|已經完全處理此元素。|  
|*PartiallyProcessed*|已經部分處理此元素  ([Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)和[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)只。)|  
|*未處理*|尚未處理此元素。|  
  
 列舉型別對應至允許的值**狀態**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.AnalysisState>。  
  
 對應至父系的項目**狀態**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.MeasureGroup>， <xref:Microsoft.AnalysisServices.MiningModel>， <xref:Microsoft.AnalysisServices.MiningStructure>，和<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
