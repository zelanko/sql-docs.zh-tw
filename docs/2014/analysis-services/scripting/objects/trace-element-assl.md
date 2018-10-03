---
title: Trace 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Trace Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Trace
helpviewer_keywords:
- Trace element
ms.assetid: dda9136a-a9c1-44a1-b8d3-b0ec4dc65c87
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8951414231fa8730f1babd3638d9e468624b94a9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48056348"
---
# <a name="trace-element-assl"></a>Trace 元素 (ASSL)
  定義可查詢的追蹤。  
  
## <a name="syntax"></a>語法  
  
```  
  
      Profiler syntax  
<Traces>  
   <Trace>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LogFileName>...</LogFileName>  
      <LogFileAppend>...</LogFileAppend>  
      <LogFileSize>...</LogFileSize>  
      <Audit>...</Audit>  
      <LogFileRollover>...</LogFileRollover>  
      <AutoRestart>...</AutoRestart>  
      <StopTime>...</StopTime>  
      <Filter>...</Filter>  
      <Events>...</Events>  
      <Annotations>...</Annotations>  
   </Trace>  
</Traces>  
```  
  
```  
  
      Extended Events syntax  
<Traces>  
   <Trace>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <XEvent>...</XEvent>  
      <Annotations>...</Annotations>  
   </Trace>  
</Traces>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[追蹤](../collections/traces-element-assl.md)|  
|子元素|[註釋](../collections/annotations-element-assl.md)，[稽核](../properties/audit-element-assl.md)， [AutoRestart](../properties/autorestart-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)，[描述](../properties/description-element-assl.md)，[事件](../collections/events-element-assl.md)，[篩選](../properties/filter-element-trace-assl.md)，[識別碼](../properties/id-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)， [LogFileAppend](../properties/logfileappend-element-assl.md)， [LogFileName](../properties/name-element-assl.md)， [LogFileRollover](../properties/logfilerollover-element-assl.md)， [LogFileSize](../properties/logfilesize-element-assl.md)，[名稱](../properties/name-element-assl.md)， [StopTime](../properties/stoptime-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器項目&#40;ASSL&#41;](server-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
