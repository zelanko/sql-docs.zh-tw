---
title: HideMemberIf 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7c2e76ae7cd667327f2eaf464ba790a34d0b253c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032419"
---
# <a name="hidememberif-element-assl"></a>HideMemberIf 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*永遠不會*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Level](../../../analysis-services/scripting/objects/level-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|Value|Description|  
|-----------|-----------------|  
|*永遠不會*|永不隱藏成員。|  
|*OnlyChildWithNoName*|當成員是其父系的唯一子系，而且其名稱為空白時，就會隱藏成員。|  
|*OnlyChildWithParentName*|當成員是父系的唯一子系，而且其名稱與其父系名稱完全相同時，就會隱藏成員。|  
|*NoName*|當成員名稱為空白時，就會隱藏成員。|  
|*ParentName*|當成員名稱與其父系名稱完全相同時，就會隱藏成員。|  
  
## <a name="remarks"></a>備註  
 列舉型別對應至允許的值**HideMemberIf**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.HideIfValue>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
