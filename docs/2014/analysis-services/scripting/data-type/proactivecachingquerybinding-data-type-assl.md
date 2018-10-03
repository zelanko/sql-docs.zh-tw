---
title: ProactiveCachingQueryBinding 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProactiveCachingQueryBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProactiveCachingQueryBinding data type
ms.assetid: c1b06e50-9e68-40db-bdab-fc2cb3a8ff64
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7b9c4aea38bb66277467275d2cf89a04cc3144a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087628"
---
# <a name="proactivecachingquerybinding-data-type-assl"></a>ProactiveCachingQueryBinding 資料類型 (ASSL)
  定義衍生的資料類型，表示資訊[ProactiveCaching](../objects/proactivecaching-element-assl.md)有關資料表和檢視，識別執行指定之查詢所需要重建快取中的資料來源變更的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ProactiveCachingQueryBinding>  
   <!-- The following elements extend ProactiveCachingBinding -->  
   <RefreshInterval>...</RefreshInterval>  
   <QueryNotification>...</QueryNotification>  
</ProactiveCachingQueryBinding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[ProactiveCachingBinding](binding-data-type-assl.md)|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[QueryNotification](../objects/querynotification-element-assl.md)， [RefreshInterval](../properties/refreshinterval-element-assl.md)|  
|衍生的元素|None|  
  
## <a name="remarks"></a>備註  
 如需詳細資訊`ProactiveCachingBinding`型別，包括繼承階層的資料表`ProactiveCachingBinding`類型，請參閱[ProactiveCachingBinding 資料類型&#40;ASSL&#41;](binding-data-type-assl.md)。  
  
 如需詳細資訊`Binding`型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表`Binding`型別和繼承階層`Binding`類型，請參閱[繫結資料類型 &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 如需 ASSL 中資料繫結的概觀，請參閱 <<c0> [ 資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。</c0>  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.ProactiveCachingQueryBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
