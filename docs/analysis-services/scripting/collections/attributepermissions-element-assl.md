---
title: AttributePermissions 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 997b59c1c69327817ff22ad16ab1120041f5b5df
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="attributepermissions-element-assl"></a>AttributePermissions 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的個別屬性權限集合[角色](../../../analysis-services/scripting/objects/role-element-assl.md)之特定維度上的項目[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeDimensionPermission> <!-- or DimensionPermission -->  
   <AttributePermissions>  
      <AttributePermission>...</AttributePermission>  
      </AttributePermissions>  
</CubeDimensionPermission>  
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
|父元素|[CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)， [DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|  
|子元素|[AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 如**DimensionPermission**，這個集合只能包含一個**AttributePermission**每個屬性。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.AttributePermissionCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [Permission 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)   
 [集合 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
