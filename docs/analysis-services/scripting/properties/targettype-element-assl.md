---
title: "TargetType 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- TargetType Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TargetType
helpviewer_keywords:
- TargetType element
ms.assetid: 2c69ea6e-2af7-435b-9841-86117d5554a7
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 49c2fd13925130bfb76730708775f6bb0d5e79ca
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="targettype-element-assl"></a>TargetType 元素 (ASSL)
  識別項目類型中所識別的項目[目標](../../../analysis-services/scripting/properties/target-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action>  
   ...  
   <TargetType>...</TargetType>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
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
  
 列舉型別對應至允許的值**TargetType**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ActionTargetType>。  
  
 對應目的父代的項目**TargetType**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

