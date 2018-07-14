---
title: HideMemberIf 元素 (ASSL) |Microsoft Docs
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
- HideMemberIf Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- HideMemberIf
helpviewer_keywords:
- HideMemberIf element
ms.assetid: ff0e6b19-6216-43ac-ba76-1628da8c333b
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0829804ae0225c848da3583c429e39d9bc176821
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187025"
---
# <a name="hidememberif-element-assl"></a>HideMemberIf 元素 (ASSL)
  指出是否應向用戶端應用程式隱藏層級中的成員，以及何時隱藏。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Level>  
   ...  
   <HideMemberIf>...</HideMemberIf>  
   ...  
</Level>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*永遠不會*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Level](../objects/level-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*永遠不會*|永不隱藏成員。|  
|*OnlyChildWithNoName*|當成員是其父系的唯一子系，而且其名稱為空白時，就會隱藏成員。|  
|*OnlyChildWithParentName*|當成員是父系的唯一子系，而且其名稱與其父系名稱完全相同時，就會隱藏成員。|  
|*NoName*|當成員名稱為空白時，就會隱藏成員。|  
|*ParentName*|當成員名稱與其父系名稱完全相同時，就會隱藏成員。|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應至 `HideMemberIf` 允許值的列舉是 <xref:Microsoft.AnalysisServices.HideIfValue>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
