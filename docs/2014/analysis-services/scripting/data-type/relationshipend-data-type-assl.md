---
title: RelationshipEnd 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 3a974dd4-e1d6-45b2-b8c8-1a914bc13a02
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23d0fce8a0856c178ef6933093400ca67ea4f9d3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197540"
---
# <a name="relationshipend-data-type-assl"></a>RelationshipEnd 資料類型 (ASSL)
  定義代表關聯性中之關聯性端的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<RelationshipEnd>  
   <Role>...</Role>  
   <Multiplicity>...</Multiplicity>  
   <DimensionID>...</DimensionID>  
   <Attributes>...</Attributes>  
   <Translations>...</Translations>  
   <VisualizationProperties>...</VisualizationProperties>  
</Relationship>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|None|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[關聯性](relationship-data-type-assl.md)|  
|子元素|[角色](../../xmla/xml-elements-properties/role-element-xmla.md)，[多重性](../properties/multiplicity-element-assl.md)， [DimensionID](../properties/id-element-assl.md)，[屬性](../collections/attributes-element-assl.md)，[翻譯](../collections/translations-element-assl.md)， [VisualizationProperties](relationshipendvisualizationproperties-data-type-assl.md)|  
|衍生的元素||  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.RelationshipEnd>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
