---
title: ColumnID 元素 (EventColumn) (ASSL) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e60f8ada3852bdbd09c8f7831b4af0110bb6a630
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031069"
---
# <a name="columnid-element-eventcolumn-assl"></a>ColumnID 元素 (EventColumn) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Columns 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/columns-element-assl.md)   
 [Event 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/event-element-assl.md)   
 [Events 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
