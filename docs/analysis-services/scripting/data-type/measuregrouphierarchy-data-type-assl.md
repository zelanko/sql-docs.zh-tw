---
title: "MeasureGroupHierarchy 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MeasureGroupHierarchy Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MeasureGroupHierarchy
helpviewer_keywords:
- MeasureGroupHierarchy data type
ms.assetid: 63c2fd97-d7ad-4715-8c49-24d684bc92d7
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a79e5ad24234b574933950ecf46912c6d6cabb99
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="measuregrouphierarchy-data-type-assl"></a>MeasureGroupHierarchy 資料類型 (ASSL)
  定義代表量值群組中某個階層之相關資訊的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MeasureGroupHierarchy>  
   <HierarchyID>...</HierarchyID>  
      <Annotations>...</Annotations>  
</MeasureGroupHierarchy>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [HierarchyID](../../../analysis-services/scripting/properties/hierarchyid-element-assl.md)|  
|衍生的元素|[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)([階層](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)集合[RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md))|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

