---
title: Location 元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Location Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.location
- urn:schemas-microsoft-com:xml-analysis#Location
- http://schemas.microsoft.com/analysisservices/2003/engine#Location
helpviewer_keywords:
- Location element
ms.assetid: cea5e776-f435-425a-9bce-812d727a2b71
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 51b0838b9843658b4081f9464c63274631ed74be
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137155"
---
# <a name="location-element-xmla"></a>Location 元素 (XMLA)
  包含遠端伺服器的父代資訊[備份](../xml-elements-commands/backup-element-xmla.md)，[還原](../xml-elements-commands/restore-element-xmla.md)，或[Synchronize](../xml-elements-commands/synchronize-element-xmla.md)命令。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[備份](../xml-elements-commands/backup-element-xmla.md)，[還原](../xml-elements-commands/restore-element-xmla.md)，[同步處理](../xml-elements-commands/synchronize-element-xmla.md)|  
  
## <a name="child-elements"></a>子元素  
  
|上階或父系|子元素|  
|------------------------|-------------------|  
|[備份](id-element-xmla.md)，[檔案](file-element-xmla.md)|  
|[還原](connectionstring-element-xmla.md)， [DataSourceID](datasourceid-element-xmla.md)， [DataSourceType](type-element-xmla.md)，[檔案](file-element-xmla.md)，[資料夾](folders-element-xmla.md)|  
|[同步處理](../xml-elements-commands/synchronize-element-xmla.md)|[ConnectionString](connectionstring-element-xmla.md)， [DataSourceID](datasourceid-element-xmla.md)， [DataSourceType](type-element-xmla.md)，[資料夾](folders-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 如`Backup`命令，`Location`項目會提供建立的遠端執行個體的遠端備份檔案的相關資訊[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 若為 `Restore` 命令，`Location` 元素會提供識別和連接至 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 遠端執行個體的相關資訊，以及用來在該遠端執行個體上還原遠端資料分割的遠端備份檔案。  
  
 若為 `Synchronize` 命令，`Location` 元素會描述要由目標執行個體使用的資料來源或必須與目標執行個體同步處理之來源執行個體上定義的遠端執行個體，端視 `DataSourceType` 父命令之 `Synchronize` 元素的值而定。  
  
 如需有關備份和還原遠端執行個體的詳細資訊，請參閱[備份和還原物件 (XMLA)](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [BackupRemotePartitions 元素&#40;XMLA&#41;](backupremotepartitions-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  