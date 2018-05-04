---
title: EventID 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- EventID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- EventID
helpviewer_keywords:
- EventID element
ms.assetid: a6b2ee50-1753-496c-af5c-206d63f2542b
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a22181941c8bb2776c641870fd6c602c68651a41
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="eventid-element-assl"></a>EventID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  可唯一識別[事件](../../../analysis-services/scripting/objects/event-element-assl.md)要擷取的一部分的項目[追蹤](../../../analysis-services/scripting/objects/trace-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Event>  
  
      <EventID>...</EventID>  
  
</Event>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[事件](../../../analysis-services/scripting/objects/event-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目**EventID**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.TraceEvent>。  
  
## <a name="see-also"></a>另請參閱  
 [Events 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
