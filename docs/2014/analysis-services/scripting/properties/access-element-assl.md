---
title: 存取元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Access Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Access
helpviewer_keywords:
- Access element
ms.assetid: 6ad99010-fac5-48e9-a099-ecbca380e127
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 60fbf476e1d884cce28dd674ab16d3bda001a3a0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051838"
---
# <a name="access-element-assl"></a>Access 元素 (ASSL)
  表示層級的存取權提供給[CellPermission](../objects/cellpermission-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CellPermission>  
   ...  
   <Access>...</Access>  
   ...  
</CellPermission>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CellPermission](../objects/cellpermission-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*讀取*|允許唯讀存取。|  
|*意外讀取*|允許意外讀取存取。|  
|*讀寫*|允許讀寫存取。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Access` 允許值的列舉是 <xref:Microsoft.AnalysisServices.CellPermissionAccess>。  
  
## <a name="see-also"></a>另請參閱  
 [Role 元素&#40;ASSL&#41;](../objects/role-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
