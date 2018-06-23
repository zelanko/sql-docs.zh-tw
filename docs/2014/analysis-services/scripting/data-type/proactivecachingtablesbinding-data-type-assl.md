---
title: ProactiveCachingTablesBinding 資料類型 (ASSL) |Microsoft 文件
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
- ProactiveCachingTablesBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProactiveCachingTablesBinding data type
ms.assetid: f6b3f6fc-757c-4b1e-bb3a-d26482888d14
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ed926bb00b0593cef9d82d4b829325c8f21ca5ac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036883"
---
# <a name="proactivecachingtablesbinding-data-type-assl"></a>ProactiveCachingTablesBinding 資料類型 (ASSL)
  定義衍生的資料類型，表示資訊[ProactiveCaching](../objects/proactivecaching-element-assl.md)有關指定之資料表和檢視表需要重建快取中的資料來源變更的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ProactiveCachingTablesBinding>  
   <!-- The following elements extend ProactiveCachingObjectNotificationBinding -->  
   <TableNotification>...</TableNotification>  
</ProactiveCachingTablesBinding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[ProactiveCachingObjectNotificationBinding](binding-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[TableNotification](../objects/tablenotification-element-assl.md)|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 如需有關`ProactiveCachingBinding`型別，包括資料表的繼承階層架構`ProactiveCachingBinding`類型，請參閱[ProactiveCachingBinding 資料類型&#40;ASSL&#41;](proactivecachingbinding-data-type-assl.md)。  
  
 如需有關`Binding`型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表`Binding`型別和繼承階層架構的`Binding`類型，請參閱[繫結資料型別&#40;ASSL&#41;](binding-data-type-assl.md).  
  
 如需 ASSL 中資料繫結的概觀，請參閱[資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ProactiveCachingTablesBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  