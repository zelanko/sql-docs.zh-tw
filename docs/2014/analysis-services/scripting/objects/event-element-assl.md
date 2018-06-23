---
title: Event 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Event Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EVENT
helpviewer_keywords:
- Event element
ms.assetid: c7911bcd-e601-4a96-a6d8-20b7c7375ff2
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 441d8758f25092d1e10128a44ace8d12f3eee79a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132522"
---
# <a name="event-element-assl"></a>Event 元素 (ASSL)
  定義`Event`要擷取成一部分[追蹤](trace-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Events>  
   <Event>  
      <EventID>...</EventID>  
      <Columns>...</Columns>  
   </Event>  
</Events>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-n：出現一次以上的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[事件](../collections/events-element-assl.md)|  
|子元素|[資料行](../collections/columns-element-assl.md)， [EventID](../properties/id-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.TraceEvent>。  
  
## <a name="see-also"></a>另請參閱  
 [追蹤項目&#40;ASSL&#41;](trace-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  