---
title: Expression 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Expression Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Expression
helpviewer_keywords:
- Expression element
ms.assetid: a9491b21-5279-4531-b6a5-9e8022060dd8
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3d7ba9bbfeddef0d4d7466141cabb914f4289034
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37155315"
---
# <a name="expression-element-assl"></a>Expression 元素 (ASSL)
  包含定義父元素內容的多維度運算式 (MDX) 運算式。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CellPermission> <!-- or StandardAction -->  
   ...  
   <Expression>...</Expression>  
   ...  
</CellPermission>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CellPermission](../objects/cellpermission-element-assl.md)， [StandardAction](../data-type/action-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 針對`CellPermission`項目，`Expression`項目包含邏輯 MDX 運算式來識別適用於所指定的權限的資料格[存取](access-element-assl.md)項目`CellPermission`項目。 如果 `Expression` 元素之 `CellPermission` 元素的值是空白的，系統就會忽略 `CellPermission` 元素。  
  
 若為 `StandardAction` 元素，`Expression` 元素會包含代表動作內容的 MDX 運算式。 如果 `Expression` 元素之 `StandardAction` 元素的值是空白的，系統就會忽略 `StandardAction` 元素。  
  
 在「分析管理物件」(AMO) 物件模型中對應至父系的元素是 <xref:Microsoft.AnalysisServices.CellPermission> 和 <xref:Microsoft.AnalysisServices.StandardAction>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
