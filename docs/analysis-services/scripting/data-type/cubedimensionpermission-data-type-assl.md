---
title: "CubeDimensionPermission 資料類型 (ASSL) |Microsoft 文件"
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
- CubeDimensionPermission Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CubeDimensionPermission
helpviewer_keywords:
- CubeDimensionPermission data type
ms.assetid: d9d39859-5f33-48bc-a402-0071755918de
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0058f41feb1bf215c6d479492c6303c613ef7b53
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="cubedimensionpermission-data-type-assl"></a>CubeDimensionPermission 資料類型 (ASSL)
  定義代表在 Cube 中特定維度上單一角色之權限的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeDimensionPermission>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Description>...</Description>  
   <Read>...</Read>  
   <Write>...</Write>  
   <AttributePermissions>...</AttributePermissions>  
   <Annotations>...</Annotations>  
</CubeDimensionPermission>  
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
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [AttributePermissions](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)， [CubeDimensionID](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md)，[描述](../../../analysis-services/scripting/properties/description-element-assl.md)，[讀取](../../../analysis-services/scripting/properties/read-element-assl.md)， [寫入](../../../analysis-services/scripting/properties/write-element-assl.md)|  
|衍生的元素|[DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md) ([DimensionPermissions](../../../analysis-services/scripting/collections/dimensionpermissions-element-assl.md)集合[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)或[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.CubeDimensionPermission>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

