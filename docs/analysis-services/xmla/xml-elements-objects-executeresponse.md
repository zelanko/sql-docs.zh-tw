---
title: "ExecuteResponse 元素 (XMLA) |Microsoft 文件"
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
- ExecuteResponse Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#ExecuteResponse
- http://schemas.microsoft.com/analysisservices/2003/engine#ExecuteResponse
- microsoft.xml.analysis.executeresponse
helpviewer_keywords:
- ExecuteResponse element
ms.assetid: 6edb1b82-da4c-4cd9-9385-bea04032f0eb
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d90ec4cac02bf3429603d095cb91c3bef77cc00d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="xml-elements---objects---executeresponse"></a>XML 項目物件-ExecuteResponse
  包含執行個體所傳回的資訊[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]回應[Execute](../../analysis-services/xmla/xml-elements-methods-execute.md)方法呼叫。  
  
 **命名空間**描述 urn:-microsoft-schemas-microsoft-com:-分析  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ExecuteResponse>  
   <return>  
</ExecuteResponse>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[傳回](../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **ExecuteResponse**項目是最上層的項目之 SOAP 回應的主體內**Execute**方法。  
  
## <a name="see-also"></a>另請參閱  
 [DiscoverResponse 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)   
 [物件 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-objects.md)  
  
  

