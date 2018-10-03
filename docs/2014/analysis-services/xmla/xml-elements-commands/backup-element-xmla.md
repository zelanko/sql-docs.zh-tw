---
title: 備份元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Backup Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Backup
- http://schemas.microsoft.com/analysisservices/2003/engine#Backup
- microsoft.xml.analysis.backup
helpviewer_keywords:
- Backup command
ms.assetid: 5bcbc14c-9db9-45b2-99de-f3a265bcb0c4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 59efda960de14ae96b0c7c948b66c89980d8f990
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48216496"
---
# <a name="backup-element-xmla"></a>Backup 元素 (XMLA)
  備份[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫備份至備份檔案。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Backup>  
      <Object>...</Object>  
      <File>...</File>  
      <Security>...</Security>  
      <ApplyCompression>...</ApplyCompression>  
      <AllowOverwrite>...</AllowOverwrite>  
      <Password>...</Password>  
      <BackupRemotePartitions>...</BackupRemotePartitions>  
      <Locations>...</Locations>  
   </Backup>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[AllowOverwrite](../xml-elements-properties/allowoverwrite-element-xmla.md)， [ApplyCompression](../xml-elements-properties/applycompression-element-xmla.md)， [BackupRemotePartitions](../xml-elements-properties/backupremotepartitions-element-xmla.md)，[檔案](../xml-elements-properties/file-element-xmla.md)，[位置](../xml-elements-properties/locations-element-xmla.md)， [物件](../xml-elements-properties/object-element-xmla.md)，[密碼](../xml-elements-properties/password-element-xmla.md)，[安全性](../xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Backup`命令會備份[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中所指定的資料庫[物件](../xml-elements-properties/object-element-xmla.md)要備份的檔案，然後選擇性地備份遠端資料分割到遠端備份檔項目。 如果 `Object` 元素參考 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫以外的物件，會發生錯誤。  
  
 哪些資訊`Backup`備份取決於資料庫中的物件所使用的儲存模式的命令。 下表會識別根據所使用之儲存模式備份的資訊。  
  
|儲存模式|備份的資訊|  
|------------------|-----------------------------------|  
|多維度 OLAP (MOLAP)|來源資料、彙總和中繼資料|  
|混合式 OLAP (HOLAP)|彙總和中繼資料|  
|關聯式 OLAP (ROLAP)|中繼資料|  
  
 期間`Backup`命令上, 放置一個共用的鎖定[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中所指定資料庫`Object`項目。 共用的鎖定釋放在`Backup`命令已完成。  
  
 多個`Backup`可以以平行方式執行命令，如果命令中包含[平行](../xml-elements-properties/parallel-element-xmla.md)的集合[批次](batch-element-xmla.md)命令。 `Parallel` 集合可將資料庫同時備份到多個備份檔。  
  
 如需有關備份和還原資料庫的詳細資訊，請參閱 <<c0> [ 備份、 還原和同步處理資料庫&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。</c0>  
  
> [!IMPORTANT]  
>  對於每個備份檔案，執行備份命令的使用者必須擁有寫入針對每個檔案所指定之備份位置的權限。 此外，使用者必須具有下列其中一個角色： [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員，或在即將備份之資料庫上擁有「完整控制 (系統管理員)」權限的資料庫角色成員。  
  
## <a name="see-also"></a>另請參閱  
 [Restore 元素&#40;XMLA&#41;](restore-element-xmla.md)   
 [同步處理項目&#40;XMLA&#41;](synchronize-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
