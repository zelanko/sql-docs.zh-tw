---
title: AttributePermission 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 09002c565cb9c4d385a42fcc3969ac28f458ed6e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="attributepermission-element-assl"></a>AttributePermission 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|子元素|[AllowedSet](../../../analysis-services/scripting/properties/allowedset-element-assl.md)，[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md)， [DefaultMember](../../../analysis-services/scripting/properties/defaultmember-element-assl.md)， [DeniedSet](../../../analysis-services/scripting/properties/deniedset-element-assl.md)，[描述](../../../analysis-services/scripting/properties/description-element-assl.md)， [VisualTotals](../../../analysis-services/scripting/properties/visualtotals-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.AttributePermission>。  
  
## <a name="see-also"></a>另請參閱  
 [CubeDimensionPermission 資料類型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)   
 [物件 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
