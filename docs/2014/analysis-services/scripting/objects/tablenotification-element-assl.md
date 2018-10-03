---
title: TableNotification 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- TableNotification Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- TableNotification element
ms.assetid: 3afd075a-74f9-428c-b527-ee497cbe71e7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b8fea5896667afa1952e088faa97b9a0797f9864
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48184268"
---
# <a name="tablenotification-element-assl"></a>TableNotification 元素 (ASSL)
  包含的資訊[ProactiveCaching](proactivecaching-element-assl.md)有關之資料表或檢視已經過修改的資料來源中的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<TableNotifications>  
   <TableNotification>  
      <DbTableName>...</DbTableName>  
      <DbSchemaName>...</DbSchemaName>  
...</TableNotification>  
</TableNotifications>  
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
|父元素|[TableNotifications](../collections/tablenotifications-element-assl.md)|  
|子元素|[DbSchemaName](../properties/name-element-assl.md)， [DbTableName](../properties/dbtablename-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.TableNotification>。  
  
## <a name="see-also"></a>另請參閱  
 [ProactiveCachingTablesBinding 資料類型&#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [ProactiveCachingObjectNotificationBinding 資料類型&#40;ASSL&#41;](../data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)   
 [ProactiveCachingBinding 資料類型&#40;ASSL&#41;](../data-type/proactivecachingbinding-data-type-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
