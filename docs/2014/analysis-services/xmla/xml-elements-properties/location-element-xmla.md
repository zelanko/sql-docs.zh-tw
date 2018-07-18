---
title: Location 元素 (XMLA) |Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6674d88797e738c4120a7cafae3d12a71e52e36f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295388"
---
# <a name="location-element-xmla"></a>Location 元素 (XMLA)
  包含父代的遠端伺服器相關資訊[備份](../xml-elements-commands/backup-element-xmla.md)，[還原](../xml-elements-commands/restore-element-xmla.md)，或[同步處理](../xml-elements-commands/synchronize-element-xmla.md)命令。  
  
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
 針對`Backup`命令，`Location`項目會提供建立的遠端執行個體的遠端備份檔案的相關資訊[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 若為 `Restore` 命令，`Location` 元素會提供識別和連接至 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 遠端執行個體的相關資訊，以及用來在該遠端執行個體上還原遠端資料分割的遠端備份檔案。  
  
 若為 `Synchronize` 命令，`Location` 元素會描述要由目標執行個體使用的資料來源或必須與目標執行個體同步處理之來源執行個體上定義的遠端執行個體，端視 `DataSourceType` 父命令之 `Synchronize` 元素的值而定。  
  
 如需有關備份和還原遠端執行個體的詳細資訊，請參閱 <<c0> [ 備份和還原物件 (XMLA)](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [BackupRemotePartitions 元素&#40;XMLA&#41;](backupremotepartitions-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
