---
title: HierarchyID 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- HierarchyID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- HierarchyID
helpviewer_keywords:
- HierarchyID element
ms.assetid: 6effe47d-e598-41f8-993a-b2bce49fd7dd
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 96fd95f6853f5edd7f7eaa5d6aa9627cc322a1bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033341"
---
# <a name="hierarchyid-element-assl"></a>HierarchyID 元素 (ASSL)
  包含識別碼 (ID) [CubeHierarchy](../data-type/hierarchy-data-type-assl.md)， [MeasureGroupHierarchy](../data-type/measuregrouphierarchy-data-type-assl.md)，或[PerspectiveHierarchy](../data-type/perspectivehierarchy-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeHierarchy> <!-- or MeasureGroupHierarchy, PerspectiveHierarchy -->  
      ...  
   <HierarchyID>...</HierarchyID>  
      ...  
</CubeHierarchy>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubeHierarchy](../data-type/hierarchy-data-type-assl.md)， [MeasureGroupHierarchy](../data-type/measuregrouphierarchy-data-type-assl.md)， [PerspectiveHierarchy](../data-type/perspectivehierarchy-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目`HierarchyID`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.CubeHierarchy>和<xref:Microsoft.AnalysisServices.PerspectiveHierarchy>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  