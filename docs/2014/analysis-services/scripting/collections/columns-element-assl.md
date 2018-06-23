---
title: Columns 元素 (ASSL) |Microsoft 文件
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
- Columns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- COLUMNS
helpviewer_keywords:
- Columns element
ms.assetid: 14011eed-6f10-4120-b256-d599d59bde80
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e635738dddc7eabda62f0c35df860db3d9a10b60
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035078"
---
# <a name="columns-element-assl"></a>Columns 元素 (ASSL)
  包含與父元素相關聯之資料行的集合。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action xsi:type="DrillThroughAction"> <!-- or one of the elements listed below in the Element Relationships table -->  
   <Columns>  
      <Column xsi:type="MeasureBinding">...</Column> <!-- parent: DrillThroughAction -->  
      <!-- or -->  
      <Column xsi:type="CubeAttributeBinding">...</Column> <!-- parent: DrillThroughAction -->  
      <!-- or -->  
      <Column xsi:type="EventColumn">...</Column> <!-- parent: Event -->  
      <!-- or -->  
      <Column xsi:type="MiningModelColumn">...</Column> <!-- parent: MiningModel or MiningModelColumn -->  
      <!-- or -->  
      <Column xsi:type="MiningStructureColumn">...</Column> <!-- parent: MiningStructure or TableMiningStructureColumn -->  
   </Columns>  
</DrillThroughAction>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
  
|上階或父系|基數|  
|------------------------|-----------------|  
|[事件](../objects/event-element-assl.md)|1-1：只出現一次的必要元素。|  
|All others|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../objects/action-element-assl.md)型別的[DrillThroughAction](../data-type/action-data-type-assl.md)，[事件](../objects/event-element-assl.md)， [MiningModel](../objects/miningmodel-element-assl.md)， [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)， [TableMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
  
|上階或父系|子元素|  
|------------------------|--------------------|  
|[DrillThroughAction](../data-type/binding-data-type-assl.md)或[MeasureBinding](../data-type/measurebinding-data-type-assl.md)|  
|[事件](../data-type/eventcolumn-data-type-assl.md)|  
|[MiningModel](../objects/miningmodel-element-assl.md)， [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|[MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md)， [TableMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 如`DrillThroughAction`項目，`Columns`集合會識別包含資料時執行這個動作時要傳回的資料行。  
  
 如`TableMiningStructureColumn`項目，`Columns`集合允許單一遞迴層級。 換句話說，任何`TableMiningStructureColumn`此集合中包含的項目不能包含任何`TableMiningStructureColumn`中的項目及其`Columns`集合。  
  
 在「分析管理物件」(AMO) 物件模型中的某些對應元素是 <xref:Microsoft.AnalysisServices.TraceColumnCollection>、<xref:Microsoft.AnalysisServices.MiningModelColumnCollection> 和 <xref:Microsoft.AnalysisServices.MiningStructureColumnCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  