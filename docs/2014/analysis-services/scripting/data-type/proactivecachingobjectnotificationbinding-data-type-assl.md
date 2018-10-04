---
title: ProactiveCachingObjectNotificationBinding 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 201774fd7b46bf3d4fc30dfe304c8ffd80f7c6eb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48080378"
---
# <a name="proactivecachingobjectnotificationbinding-data-type-assl"></a>ProactiveCachingObjectNotificationBinding 資料類型 (ASSL)
  定義抽象的衍生的資料類型，表示資訊[ProactiveCaching](../objects/proactivecaching-element-assl.md)有關資料來源變更，在指定的資料表和檢視表或資料表和檢視透過現有資料繫結所識別的項目需要重建快取。  
  
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
|父元素|None|  
|子元素|[NotificationTechnique](../properties/notificationtechnique-element-assl.md)|  
|衍生的元素|None|  
  
## <a name="remarks"></a>備註  
 如需詳細資訊`ProactiveCachingBinding`型別，包括繼承階層的資料表`ProactiveCachingBinding`類型，請參閱[ProactiveCachingBinding 資料類型&#40;ASSL&#41;](binding-data-type-assl.md)。  
  
 如需詳細資訊`Binding`型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表`Binding`型別和繼承階層`Binding`類型，請參閱[繫結資料類型 &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 如需 ASSL 中資料繫結的概觀，請參閱 <<c0> [ 資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。</c0>  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.ProactiveCachingObjectNotificationBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
