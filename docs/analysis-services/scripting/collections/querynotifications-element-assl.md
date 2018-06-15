---
title: QueryNotifications 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d3075be5d5f7a2674819fc2a84ff4686e6ae939f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031399"
---
# <a name="querynotifications-element-assl"></a>QueryNotifications 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含集合[QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md)項目提供資訊給[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有關判斷資料來源是否已經修改所執行之查詢的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ProactiveCachingQueryBinding>  
   ...  
   <QueryNotifications>  
      <QueryNotification>...</QueryNotification>  
...</QueryNotifications>  
   ...  
</ProactiveCachingQueryBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ProactiveCachingQueryBinding](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)|  
|子元素|[QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.QueryNotificationCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [集合 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
