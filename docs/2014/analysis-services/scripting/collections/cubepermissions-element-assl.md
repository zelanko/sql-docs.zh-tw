---
title: CubePermissions 元素 (ASSL) |Microsoft 文件
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
- CubePermissions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubePermissions
helpviewer_keywords:
- CubePermissions element
ms.assetid: 75a3a0c2-e1d4-4896-b0f5-2ea9c769b927
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d55b74204090e14e48ad0cf9ab30aa6b03680416
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022003"
---
# <a name="cubepermissions-element-assl"></a>CubePermissions 元素 (ASSL)
  包含適用於權限集合[Cube](../objects/cube-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Cube>  
   ...  
   <CubePermissions>  
      <CubePermission>...</CubePermission>  
   </CubePermissions>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Cube](../objects/cube-element-assl.md)|  
|子元素|[CubePermission](../objects/cubepermission-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.CubePermissionCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [Permission 資料類型&#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  