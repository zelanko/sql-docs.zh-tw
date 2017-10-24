---
title: "CubeAttribute 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CubeAttribute Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CubeAttribute
helpviewer_keywords:
- CubeAttribute data type
ms.assetid: 114ffb44-460b-4971-b31b-dd844e960b81
caps.latest.revision: 45
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c04b5602de94ac46b736ebfc878760174ced5a8d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="cubeattribute-data-type-assl"></a>CubeAttribute 資料類型 (ASSL)
  定義代表屬性相關聯的基本資料類型[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeAttribute>  
   <AttributeID>...</AttributeID>  
   <AggregationUsage>...</AggregationUsage>  
   <AttributeHierarchyOptimizedState>...</AttributeHierarchyOptimizedState>  
   <AttributeHierarchyEnabled>...</AttributeHierarchyEnabled>  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   <Annotations>...</Annotations>  
</CubeAttribute>  
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
|子元素|[AggregationUsage](../../../analysis-services/scripting/properties/aggregationusage-element-assl.md)，[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [AttributeHierarchyEnabled](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md)， [AttributeHierarchyOptimizedState](../../../analysis-services/scripting/properties/attributehierarchyoptimizedstate-element-assl.md)， [AttributeHierarchyVisible](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md)， [AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md)|  
|衍生的元素|[屬性](../../../analysis-services/scripting/objects/attribute-element-assl.md)([屬性](../../../analysis-services/scripting/collections/attributes-element-assl.md)集合[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md))|  
  
## <a name="remarks"></a>備註  
 *AttributeHierarchyOptimizedState*在 DeploymentMode 組態屬性值 1 或 2 中執行服務時，不支援項目 (SharePoint 或表格式模式，用來執行[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]和表格式模型資料庫）。  
  
 無法加入屬性當做階層層級時的屬性， *AtttributeHierarchyEnabled*，設為 FALSE 而且執行個體是在 DeploymentMode 1 或 2 （SharePoint 或表格式伺服器模式） 下。  
  
 中的屬性[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)中未明確包含的項目[屬性](../../../analysis-services/scripting/collections/attributes-element-assl.md)會成為具有預設值指派給他們的集合。 屬性會加入至集合之後，可以由傳回屬性[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法。  
  
 [AggregationUsage](../../../analysis-services/scripting/properties/aggregationusage-element-assl.md)元素會控制如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]自動設計屬性的彙總。 **AggregationUsage**項目不會限制任何未手動建立 cube 的彙總。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.CubeAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

