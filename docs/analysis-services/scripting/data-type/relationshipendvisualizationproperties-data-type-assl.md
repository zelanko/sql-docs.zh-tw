---
title: "RelationshipEndVisualizationProperties 資料類型 (ASSL) |Microsoft 文件"
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
applies_to:
- SQL Server 2016 Preview
ms.assetid: 11f9a10f-d36c-4faf-b595-3fe969d1935e
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9627f9a245230f13030b87ae63df47ec920c271a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

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
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)|  
|子元素|[FolderPosition](../../../analysis-services/xmla/xml-elements-properties/folderposition-element-xml.md)， [ContextualNameRule](../../../analysis-services/xmla/xml-elements-properties/contextualnamerule-element-xml.md)， [DefaultDetailsPosition](../../../analysis-services/xmla/xml-elements-properties/defaultdetailsposition-element-xml.md)， [DisplayKeyPosition](../../../analysis-services/xmla/xml-elements-properties/displaykeyposition-element-xml.md)， [CommonIdentifierPosition](../../../analysis-services/xmla/xml-elements-properties/commonidentifierposition-element-xml.md)， [IsDefaultMeasure](../../../analysis-services/xmla/xml-elements-properties/isdefaultmeasure-element-xml.md)， [IsDefaultImage](../../../analysis-services/xmla/xml-elements-properties/isdefaultimage-element-xml.md)， [SortPropertiesPosition](../../../analysis-services/xmla/xml-elements-properties/sortpropertiesposition-element-xml.md)|  
|衍生的元素||  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.RelationshipEnd>。  
  
  

