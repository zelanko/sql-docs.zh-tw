---
title: "DataAggregation 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
- DataAggregation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DataAggregation element
ms.assetid: baf6d2c9-54f6-4a6d-95f7-e1e758be458d
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 92556b6af8a3d56f647fcbea8b34e197fb8ce663
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dataaggregation-element-assl"></a>DataAggregation 元素 (ASSL)
  決定執行個體是否可彙總保存的資料或快取的資料[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MeasureGroup>  
   ...  
   <DataAggregation>...</DataAggregation>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*DataAndCacheAggregatable*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[量值群組](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|說明|  
|-----------|-----------------|  
|*無*|不會針對這個量值群組執行彙總。|  
|*DataAggregatable*|可針對這個量值群組的保存資料進行彙總。|  
|*CacheAggregatable*|可針對這個量值群組的快取資料進行彙總。|  
|*DataAndCacheAggregatable*|可同時針對這個量值群組的保存資料和快取資料進行彙總。|  
  
 對應目的父代的項目**DataAggregation**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.MeasureGroup>。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Dimension 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

