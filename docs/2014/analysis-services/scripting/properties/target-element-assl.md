---
title: 目標元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Target Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Target
helpviewer_keywords:
- Target element
ms.assetid: 08ce0441-94b6-4f1d-acba-f31c8212cb79
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23d55d909179fd568075feba54199514a7396c6b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169058"
---
# <a name="target-element-assl"></a>Target 元素 (ASSL)
  識別的目標[動作](../objects/action-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action>  
   ...  
   <Target>...</Target>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../objects/action-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個項目的預期值而定的值[TargetType](targettype-element-assl.md)父元素`Action`。 下表將根據 `Target` 的值來描述 `TargetType` 的預期值。  
  
|TargetType 值|預期的值|  
|----------------------|--------------------|  
|*Cube*|Cube 的名稱。|  
|*資料格*|Subcube 運算式。|  
|*設定*|集合運算式或命名集的名稱。 **注意：** subselect 陳述式無法使用。|  
|*階層架構 HierarchyMembers*|階層的名稱。|  
|*維度 DimensionMembers*|維度的名稱。|  
|*層級 LevelMembers*|層級的名稱。|  
|*屬性 AttributeMembers*|屬性的名稱。|  
  
 對應至父系的元素`Target`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
