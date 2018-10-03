---
title: TargetType 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- TargetType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TargetType
helpviewer_keywords:
- TargetType element
ms.assetid: 2c69ea6e-2af7-435b-9841-86117d5554a7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ed0ca768f075b7cd4249c9d8b021e2ec10d54c46
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099558"
---
# <a name="targettype-element-assl"></a>TargetType 元素 (ASSL)
  識別項目類型中所識別之項目的[目標](target-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action>  
   ...  
   <TargetType>...</TargetType>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../objects/action-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*Cube*|此動作的目標是 Cube。|  
|*資料格*|此動作的目標是 Subcube。|  
|*設定*|此動作的目標是集合。|  
|*Hierarchy*|此動作的目標是階層。|  
|*Level*|此動作的目標是層級。|  
|*DimensionMembers*|此動作的目標是維度的成員。|  
|*HierarchyMembers*|此動作的目標是階層的成員。|  
|*LevelMembers*|此動作的目標是層級的成員。|  
|*AttributeMembers*|此動作的目標是屬性的成員。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `TargetType` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ActionTargetType>。  
  
 對應至父系的元素`TargetType`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
