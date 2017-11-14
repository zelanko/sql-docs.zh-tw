---
title: "MeasureGroup 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
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
apiname:
- MeasureGroup Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MeasureGroup
helpviewer_keywords:
- MeasureGroup element
ms.assetid: 7aa099db-5dc7-4cac-b437-f73fc0921b24
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5232a3299f269d6f798523d934ca80cff21097df
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="measuregroup-element-assl"></a>MeasureGroup 元素 (ASSL)
  定義位於相同資料粒度層級的一組量值。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MeasureGroups>  
   <MeasureGroup> <!-- ancestor: Cube -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</<Create  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <LastProcessed>...</LastProcessed>  
      <Translations>...</Translations>  
      <Type>...</Type>  
      <State>...</State>  
      <MeasureQualification>...</MeasureQualification>  
      <Measures>...</Measures>  
      <DataAggregation>...</DataAggregation>  
      <Source>...</Source>  
            <StorageMode>...</StorageMode>  
      <StorageLocation>...</StorageLocation>  
      <IgnoreUnrelatedDimensions>...</IgnoreUnrelatedDimensions>  
            <ProactiveCaching>...</ProactiveCaching>  
      <EstimatedRows>...</EstimatedRows>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <EstimatedSize>...</EstimatedSize>  
      <ProcessingMode>...</ProcessingMode>  
      <Dimensions>...</Dimensions>  
      <Partitions>...</Partitions>  
      <AggregationPrefix>...</AggregationPrefix>  
      <ProcessingPriority>...</ProcessingPriority>  
            <AggregationDesigns>...</AggregationDesigns>  
      <Annotations>...</Annotations>  
   </MeasureGroup>  
   <!-- or  -->  
   <MeasureGroup xsi:type="MeasureGroupBinding">...</MeasureGroup> <!-- ancestor: CubeBinding -->  
   <!-- or  -->  
   <MeasureGroup xsi:type="PerspectiveMeasureGroup">...</MeasureGroup> <!-- ancestor: Perspective -->  
</MeasureGroups>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|請參閱下表。|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
|上階或父系|資料類型|  
|------------------------|---------------|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|無|  
|[CubeBinding](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[檢視方塊](../../../analysis-services/scripting/objects/perspective-element-assl.md)|[PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[量值群組](../../../analysis-services/scripting/collections/measuregroups-element-assl.md)|  
|子元素|請參閱下表。|  
  
|上階或父系|子元素|  
|------------------------|--------------------|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[AggregationDesigns](../../../analysis-services/scripting/collections/aggregationdesigns-element-assl.md)， [AggregationPrefix](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md)，[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)， [DataAggregation](../../../analysis-services/scripting/properties/dataaggregation-element-assl.md)，[描述](../../../analysis-services/scripting/properties/description-element-assl.md)，[維度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)， [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)， [EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md)， [EstimatedSize](../../../analysis-services/scripting/properties/estimatedsize-element-assl.md)，[識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)， [IgnoreUnrelatedDimensions](../../../analysis-services/scripting/properties/ignoreunrelateddimensions-element-assl.md)， [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)， [MeasureQualification](../../../analysis-services/scripting/properties/measurequalificaton-element-assl.md)，[量值](../../../analysis-services/scripting/collections/measures-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)，[分割](../../../analysis-services/scripting/collections/partitions-element-assl.md)， [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)， [ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md)， [ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md)，[來源](../../../analysis-services/scripting/properties/source-element-measure-assl.md)，[狀態](../../../analysis-services/scripting/properties/state-element-assl.md)， [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)， [StorageMode](../../../analysis-services/scripting/properties/storagemode-element-assl.md)，[翻譯](../../../analysis-services/scripting/collections/translations-element-assl.md)，[類型](../../../analysis-services/scripting/properties/type-element-measuregroup-assl.md)|  
|[CubeBinding](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)|無|  
|[檢視方塊](../../../analysis-services/scripting/objects/perspective-element-assl.md)|無|  
  
## <a name="remarks"></a>備註  
 量值群組的所有量值都必須來自單一資料表。 量值群組可以定義可針對每個資料分割覆寫的預設繫結。  
  
 **MeasureGroup** 元素會定義一般 Cube 和虛擬 Cube 之量值群組通用的詳細資料。 個別的子類型會定義每個類型專用的詳細資料。  
  
 **State** 的 **MeasureGroup** 屬性具有下列值：  
  
-   *FullyProcessed* (如果所有資料分割都已經過處理的話)。  
  
-   *PartiallyProcessed* (如果至少一個資料分割已經過處理的話)。  
  
-   *Unprocessed* (如果沒有任何資料分割經過處理的話)。  
  
 在「分析管理物件」(AMO) 物件模型中對應的元素是 <xref:Microsoft.AnalysisServices.MeasureGroup> 和 <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>。  
  
## <a name="see-also"></a>另請參閱  
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

