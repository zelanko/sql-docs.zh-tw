---
title: QueryNotification 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- QueryNotification Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- QueryNotification element
ms.assetid: 0ee06730-81ff-4913-96e6-f39b6f181650
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4eddd5a96c5c5ab541ba9349d7b664b110589a74
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177730"
---
# <a name="querynotification-element-assl"></a>QueryNotification 元素 (ASSL)
  包含有關判斷資料來源是否已經修改所執行之查詢的 [ProactiveCaching](proactivecaching-element-assl.md) 元素的資訊。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<QueryNotifications>  
   <QueryNotification>  
      <Query>...</Query>  
...</QueryNotification>  
</QueryNotifications>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|1-n：出現一次以上的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[QueryNotifications](../collections/querynotifications-element-assl.md)|  
|子元素|[查詢](../properties/query-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.QueryNotification>。  
  
## <a name="see-also"></a>另請參閱  
 [ProactiveCachingQueryBinding 資料類型&#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
