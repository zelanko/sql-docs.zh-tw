---
title: MeasureGroup 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroup Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroup
helpviewer_keywords:
- MeasureGroup element
ms.assetid: 7aa099db-5dc7-4cac-b437-f73fc0921b24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84186a736f7d3e17587a3a5457b1c7850c02f12b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089708"
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
  
|特性|描述|  
|--------------------|-----------------|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
|上階或父系|資料類型|  
|------------------------|---------------|  
|[Cube](cube-element-assl.md)|None|  
|[CubeBinding](../data-type/binding-data-type-assl.md)|  
|[檢視方塊](../data-type/perspectivemeasuregroup-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MeasureGroups](../collections/groups-element-assl.md)|  
|子元素||  
  
|上階或父系|子元素|  
|------------------------|--------------------|  
|[Cube](../collections/aggregationdesigns-element-assl.md)， [AggregationPrefix](../properties/aggregationprefix-element-assl.md)，[註解](../collections/annotations-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [DataAggregation](aggregation-element-assl.md)， [描述](../properties/description-element-assl.md)，[維度](../collections/dimensions-element-assl.md)， [ErrorConfiguration](errorconfiguration-element-assl.md)， [EstimatedRows](../properties/estimatedrows-element-assl.md)， [EstimatedSize](../properties/estimatedsize-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [IgnoreUnrelatedDimensions](../properties/ignoreunrelateddimensions-element-assl.md)， [LastProcessed](../properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)， [MeasureQualification](../properties/measurequalificaton-element-assl.md)，[量值](../collections/measures-element-assl.md)，[名稱](../properties/name-element-assl.md)，[分割](../collections/partitions-element-assl.md)， [ProactiveCaching](proactivecaching-element-assl.md)， [ProcessingMode](../properties/processingmode-element-assl.md)， [ProcessingPriority](../properties/processingpriority-element-assl.md)，[來源](../properties/source-element-measure-assl.md)，[狀態](../properties/state-element-assl.md)， [StorageLocation](../properties/storagelocation-element-assl.md)， [StorageMode](../properties/storagemode-element-assl.md)，[翻譯](../collections/translations-element-assl.md)，[類型](../properties/type-element-measuregroup-assl.md)|  
|[CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md)|None|  
|[檢視方塊](perspective-element-assl.md)|None|  
  
## <a name="remarks"></a>備註  
 量值群組的所有量值都必須來自單一資料表。 量值群組可以定義可針對每個資料分割覆寫的預設繫結。  
  
 `MeasureGroup` 元素會定義一般 Cube 和虛擬 Cube 之量值群組通用的詳細資料。 個別的子類型會定義每個類型專用的詳細資料。  
  
 `State` 的 `MeasureGroup` 屬性具有下列值：  
  
-   *FullyProcessed* (如果所有資料分割都已經過處理的話)。  
  
-   *PartiallyProcessed* (如果至少一個資料分割已經過處理的話)。  
  
-   *Unprocessed* (如果沒有任何資料分割經過處理的話)。  
  
 在「分析管理物件」(AMO) 物件模型中對應的元素是 <xref:Microsoft.AnalysisServices.MeasureGroup> 和 <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
