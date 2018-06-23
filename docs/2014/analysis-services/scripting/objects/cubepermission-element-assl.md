---
title: CubePermission 元素 (ASSL) |Microsoft 文件
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
- CubePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubePermission
helpviewer_keywords:
- CubePermission element
ms.assetid: b144b623-ff20-4ead-91ad-4c718f3b140b
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 557fd858a02ed3e0d05679dca56740d2d8eb2128
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030373"
---
# <a name="cubepermission-element-assl"></a>CubePermission 元素 (ASSL)
  定義特定成員的權限[角色](role-element-assl.md)元素中特殊[Cube](cube-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubePermissions>  
   <CubePermission>  
      <!-- The following elements extend Permission -->  
      <ReadSourceData>...</ReadSourceData>  
            <DimensionPermissions>...</DimensionPermissions>  
            <CellPermissions>...</CellPermissions>  
   </CubePermission>  
</CubePermissions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[權限](../data-type/permission-data-type-assl.md)|  
|預設值|無|  
|基數|0-n：只能出現一次或出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubePermissions](../collections/cubepermissions-element-assl.md)|  
|子元素|[CellPermissions](../collections/cellpermissions-element-assl.md)， [DimensionPermissions](../collections/dimensionpermissions-element-assl.md)， [ReadSourceData](data-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.CubePermission>。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 元素&#40;ASSL&#41;](cube-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  