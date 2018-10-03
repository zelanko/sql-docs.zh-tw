---
title: ProcessingQuery 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProcessingQuery Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProcessingQuery element
ms.assetid: d18e6f4b-c24c-4f73-8b85-4b6e8a82a695
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 055ec55609d60060385ebcce077119cf61549e1f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051128"
---
# <a name="processingquery-element-assl"></a>ProcessingQuery 元素 (ASSL)
  包含要針對累加式處理狀態通知執行之查詢的參數化文字。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<IncrementalProcessingNotification>  
   ...  
   <ProcessingQuery>...</ProcessingQuery>  
   ...  
</IncrementalProcessingNotification>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[IncrementalProcessingNotification](../objects/incrementalprocessingnotification-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 中的資料表[DataSourceView](../objects/datasourceview-element-assl.md)所參考`ProcessingQuery`同層級元素，來識別[TableID](id-element-assl.md)。  
  
 對應至父系的元素`ProcessingQuery`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
