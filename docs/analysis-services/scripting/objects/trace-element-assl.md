---
title: "Trace 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Trace Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Trace
helpviewer_keywords: Trace element
ms.assetid: dda9136a-a9c1-44a1-b8d3-b0ec4dc65c87
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4e7b32ad2396eded2ba9f222879121cdca4f2544
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="trace-element-assl"></a>Trace 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義可查詢的追蹤。  
  
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
      <AutoRestart>...</AutoRestart>
      <XEvent>...</XEvent>  
      <Annotations>...</Annotations>  
   </Trace>  
</Traces>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[追蹤](../../../analysis-services/scripting/collections/traces-element-assl.md)|  
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[稽核](../../../analysis-services/scripting/properties/audit-element-assl.md)， [AutoRestart](../../../analysis-services/scripting/properties/autorestart-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)，[描述](../../../analysis-services/scripting/properties/description-element-assl.md)，[事件](../../../analysis-services/scripting/collections/events-element-assl.md)，[篩選](../../../analysis-services/scripting/properties/filter-element-trace-assl.md)，[識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)， [LogFileAppend](../../../analysis-services/scripting/properties/logfileappend-element-assl.md)， [LogFileName](../../../analysis-services/scripting/properties/logfilename-element-assl.md)， [LogFileRollover](../../../analysis-services/scripting/properties/logfilerollover-element-assl.md)， [LogFileSize](../../../analysis-services/scripting/properties/logfilesize-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)， [StopTime](../../../analysis-services/scripting/properties/stoptime-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>請參閱  
 [Server 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
