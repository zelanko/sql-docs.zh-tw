---
title: "HierarchyInfo 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: HierarchyInfo Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#HierarchyInfo
- microsoft.xml.analysis.hierarchyinfo
- urn:schemas-microsoft-com:xml-analysis#HierarchyInfo
helpviewer_keywords: HierarchyInfo element
ms.assetid: b4472251-1f1d-4233-a8e6-407397862ab4
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 25659220c3a65b3741e3859e2e92f3047c8d6d56
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="hierarchyinfo-element-xmla"></a>HierarchyInfo 元素 (XMLA)
  代表包含父系的單一階層[AxisInfo](../../../analysis-services/xmla/xml-elements-properties/axisinfo-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AxisInfo>  
   ...  
   <HierarchyInfo name="string">  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </HierarchyInfo>  
   ...  
</AxisInfo>  
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
|父元素|[AxisInfo](../../../analysis-services/xmla/xml-elements-properties/axisinfo-element-xmla.md)|  
|子元素|[標題](../../../analysis-services/xmla/xml-elements-properties/caption-element-xmla.md)， [DisplayInfo](../../../analysis-services/xmla/xml-elements-properties/displayinfo-element-xmla.md)， [LName](../../../analysis-services/xmla/xml-elements-properties/lname-element-xmla.md)， [LNum](../../../analysis-services/xmla/xml-elements-properties/lnum-element-xmla.md)， [UName](../../../analysis-services/xmla/xml-elements-properties/uname-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|Attribute|說明|  
|---------------|-----------------|  
|名稱|需要**字串**屬性。 階層的名稱。|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>請參閱＜  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
