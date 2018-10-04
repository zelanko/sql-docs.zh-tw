---
title: 狀態元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- State Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- State
helpviewer_keywords:
- State element
ms.assetid: b6ee1144-89f7-4ced-bc87-c2e33ca25f73
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1aaf3af4f5a98c8601f9738765a248fe597ccb31
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072088"
---
# <a name="state-element-assl"></a>State 元素 (ASSL)
  包含描述父元素之目前處理狀態的唯讀值。  
  
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
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Cube](../objects/cube-element-assl.md)，[維度](../objects/dimension-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)， [MiningModel](../objects/miningmodel-element-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)，[資料分割](../objects/partition-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*處理*|已經完全處理此元素。|  
|*PartiallyProcessed*|已經部分處理此元素  ([Cube](../objects/cube-element-assl.md)並[MeasureGroup](../objects/group-element-assl.md)只。)|  
|*尚未處理*|尚未處理此元素。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `State` 允許值的列舉是 <xref:Microsoft.AnalysisServices.AnalysisState>。  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `State` 父系的元素是 <xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.MeasureGroup>、<xref:Microsoft.AnalysisServices.MiningModel>、<xref:Microsoft.AnalysisServices.MiningStructure> 和 <xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
