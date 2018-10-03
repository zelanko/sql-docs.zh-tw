---
title: Members 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Members Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Members
helpviewer_keywords:
- Members element
ms.assetid: 4bf585a3-b681-486d-852b-1244c5658a04
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b7d2be7834c48c5a65877ae6fd480f2a7d6ea459
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191058"
---
# <a name="members-element-assl"></a>Members 元素 (ASSL)
  包含的集合[成員](../objects/member-element-assl.md)父項目的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Group> <!-- or Role --<  
   ...  
   <Members>  
      <Member>...</Member>  
   </Members>  
   ...  
</Group>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[群組](../objects/group-element-assl.md)，[角色](../objects/role-element-assl.md)|  
|子元素|[成員](../objects/member-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`Members`在 「 分析管理物件 (AMO) 物件模型所<xref:Microsoft.AnalysisServices.Group>和<xref:Microsoft.AnalysisServices.Role>。  
  
## <a name="see-also"></a>另請參閱  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
