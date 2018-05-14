---
title: CubeHierarchy 資料類型 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 31f1aa1ece1b17da3f68804166c9b092fea18367
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="cubehierarchy-data-type-assl"></a>CubeHierarchy 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義代表的相關資訊的基本資料類型[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)中的項目[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```  
<CubeHierarchy>   <HierarchyID>...</HierarchyID>   <Name>...</Name>   <OptimizedState>...</OptimizedState>   <Visible>...</Visible>   <Enabled>...</Enabled>   <Annotations>...</Annotations></CubeHierarchy>  
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
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[啟用](../../../analysis-services/scripting/properties/enabled-element-assl.md)， [HierarchyID](../../../analysis-services/scripting/properties/hierarchyid-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)， [OptimizedState](../../../analysis-services/scripting/properties/optimizedstate-element-assl.md)，[可見](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
|衍生的元素|[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)([階層](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)集合[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md))|  
  
## <a name="remarks"></a>備註  
 此資料類型沒有任何限制，而且可在任何部署模式下使用：0-多維度和資料採礦、1-SharePoint 及 2-表格式。  
  
 在 SQL Server 2016 Analysis Services 和更新版本，*啟用*屬性不能設定為**False**如*CubeHierarchy*。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.CubeHierarchy>。  
  
## <a name="see-also"></a>另請參閱  
 [Discover 方法&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
