---
title: ProactiveCachingObjectNotificationBinding 資料類型 (ASSL) |Microsoft 文件
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
- ProactiveCachingObjectNotificationBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProactiveCachingObjectNotificationBinding data type
ms.assetid: b3cf5fb6-6121-4f25-8de6-f171792c440d
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c901ea8aa1a11086c8ed6e4bdada9bb1f19acf1f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023639"
---
# <a name="proactivecachingobjectnotificationbinding-data-type-assl"></a>ProactiveCachingObjectNotificationBinding 資料類型 (ASSL)
  定義抽象的衍生的資料類型，表示資訊[ProactiveCaching](../objects/proactivecaching-element-assl.md)有關資料來源變更，在指定的資料表和檢視表或資料表與檢視透過現有資料繫結中的項目如果是需要重建快取。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ProactiveCachingObjectNotificationBinding>  
   <!-- The following elements extend ProactiveCachingBinding -->  
   <NotificationTechnique>...</NotificationTechnique>  
</ProactiveCachingObjectNotificationBinding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[ProactiveCachingBinding](binding-data-type-assl.md)|  
|衍生資料類型|[ProactiveCachingInheritedBinding](inheritedbinding-data-type-assl.md)， [ProactiveCachingTablesBinding](proactivecachingtablesbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[NotificationTechnique](../properties/notificationtechnique-element-assl.md)|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 如需有關`ProactiveCachingBinding`型別，包括資料表的繼承階層架構`ProactiveCachingBinding`類型，請參閱[ProactiveCachingBinding 資料類型&#40;ASSL&#41;](binding-data-type-assl.md)。  
  
 如需有關`Binding`型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表`Binding`型別和繼承階層架構的`Binding`類型，請參閱[繫結資料型別&#40;ASSL&#41;](binding-data-type-assl.md).  
  
 如需 ASSL 中資料繫結的概觀，請參閱[資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ProactiveCachingObjectNotificationBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  