---
title: RoleID 元素 (ASSL) |Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 710306c1a31a188bea19b7bf53e7ac2c7324c00d
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38007220"
---
# <a name="roleid-element-assl"></a>RoleID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  識別要定義權限的角色。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Permission> <!-- or one of the listed below in the Element Relationships table -->  
   ...  
   <RoleID>...</RoleID>  
   ...  
</Permission>  
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
|父元素|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)， [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)， [DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)， [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)， [MiningStructurePermission](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)，[權限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素**RoleID**在 「 分析管理物件 (AMO) 物件模型會<xref:Microsoft.AnalysisServices.CubePermission>， <xref:Microsoft.AnalysisServices.DatabasePermission>， <xref:Microsoft.AnalysisServices.DimensionPermission>， <xref:Microsoft.AnalysisServices.MiningModelPermission>， <xref:Microsoft.AnalysisServices.MiningStructurePermission>，以及<xref:Microsoft.AnalysisServices.Permission>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
