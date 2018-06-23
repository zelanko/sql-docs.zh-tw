---
title: EventID 元素 (ASSL) |Microsoft 文件
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
- EventID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EventID
helpviewer_keywords:
- EventID element
ms.assetid: a6b2ee50-1753-496c-af5c-206d63f2542b
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b5ee579bd4bc20bea12b1dbb9490a7f9c93fde32
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036194"
---
# <a name="eventid-element-assl"></a>EventID 元素 (ASSL)
  可唯一識別[事件](../objects/event-element-assl.md)要擷取的一部分的項目[追蹤](../objects/trace-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Event>  
  
      <EventID>...</EventID>  
  
</Event>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[事件](../objects/event-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目`EventID`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.TraceEvent>。  
  
## <a name="see-also"></a>另請參閱  
 [Events 元素&#40;ASSL&#41;](../collections/events-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  