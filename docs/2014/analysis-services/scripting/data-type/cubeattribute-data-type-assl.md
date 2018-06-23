---
title: CubeAttribute 資料類型 (ASSL) |Microsoft 文件
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
- CubeAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeAttribute
helpviewer_keywords:
- CubeAttribute data type
ms.assetid: 114ffb44-460b-4971-b31b-dd844e960b81
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dce594145db99d7edfa991c2e975f62e55d3ef34
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034459"
---
# <a name="cubeattribute-data-type-assl"></a>CubeAttribute 資料類型 (ASSL)
  定義代表屬性相關聯的基本資料類型[Cube](../objects/cube-element-assl.md)項目。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[AggregationUsage](../properties/aggregationusage-element-assl.md)，[註解](../collections/annotations-element-assl.md)， [AttributeHierarchyEnabled](../properties/enabled-element-assl.md)， [AttributeHierarchyOptimizedState](../properties/state-element-assl.md)， [AttributeHierarchyVisible](../properties/visible-element-assl.md)， [AttributeID](../properties/id-element-assl.md)|  
|衍生的元素|[屬性](../objects/attribute-element-assl.md)([屬性](../collections/attributes-element-assl.md)集合[CubeDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>備註  
 *AttributeHierarchyOptimizedState*在 DeploymentMode 組態屬性值 1 或 2 （SharePoint 或表格式模式，用來執行 PowerPivot 和表格式模型資料庫） 執行服務時，不支援項目。  
  
 無法加入屬性當做階層層級時的屬性， *AtttributeHierarchyEnabled*，設為 FALSE 而且執行個體是在 DeploymentMode 1 或 2 （SharePoint 或表格式伺服器模式） 下。  
  
 中的屬性[CubeDimension](dimension-data-type-assl.md)中未明確包含的項目[屬性](../collections/attributes-element-assl.md)會成為具有預設值指派給他們的集合。 屬性會加入至集合之後，可以由傳回屬性[探索](../../xmla/xml-elements-methods-discover.md)方法。  
  
 [AggregationUsage](../properties/aggregationusage-element-assl.md)元素會控制如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]自動設計屬性的彙總。 `AggregationUsage` 元素不會限制手動針對 Cube 建立的任何彙總。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.CubeAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  