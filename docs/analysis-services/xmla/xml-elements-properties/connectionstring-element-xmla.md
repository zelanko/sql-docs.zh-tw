---
title: "ConnectionString 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ConnectionString Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.connectionstring
- urn:schemas-microsoft-com:xml-analysis#ConnectionString
- http://schemas.microsoft.com/analysisservices/2003/engine#ConnectionString
helpviewer_keywords:
- ConnectionString element
ms.assetid: 3b0575aa-79ed-4f14-ae7e-dd587af4cdb1
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b6c6227db17c74b4c33d07abfcd809ae01bc3a9a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="connectionstring-element-xmla"></a>ConnectionString 元素 (XMLA)
  包含父系所使用的連接字串[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)或[來源](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Location> <!-- or Source -->  
   ...  
   <ConnectionString>...</ConnectionString>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|請參閱下表。|  
  
|上階或父系|基數|  
|------------------------|-----------------|  
|[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|1-1：只出現一次的必要元素。|  
|[Source](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)，[來源](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如**位置**項目， **ConnectionString**元素包含所使用的連接字串**還原**或**Synchronize**命令來更新本機資料來源或連接到遠端執行個體。  
  
 如**來源**項目， **ConnectionString**元素包含所使用的連接字串**同步處理**命令連接到來源執行個體。  
  
 如需有關備份和還原物件的詳細資訊，請參閱[備份、 還原，並同步處理資料庫 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>另請參閱  
 [Restore 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [同步處理項目 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

