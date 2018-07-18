---
title: CubeDimension 資料類型 (ASSL) |Microsoft Docs
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
- CubeDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeDimension
helpviewer_keywords:
- CubeDimension data type
ms.assetid: 128ac790-65a1-4e35-b909-8dba2a61b24c
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a02ef89f5dac200450faf8151a71aeae703e8b35
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220318"
---
# <a name="cubedimension-data-type-assl"></a>CubeDimension 資料類型 (ASSL)
  定義代表維度與 Cube 之間關聯性的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeDimension>  
      <ID>...</ID>  
   <Name>...</Name>  
   <Translations>...</Translations>  
   <DimensionID>...</DimensionID>  
   <Visible>...</Visible>  
   <AllMemberAggregationUsage>...</AllMemberAggregationUsage>  
   <HierarchyUniqueNameStyle>...</HierarchyUniqueNameStyle>  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
      <Attributes>...</Attributes>  
   <Hierarchies>...</Hierarchies>  
      <Annotations>...</Annotation>  
</CubeDimension>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[AllMemberAggregationUsage](../properties/aggregationusage-element-assl.md)，[註解](../collections/annotations-element-assl.md)，[屬性](../collections/attributes-element-assl.md)， [DimensionID](../properties/id-element-assl.md)，[階層](../collections/hierarchies-element-assl.md)， [HierarchyUniqueNameStyle](../properties/hierarchyuniquenamestyle-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [MemberUniqueNameStyle](../properties/memberuniquenamestyle-element-assl.md)，[名稱](../properties/name-element-assl.md)，[可見](../properties/visible-element-assl.md)，[翻譯](../collections/translations-element-assl.md)|  
|衍生的元素|[維度](../objects/dimension-element-assl.md)([維度](../collections/dimensions-element-assl.md)的集合[Cube](../objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 `CubeDimension` 上的每個維度關聯性都有一個 `Cube`。 `CubeDimension` 涵蓋 Cube 的所有 `MeasureGroups`。  
  
 A`CubeDimension`必須包含[CubeHierarchy](hierarchy-data-type-assl.md)如果維度與階層的特定項目，包括停用階層 （因而，允許選取的階層要套用至特定的項目維度使用方式），或變成不可見的階層。  
  
 同樣地，`CubeDimension`必須包含[CubeAttribute](cubeattribute-data-type-assl.md)只有維度具有特定屬性。 (沒有任何方法可選取要套用至特定維度使用方式的屬性，不過您可以讓屬性隱藏)。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.CubeDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
