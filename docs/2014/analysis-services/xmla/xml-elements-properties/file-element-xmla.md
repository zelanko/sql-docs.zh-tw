---
title: 檔案元素 (XMLA) |Microsoft 文件
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
- File Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.file
- http://schemas.microsoft.com/analysisservices/2003/engine#File
- urn:schemas-microsoft-com:xml-analysis#File
helpviewer_keywords:
- File element
ms.assetid: 3dfd0e9b-746b-4ce5-8a95-610d2e573739
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 644e08e68ef38338d5b93c5abc7afe211c04c935
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135010"
---
# <a name="file-element-xmla"></a>File 元素 (XMLA)
  識別要父系所使用的檔案[備份](../xml-elements-commands/backup-element-xmla.md)或[還原](../xml-elements-commands/restore-element-xmla.md)命令，或父系[位置](location-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <File>...</File>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[備份](../xml-elements-commands/backup-element-xmla.md)，[位置](location-element-xmla.md)，[還原](../xml-elements-commands/restore-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `File` 元素包含 UNC 檔案名稱，而且父元素會決定 `File` 元素的使用方式。  
  
 若為 `Backup` 命令，`File` 元素就會決定 `Backup` 命令所建立之備份檔案的名稱。 如果路徑未指定檔案名稱的一部分，在指定的路徑`BackupDir`執行個體的組態屬性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]用。 如果指定的檔案已經存在，除非 `AllowOverwrite` 父命令的 `Backup` 元素設定為 `True`，否則就會發生錯誤。  
  
 若為 `Restore` 命令，`File` 元素就會決定要由 `Restore` 命令還原之備份檔案的名稱。  
  
 若為 `Location` 元素，`File` 元素會針對包含遠端資料分割的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體描述遠端備份檔案。 如需有關備份和還原遠端資料分割的詳細資訊，請參閱[備份、 還原及同步處理資料庫&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [AllowOverwrite 元素&#40;XMLA&#41;](allowoverwrite-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  