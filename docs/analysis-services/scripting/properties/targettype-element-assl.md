---
title: TargetType 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fe1e79254f4daef21634b4e9c5b2144c857bfee0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039392"
---
# <a name="targettype-element-assl"></a>TargetType 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|*階層架構*|此動作的目標是階層。|  
|*Level*|此動作的目標是層級。|  
|*DimensionMembers*|此動作的目標是維度的成員。|  
|*HierarchyMembers*|此動作的目標是階層的成員。|  
|*LevelMembers*|此動作的目標是層級的成員。|  
|*AttributeMembers*|此動作的目標是屬性的成員。|  
  
 列舉型別對應至允許的值**TargetType**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ActionTargetType>。  
  
 對應目的父代的項目**TargetType**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
