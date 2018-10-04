---
title: IncrementalProcessingNotification 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- IncrementalProcessingNotification Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- IncrementalProcessingNotification data type
ms.assetid: 66e27f92-65c1-4a34-b9c2-bfbb5aeb7d7c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d02257847043aaa93db216d3d25cca91f9a76130
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48068898"
---
# <a name="incrementalprocessingnotification-data-type-assl"></a>IncrementalProcessingNotification 資料類型 (ASSL)
  定義衍生的資料類型，表示資訊[ProactiveCaching](../objects/proactivecaching-element-assl.md)有關判斷累加式處理進度所執行之查詢的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<IncrementalProcessingNotification>  
   <!-- The following elements extend QueryNotification -->  
   <TableID>...</TableID>  
   <ProcessingQuery>...</ProcessingQuery>  
</IncrementalProcessingNotification>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[QueryNotification](../objects/querynotification-element-assl.md)|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[ProcessingQuery](../properties/query-element-assl.md)， [TableID](../properties/id-element-assl.md)|  
|衍生的元素|None|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>。  
  
## <a name="see-also"></a>另請參閱  
 [ProactiveCachingQueryBinding 資料類型&#40;ASSL&#41;](binding-data-type-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
