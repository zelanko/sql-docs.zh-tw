---
title: OverrideBehavior 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- OverrideBehavior Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- OverrideBehavior element
ms.assetid: 6a5b361a-6061-4b73-b1a7-1237fb77606c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 88cf3dd287e1b55fee5377e2238d4d7c738cfe16
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203618"
---
# <a name="overridebehavior-element-assl"></a>OverrideBehavior 元素 (ASSL)
  表示所描述之關聯性的覆寫行為[AttributeRelationship](../objects/attributerelationship-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <OverrideBehavior>...</OverrideBehavior>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*強式*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributeRelationship](../objects/attributerelationship-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `OverrideBehavior` 元素會決定相關屬性上的定位如何影響屬性上的定位。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*強式*|指出 AttributeRelationship 元素所描述之關聯性的覆寫行為。 決定一個屬性的定位如何影響其他位置。|  
|*無*|沒有影響。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `OverrideBehavior` 允許值的列舉是 <xref:Microsoft.AnalysisServices.OverrideBehavior>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
