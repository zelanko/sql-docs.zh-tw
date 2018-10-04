---
title: ColumnID 元素 (EventColumn) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ColumnID Element (EventColumn)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ColumnID
helpviewer_keywords:
- ColumnID element
ms.assetid: c4f4fbad-9d70-4de2-8cf7-caee80a4a1e4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4eeb9954f3318a9286865454b6eb61a15f4d4236
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48216388"
---
# <a name="columnid-element-eventcolumn-assl"></a>ColumnID 元素 (EventColumn) (ASSL)
  包含資訊的一部分，針對某個事件擷取的資料行的識別碼 (ID)[追蹤](../objects/trace-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[EventColumn](../data-type/eventcolumn-data-type-assl.md)|  
|子元素|無。|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`ColumnID`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.TraceColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [資料行的項目&#40;ASSL&#41;](../collections/columns-element-assl.md)   
 [事件項目的&#40;ASSL&#41;](../objects/event-element-assl.md)   
 [Events 元素&#40;ASSL&#41;](../collections/events-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
