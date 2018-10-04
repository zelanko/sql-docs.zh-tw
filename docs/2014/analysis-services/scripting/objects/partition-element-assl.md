---
title: 資料分割元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Partition Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PARTITION
helpviewer_keywords:
- Partition element
ms.assetid: 40020840-1bb7-478f-9017-1a30342ac4c6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4ad06de27b07ab58df2d5357b960906093daa5f5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198798"
---
# <a name="partition-element-assl"></a>Partition 元素 (ASSL)
  定義的資料分割[MeasureGroup](group-element-assl.md)項目或資料分割中的繫結的行外[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Partitions>  
      <Partition> <!-- ancestor: MeasureGroup -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Source>...</Source>  
      <ProcessingPriority>...</ProcessingPriority>  
      <AggregationPrefix>...</AggregationPrefix>  
      <StorageMode>...</StorageMode>  
      <ProcessingMode>...</ProcessingMode>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <StorageLocation>...</StorageLocation>  
      <RemoteDatasourceID>...</RemoteDatasourceID>  
      <Slice>...</Slice>  
      <ProactiveCaching>...</ProactiveCaching>  
      <Type>...</Type>  
      <EstimatedSize>...</EstimatedSize>  
      <EstimatedRows>...</EstimatedRows>  
      <CurrentStorageMode>...</CurrentStorageMode>  
      <AggregationDesignID>...</AggregationDesignID>  
      <AggregationInstances>...</AggregationInstances>  
      <AggregationInstanceSource>...</AggregationInstanceSource>  
      <LastProcessed>...</LastProcessed>  
      <State>...</State>  
      <Annotations>.../Annotations>  
   </Partition>  
   <!-- or -->  
   <Partition xsi:type="PartitionBinding"> <!-- ancestor: MeasureGroupBinding -->  
   </Partition>  
</Partitions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
|上階或父系|資料類型|  
|------------------------|---------------|  
|[MeasureGroup](group-element-assl.md)|None|  
|[MeasureGroupBinding](../data-type/binding-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料分割](../collections/partitions-element-assl.md)|  
  
|上階或父系|子元素|  
|------------------------|--------------------|  
|[MeasureGroup](../properties/id-element-assl.md)， [AggregationInstances](../collections/aggregationinstances-element-assl.md)， [AggregationInstanceSource](../properties/aggregationinstancesource-element-assl.md)， [AggregationPrefix](../properties/aggregationprefix-element-assl.md)，[註解](../collections/annotations-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [CurrentStorageMode](../properties/storagemode-element-assl.md)，[描述](../properties/description-element-assl.md)， [ErrorConfiguration](errorconfiguration-element-assl.md)， [EstimatedRows](../properties/estimatedrows-element-assl.md)， [EstimatedSize](../properties/estimatedsize-element-assl.md)， [ID](../properties/id-element-assl.md)， [LastProcessed](../properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)，[名稱](../properties/name-element-assl.md)， [ProactiveCaching](proactivecaching-element-assl.md)， [ProcessingMode](../properties/processingmode-element-assl.md)， [ProcessingPriority](../properties/processingpriority-element-assl.md)， [RemoteDatasourceID](../properties/datasourceid-element-assl.md)，[配量](../properties/slice-element-assl.md)，[來源](../properties/source-element-binding-assl.md)，[狀態](../properties/state-element-assl.md)， [StorageLocation](../properties/storagelocation-element-assl.md)， [StorageMode](../properties/storagemode-element-assl.md)，[類型](../properties/type-element-partition-assl.md)|  
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)|None|  
  
## <a name="remarks"></a>備註  
 此元素在 DeploymentMode 值 2 (表格式伺服器模式) 下，擁有下列驗證：  
  
-   下列子元素不受支援，因此不應該使用：  
  
    -   [ProcessingPriority](../properties/processingpriority-element-assl.md)  
  
    -   [AggregationPrefix](../properties/aggregationprefix-element-assl.md)  
  
    -   [StorageLocation](../properties/storagelocation-element-assl.md)  
  
    -   [ProcessingMode](../properties/processingmode-element-assl.md)  
  
    -   [ErrorConfiguration](errorconfiguration-element-assl.md)  
  
    -   [StorageLocation](../properties/storagelocation-element-assl.md)  
  
    -   [RemoteDatasourceID](../properties/datasourceid-element-assl.md)  
  
    -   [配量](../properties/slice-element-assl.md)  
  
    -   [ProactiveCaching](proactivecaching-element-assl.md)  
  
    -   [型別](../properties/type-element-partition-assl.md)  
  
    -   [CurrentStorageMode](../properties/storagemode-element-assl.md)  
  
    -   [AggregationDesignID](../properties/aggregationdesignid-element-assl.md)  
  
    -   [AggregationInstances](../collections/aggregationinstances-element-assl.md)  
  
    -   [AggregationInstanceSource](../properties/aggregationinstancesource-element-assl.md)  
  
     如果使用上述任何元素，可能會發生錯誤。  
  
-   [來源](../properties/source-element-binding-assl.md)元素只接受**查詢**繫結。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
