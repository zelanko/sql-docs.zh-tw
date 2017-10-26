---
title: "DataSourceType 元素 (XMLA) |Microsoft 文件"
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
- DataSourceType Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DataSourceType
- microsoft.xml.analysis.datasourcetype
- http://schemas.microsoft.com/analysisservices/2003/engine#DataSourceType
helpviewer_keywords:
- DataSourceType element
ms.assetid: f5a348b1-911b-4139-832e-4bcb6d80a728
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 998d12b9426eb656c57d56dd4440926a968dffad
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="datasourcetype-element-xmla"></a>DataSourceType 元素 (XMLA)
  指出是否[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)指定的項目[還原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)或[Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)命令在本機或遠端。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Location>  
   ...  
   <DataSourceType>...</DataSourceType>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*遠端*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **DataSourceType**元素會決定資料來源是否已由**位置**元素包含本機資料來源或遠端資料來源。 如需有關備份和還原遠端資料分割的詳細資訊，請參閱[備份、 還原，並同步處理資料庫 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*本機*|**位置**項目會定義本機資料來源。 使用此值時，如果**還原**和**Synchronize**命令使用中定義的資訊**位置**從其中擷取項目來更新資料來源，備份檔案中指定**檔案**元素**備份**命令或資料庫中指定**來源**元素**同步處理**識別中的命令**DataSourceID**元素**位置**項目。<br /><br /> 這個值允許使用關聯式 OLAP (ROLAP) 儲存的物件在還原或同步處理之後，針對其資料和中繼資料使用不同的資料庫。<br /><br /> 注意： ROLAP 資料，例如維度資料表或回寫資料表中的資料不還原或同步處理。 只有 ROLAP 物件的中繼資料會進行還原或同步處理。|  
|*遠端*|**位置**項目會定義遠端資料來源。 使用此值時，如果**還原**和**Synchronize**命令使用中定義的資訊**位置**還原或同步處理遠端資料分割的項目從備份檔案中指定**檔案**元素**備份**命令或資料庫中指定**來源**項目**Synchronize**命令中識別之遠端執行個體**DataSourceID**的**位置**項目。|  
  
## <a name="see-also"></a>另請參閱  
 [ConnectionString 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md)   
 [DataSourceID 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

