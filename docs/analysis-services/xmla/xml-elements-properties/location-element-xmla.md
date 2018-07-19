---
title: Location 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4953981e7657706a986e9a2407f6786ff676a854
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38004490"
---
# <a name="location-element-xmla"></a>Location 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含父代的遠端伺服器相關資訊[備份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)，[還原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)，或[同步處理](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element relationships table -->  
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
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
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
 針對**備份**命令**位置**項目會提供 Analysis Services 的遠端執行個體建立遠端備份檔案的相關資訊。  
  
 針對**還原**命令**位置**項目提供的資訊識別和連線到遠端[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體，以及用來還原遠端的遠端備份檔案該遠端執行個體上的資料分割。  
  
 針對**同步處理**命令**位置**元素描述的目標執行個體所使用的資料來源，或是必須與同步處理來源執行個體上定義的遠端執行個體目標執行個體的值而定**DataSourceType**父元素**同步處理**命令。  
  
 如需有關備份和還原遠端執行個體的詳細資訊，請參閱 <<c0> [ 備份和還原物件 (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>另請參閱
 [BackupRemotePartitions 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md)   
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
