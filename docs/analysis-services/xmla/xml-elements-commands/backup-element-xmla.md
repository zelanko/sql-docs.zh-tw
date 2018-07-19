---
title: 備份元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e00a4991226779a91e16806dbe15973d946ec69
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38007148"
---
# <a name="backup-element-xmla"></a>Backup 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Analysis Services 將資料庫備份至備份檔案。  
  
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
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[AllowOverwrite](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md)， [ApplyCompression](../../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md)， [BackupRemotePartitions](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md)，[檔案](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)，[位置](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md)， [物件](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)，[密碼](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md)，[安全性](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **備份**命令會備份[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中所指定資料庫[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)要備份的檔案，然後選擇性地備份遠端資料分割到遠端備份檔項目。 如果**物件**項目以外的其他參考的物件[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫，則會發生錯誤。  
  
 **Backup** 命令所備份的資訊取決於物件在資料庫中所使用的儲存模式。 下表會識別根據所使用之儲存模式備份的資訊。  
  
|儲存模式|備份的資訊|  
|------------------|-----------------------------------|  
|多維度 OLAP (MOLAP)|來源資料、彙總和中繼資料|  
|混合式 OLAP (HOLAP)|彙總和中繼資料|  
|關聯式 OLAP (ROLAP)|中繼資料|  
  
 期間**備份**命令上, 放置一個共用的鎖定[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中所指定資料庫**物件**項目。 當 **Backup** 命令完成時，就會釋出共用鎖定。  
  
 多個**備份**可以以平行方式執行命令，如果命令都會納入[平行](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)集合[批次](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)命令。 **Parallel** 集合可將資料庫同時備份到多個備份檔。  
  
 如需有關備份和還原資料庫的詳細資訊，請參閱 <<c0> [ 備份、 還原和同步處理資料庫&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。</c0>  
  
> [!IMPORTANT]  
>  對於每個備份檔案，執行備份命令的使用者必須擁有寫入針對每個檔案所指定之備份位置的權限。 此外，使用者必須具有下列其中一個角色： [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員，或在即將備份之資料庫上擁有「完整控制 (系統管理員)」權限的資料庫角色成員。  
  
## <a name="see-also"></a>另請參閱
 [Restore 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [同步處理項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
