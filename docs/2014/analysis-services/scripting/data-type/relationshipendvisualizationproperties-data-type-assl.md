---
title: RelationshipEndVisualizationProperties 資料類型 (ASSL) |Microsoft Docs
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
ms.assetid: 11f9a10f-d36c-4faf-b595-3fe969d1935e
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 58348251e9ea00c4f6eebc5fcec067683e49a3a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161269"
---
# <a name="relationshipendvisualizationproperties-data-type-assl"></a>RelationshipEndVisualizationProperties 資料類型 (ASSL)
  定義代表關聯性中之關聯性端的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<RelationshipEnd>  
   <FolderPosition>...</FolderPosition>  
   <ContextualNameRule>...</ContextualNameRule>  
   <DefaultDetailsPosition>...</DefaultDetailsPosition>  
   <DisplayKeyPosition>...</DisplayKeyPosition>  
   <CommonIdentifierPosition>...</CommonIdentifierPosition>  
   <IsDefaultMeasure>...</IsDefaultMeasure>  
   <IsDefaultImage>...</IsDefaultImage>  
   <SortPropertiesPosition>...</SortPropertiesPosition>  
</RelationshipEnd>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[RelationshipEnd](relationshipend-data-type-assl.md)|  
|子元素|[FolderPosition](../../xmla/xml-elements-properties/folderposition-element-xml.md)， [ContextualNameRule](../../xmla/xml-elements-properties/contextualnamerule-element-xml.md)， [DefaultDetailsPosition](../../xmla/xml-elements-properties/defaultdetailsposition-element-xml.md)， [DisplayKeyPosition](../../xmla/xml-elements-properties/displaykeyposition-element-xml.md)， [CommonIdentifierPosition](../../xmla/xml-elements-properties/commonidentifierposition-element-xml.md)， [IsDefaultMeasure](../../xmla/xml-elements-properties/isdefaultmeasure-element-xml.md)， [IsDefaultImage](../../xmla/xml-elements-properties/isdefaultimage-element-xml.md)， [SortPropertiesPosition](../../xmla/xml-elements-properties/sortpropertiesposition-element-xml.md)|  
|衍生的元素||  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.RelationshipEnd>。  
  
  
