---
title: ColumnID 元素 (EventColumn) (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: c887b78b04f45752a406d618a84078a8e002abba
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="columnid-element-eventcolumn-assl"></a>ColumnID 元素 (EventColumn) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含資訊的一部分，針對某個事件擷取的資料行的識別碼 (ID)[追蹤](../../../analysis-services/scripting/objects/trace-element-assl.md)項目。  
  
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
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[EventColumn](../../../analysis-services/scripting/data-type/eventcolumn-data-type-assl.md)|  
|子元素|無。|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**ColumnID**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.TraceColumn>。  
  
## <a name="see-also"></a>請參閱  
 [Columns 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/columns-element-assl.md)   
 [Event 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/event-element-assl.md)   
 [Events 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
