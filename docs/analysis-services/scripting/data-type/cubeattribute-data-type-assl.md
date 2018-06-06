---
title: CubeAttribute 資料類型 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 11a45e49fa902554aaa2b7be1486fb976f03c580
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="cubeattribute-data-type-assl"></a>CubeAttribute 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
