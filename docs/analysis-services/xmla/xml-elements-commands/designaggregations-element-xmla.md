---
title: "DesignAggregations 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DesignAggregations Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DesignAggregations
- microsoft.xml.analysis.designaggregations
- http://schemas.microsoft.com/analysisservices/2003/engine#DesignAggregations
helpviewer_keywords:
- DesignAggregations command
ms.assetid: 4c419dbc-7405-40aa-8ddd-6b46685a297d
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0a20166ec005068195d93ee22c40837213944445
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="designaggregations-element-xmla"></a>DesignAggregations 元素 (XMLA)
  針對建立的彙總設計的彙總[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <DesignAggregations>  
      <Object>...</Object>  
      <Time>...</Time>  
      <Steps>...</Steps>  
      <Optimization>...</Optimization>  
      <Storage>...</Storage>  
      <Materialize>...</Materialize>  
      <Queries>...</Queries>  
   </DesignAggregations>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[具體化](../../../analysis-services/xmla/xml-elements-properties/materialize-element-xmla.md)，[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)，[最佳化](../../../analysis-services/xmla/xml-elements-properties/optimization-element-xmla.md)，[查詢](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md)，[步驟](../../../analysis-services/xmla/xml-elements-properties/steps-element-xmla.md)，[儲存體](../../../analysis-services/xmla/xml-elements-properties/storage-element-xmla.md)，[時間](../../../analysis-services/xmla/xml-elements-properties/time-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **DesignAggregations**命令用來產生彙總設計所儲存的彙總定義。 然後，彙總設計可以用來具體化分割區的彙總而且可以在分割區之間重複使用。  
  
## <a name="see-also"></a>另請參閱  
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

