---
title: "MeasureGroupDimension 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MeasureGroupDimension Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MeasureGroupDimension
helpviewer_keywords: MeasureGroupDimension data type
ms.assetid: 9d1c1c19-31ce-4c42-b2e6-4c1b08875a83
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0a7c98b6be117dbb61579ce6c95c474cb1457cfc
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="measuregroupdimension-data-type-assl"></a>MeasureGroupDimension 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義代表維度與量值群組之間的關聯性的抽象基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MeasureGroupDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
      <Annotations>...</Annotations>  
   <Source>...</Source>  
</MeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|[DataMiningMeasureGroupDimension](../../../analysis-services/scripting/data-type/dataminingmeasuregroupdimension-data-type-assl.md)， [DegenerateMeasureGroupDimension](../../../analysis-services/scripting/data-type/degeneratemeasuregroupdimension-data-type-assl.md)， [ManyToManyMeasureGroupDimension](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md)， [ReferenceMeasureGroupDimension](../../../analysis-services/scripting/data-type/referencemeasuregroupdimension-data-type-assl.md)， [RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [CubeDimensionID](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md)，[來源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
|衍生的元素|[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)([維度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)集合[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 每個**MeasureGroupDimension**是其中一個 cube 維度的參考。 這些元素會定義哪些 Cube 維度會套用至量值群組。  
  
 提供的屬性集合會決定量值群組上量值具有的資料粒度 (範圍)。 例如，代表產品銷售量的量值會包含在 Sales 量值群組中。 這些量值的資訊會以每月 (而非每週或每日) 資料粒度儲存在基礎資料來源中。 在此情況下，會列出 Month 屬性供**MeasureGroupDimension**描述時間維度與 Sales 量值群組之間的關聯性。 在少數情況中，資料粒度可能會以屬性集合的方式定義。 例如，假設指定了屬性集合 {Day, Week, Month, Year}，其中 Day 隱含 Week 和 Month，但是 Week 並未隱含 Month，則 Forecasts 量值群組中包含的量值可能會具有 Month 和 Week，但不具有 Day。  
  
 如果沒有提供任何屬性，系統就只會列出維度的索引鍵屬性 (定義資料粒度的最低層級)。 量值群組的每個資料分割都必須具有相同的資料粒度。 列出的屬性集合在屬性之間的關聯性方面不應該重複。 例如，如果 Month 隱含 Year，此資料粒度就會定義為 Month，而非 Month 和 Year。  
  
 A **MeasureGroupDimension**必須包含階層，則必須要指出特定項目。 (沒有任何方法可選取哪些階層要套用至特定量值群組)。 同樣地，它必須包含[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)只有當要指出特定項目。  
  
 每個階層都必須是包含之階層的子集[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)。 您無法選取這些層級，不過某些層級可能會自動停用，端視量值群組的資料粒度而定。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.MeasureGroupDimension>。  
  
## <a name="see-also"></a>請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
