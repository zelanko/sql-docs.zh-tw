---
title: MeasureGroupDimension 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroupDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroupDimension
helpviewer_keywords:
- MeasureGroupDimension data type
ms.assetid: 9d1c1c19-31ce-4c42-b2e6-4c1b08875a83
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c2c30eed2884aa84d7292668d9464a751467b391
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173698"
---
# <a name="measuregroupdimension-data-type-assl"></a>MeasureGroupDimension 資料類型 (ASSL)
  定義代表某個維度與量值群組之間關聯性的抽象基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MeasureGroupDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
      <Annotations>...</Annotations>  
   <Source>...</Source>  
</MeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|None|  
|衍生資料類型|[DataMiningMeasureGroupDimension](dimension-data-type-assl.md)， [DegenerateMeasureGroupDimension](measuregroupdimension-data-type-assl.md)， [ManyToManyMeasureGroupDimension](manytomanymeasuregroupdimension-data-type-assl.md)， [ReferenceMeasureGroupDimension](referencemeasuregroupdimension-data-type-assl.md)， [RegularMeasureGroupDimension](regularmeasuregroupdimension-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[註釋](../collections/annotations-element-assl.md)， [CubeDimensionID](../properties/id-element-assl.md)，[來源](../properties/source-element-binding-assl.md)|  
|衍生的元素|[維度](../objects/dimension-element-assl.md)([維度](../collections/dimensions-element-assl.md)的集合[MeasureGroup](../objects/group-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 每個 `MeasureGroupDimension` 都是 Cube 上其中一個維度的參考。 這些元素會定義哪些 Cube 維度會套用至量值群組。  
  
 提供的屬性集合會決定量值群組上量值具有的資料粒度 (範圍)。 例如，代表產品銷售量的量值會包含在 Sales 量值群組中。 這些量值的資訊會以每月 (而非每週或每日) 資料粒度儲存在基礎資料來源中。 在這個情況中，系統只會針對描述時間維度與 Sales 量值群組之間關聯性的 `MeasureGroupDimension` 列出 Month 屬性。 在少數情況中，資料粒度可能會以屬性集合的方式定義。 例如，假設指定了屬性集合 {Day, Week, Month, Year}，其中 Day 隱含 Week 和 Month，但是 Week 並未隱含 Month，則 Forecasts 量值群組中包含的量值可能會具有 Month 和 Week，但不具有 Day。  
  
 如果沒有提供任何屬性，系統就只會列出維度的索引鍵屬性 (定義資料粒度的最低層級)。 量值群組的每個資料分割都必須具有相同的資料粒度。 列出的屬性集合在屬性之間的關聯性方面不應該重複。 例如，如果 Month 隱含 Year，此資料粒度就會定義為 Month，而非 Month 和 Year。  
  
 只有當 `MeasureGroupDimension` 具有特別要指出的內容時，它才必須包含階層  (沒有任何方法可選取哪些階層要套用至特定量值群組)。 同樣地，它必須包含[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)才具有特別要指出。  
  
 每個階層都必須包含之階層的子集[CubeDimension](cubedimension-data-type-assl.md)。 您無法選取這些層級，不過某些層級可能會自動停用，端視量值群組的資料粒度而定。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.MeasureGroupDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
