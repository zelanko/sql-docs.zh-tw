---
title: "Hierarchies 元素 (ASSL) |Microsoft 文件"
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
apiname: Hierarchies Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Hierarchies
helpviewer_keywords: Hierarchies element
ms.assetid: dc844eea-869c-4217-b9be-e543a76f5e92
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1faf121482f52e31a19c6fadcb82ec76c66366ee
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="hierarchies-element-assl"></a>Hierarchies 元素 (ASSL)
  包含集合[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)元素與父元素相關聯。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Dimension> <!-- or CubeDimension, PerspectiveDimension -->  
   ...  
   <Hierarchies>  
            <Hierarchy>...</Hierarchy> <!-- parent: Dimension -->  
      <!-- or -->  
      <Hierarchy xsi:type="CubeHierarchy">...</Hierarchy> <!-- parent: CubeDimension -->  
     <!-- or -->  
      <Hierarchy xsi:type="PerspectiveHierarchy">...</Hierarchy> <!-- parent: PerspectiveDimension -->  
   <Hierarchies>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)，[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|  
|子元素|請參閱下表。|  
  
|上階或父系|子元素|  
|------------------------|-------------------|  
|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)型別的[CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)|  
|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|[Hierarchy](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|  
|[PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)型別的[PerspectiveHierarchy](../../../analysis-services/scripting/data-type/perspectivehierarchy-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應的元素是 <xref:Microsoft.AnalysisServices.HierarchyCollection>、<xref:Microsoft.AnalysisServices.CubeHierarchyCollection> 和 <xref:Microsoft.AnalysisServices.PerspectiveHierarchyCollection>。  
  
## <a name="see-also"></a>請參閱＜  
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
