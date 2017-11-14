---
title: "ColumnID 元素 (EventColumn) (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ColumnID Element (EventColumn)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ColumnID
helpviewer_keywords:
- ColumnID element
ms.assetid: c4f4fbad-9d70-4de2-8cf7-caee80a4a1e4
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 38cac2f8ddbe9fd79e14308ff9587099c1991426
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="columnid-element-eventcolumn-assl"></a>ColumnID 元素 (EventColumn) (ASSL)
  包含資訊的一部分，針對某個事件擷取的資料行的識別碼 (ID)[追蹤](../../../analysis-services/scripting/objects/trace-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
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
|父元素|[EventColumn](../../../analysis-services/scripting/data-type/eventcolumn-data-type-assl.md)|  
|子元素|無。|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**ColumnID**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.TraceColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [Columns 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/columns-element-assl.md)   
 [Event 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/event-element-assl.md)   
 [Events 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

