---
title: 目標元素 (ASSL) |Microsoft 文件
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
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 65150d66769a2ebdb67609989efbc1a7f81e9f89
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024064"
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
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../objects/action-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個項目的預期值取決於值[TargetType](targettype-element-assl.md)父項目`Action`。 下表將根據 `Target` 的值來描述 `TargetType` 的預期值。  
  
|TargetType 值|預期的值|  
|----------------------|--------------------|  
|*Cube*|Cube 的名稱。|  
|*資料格*|Subcube 運算式。|  
|*設定*|集合運算式或命名集的名稱。 **注意：** 不能在 subselect 陳述式。|  
|*階層架構 HierarchyMembers*|階層的名稱。|  
|*維度 DimensionMembers*|維度的名稱。|  
|*層級 LevelMembers*|層級的名稱。|  
|*屬性 AttributeMembers*|屬性的名稱。|  
  
 對應目的父代的項目`Target`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  