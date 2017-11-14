---
title: "PartitionID 元素 (XMLA) |Microsoft 文件"
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
apiname:
- PartitionID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#PartitionID
- urn:schemas-microsoft-com:xml-analysis#PartitionID
- microsoft.xml.analysis.partitionid
helpviewer_keywords:
- PartitionID element
ms.assetid: 19f06454-9719-488e-aeb6-3fc879313351
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 849b49c76f26b8631fc328da55826936a96d4c77
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="partitionid-element-xmla"></a>PartitionID 元素 (XMLA)
  識別父元素中包含物件參考的資料分割。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Object> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <PartitionID>...</PartitionID>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|請參閱下表。|  
  
|上階或父系|基數|  
|------------------------|-----------------|  
|[Source](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)、[Target](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)|1-1：只出現一次的必要元素。|  
|All others|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Object](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)、[ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)、[Source](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)、[Target](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

