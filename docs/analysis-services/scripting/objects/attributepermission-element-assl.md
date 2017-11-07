---
title: "AttributePermission 元素 (ASSL) |Microsoft 文件"
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
- AttributePermission Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AttributePermission
helpviewer_keywords:
- AttributePermission element
ms.assetid: efc8aa63-3959-4b2e-98f8-2a9c424298c2
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a780b5f3f29edf8ff320763740ca505826f2c80d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="attributepermission-element-assl"></a>AttributePermission 元素 (ASSL)
  定義的權限的成員[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素中個別維度屬性上有[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AttributePermissions>  
   <AttributePermission>  
      <AttributeID>...</AttributeID>  
      <Description>...</Description>  
      <DefaultMember>...</DefaultMember>  
            <VisualTotals>...</VisualTotals>  
      <AllowedSet>...</AllowedSet>  
            <DeniedSet>...</DeniedSet>  
      <Annotations>...</Annotations>  
   </AttributePermission>  
</AttributePermissions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributePermissions](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)|  
|子元素|[AllowedSet](../../../analysis-services/scripting/properties/allowedset-element-assl.md)，[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md)， [DefaultMember](../../../analysis-services/scripting/properties/defaultmember-element-assl.md)， [DeniedSet](../../../analysis-services/scripting/properties/deniedset-element-assl.md)， [描述](../../../analysis-services/scripting/properties/description-element-assl.md)， [VisualTotals](../../../analysis-services/scripting/properties/visualtotals-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.AttributePermission>。  
  
## <a name="see-also"></a>另請參閱  
 [CubeDimensionPermission 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)   
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

