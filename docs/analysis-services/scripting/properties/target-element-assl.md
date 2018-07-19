---
title: 目標元素 (ASSL) |Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 98ec5c729f5735343f5eaa87e5232fcfb138cf38
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38045776"
---
# <a name="target-element-assl"></a>Target 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  識別的目標[動作](../../../analysis-services/scripting/objects/action-element-assl.md)項目。  
  
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
|父元素|[動作](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個項目的預期值而定的值[TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md)父元素**動作**。 下表描述的期望值**目標**的值為基礎**TargetType**。  
  
|TargetType 值|預期的值|  
|----------------------|--------------------|  
|*Cube*|Cube 的名稱。|  
|*資料格*|Subcube 運算式。|  
|*設定*|集合運算式或命名集的名稱。<br /><br /> 注意： 無法使用子選擇陳述式。|  
|*階層架構 HierarchyMembers*|階層的名稱。|  
|*維度 DimensionMembers*|維度的名稱。|  
|*層級 LevelMembers*|層級的名稱。|  
|*屬性 AttributeMembers*|屬性的名稱。|  
  
 對應至父系的元素**目標**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
