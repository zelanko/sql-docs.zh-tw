---
title: "Location 元素 (XMLA) |Microsoft 文件"
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
- Location Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.location
- urn:schemas-microsoft-com:xml-analysis#Location
- http://schemas.microsoft.com/analysisservices/2003/engine#Location
helpviewer_keywords:
- Location element
ms.assetid: cea5e776-f435-425a-9bce-812d727a2b71
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 57d724e1ed2aeae526077af50700e9fad504d29a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="location-element-xmla"></a>Location 元素 (XMLA)
  包含遠端伺服器的父代資訊[備份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)，[還原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)，或[Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Location>  
```  
  
```  
  
<File>...</File> <!-- for Backup and Restore only -->  
<DataSourceID>...</DataSourceID>  
<DataSourceType>...</DataSourceType> <!-- for Restore and Synchronize only -->  
<ConnectionString>...</ConnectionString> <!-- for Restore and Synchronize only -->  
<Folders>...</Folders> <!-- for Restore and Synchronize only -->  
```  
  
```  
  
   </Location>  
   ...  
</Backup>  
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
|父元素|[備份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)，[還原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)，[同步處理](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|子元素|請參閱下表。|  
  
|上階或父系|子元素|  
|------------------------|-------------------|  
|[備份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|[DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)，[檔案](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)|  
|[Restore](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|[ConnectionString](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md)， [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)， [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md)，[檔案](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)，[資料夾](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
|[同步處理](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|[ConnectionString](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md)， [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)， [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md)，[資料夾](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 如**備份**命令，**位置**項目會提供建立的遠端執行個體的遠端備份檔案的相關資訊[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 如**還原**命令，**位置**項目會提供資訊識別和連接至遠端[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體，以及用來還原遠端的遠端備份檔案該遠端執行個體上的資料分割。  
  
 如**Synchronize**命令，**位置**元素描述的目標執行個體所使用的資料來源，或是必須與同步處理來源執行個體上定義的遠端執行個體目標執行個體的值而定**DataSourceType**父項目**Synchronize**命令。  
  
 如需有關備份和還原遠端執行個體的詳細資訊，請參閱[備份和還原物件 (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [BackupRemotePartitions 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

