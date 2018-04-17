---
title: Restore 元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Restore Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Restore
- urn:schemas-microsoft-com:xml-analysis#Restore
- microsoft.xml.analysis.restore
helpviewer_keywords:
- Restore command
ms.assetid: bb5a0c92-3927-4fa4-975b-6e4d79e0a912
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4aca6a4028390f9edd704ae6671f1904ea627f2c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="restore-element-xmla"></a>Restore 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]還原[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫從備份檔案。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Restore>  
      <DatabaseName>...</DatabaseName>  
      <DatabaseID>...</DatabaseID>  
      <File>...</File>  
      <Security>...</Security>  
      <AllowOverwrite>...</AllowOverwrite>  
      <Password>...</Password>  
      <Locations>...</Locations>  
      <DbStorageLocation>...</DbStorageLocation>  
   </Restore>  
</Command>  
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
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[AllowOverwrite](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md)， [DatabaseName](../../../analysis-services/xmla/xml-elements-properties/databasename-element-xmla.md)， [DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md)，[檔案](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)，[位置](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md)，[密碼](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md)，[安全性](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md)， [DbStorageLocation](../../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)|  
  
## <a name="remarks"></a>備註  
 **還原**命令還原[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中所指定資料庫**DatabaseName**從項目備份檔案以及選擇性地還原遠端資料分割從遠端備份檔案。  
  
 根據儲存在備份檔中之物件所使用的儲存模式， **Restore** 命令可以還原如下表所列的資訊。  
  
|儲存模式|資訊|  
|------------------|-----------------|  
|多維度 OLAP (MOLAP)|來源資料、彙總和中繼資料|  
|混合式 OLAP (HOLAP)|彙總和中繼資料|  
|關聯式 OLAP (ROLAP)|中繼資料|  
  
 期間**還原**命令的獨佔鎖定位於[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中所指定資料庫**DatabaseName**項目。 當 **Restore** 命令完成之後，就會釋放這個鎖定。  
  
 如需有關備份和還原資料庫的詳細資訊，請參閱[備份、 還原，並同步處理資料庫 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
> [!IMPORTANT]  
>  對於每個備份檔案，執行還原命令的使用者必須擁有從針對每個檔案所指定之備份位置讀取的權限。 若要還原沒有安裝在伺服器上的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫，使用者也必須是該 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員。 若要覆寫 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫，使用者必須具有下列其中一個角色： [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員，或在即將還原之資料庫上擁有完整控制權 (管理員) 權限的資料庫角色成員。  
  
> [!NOTE]  
>  還原現有的資料庫之後，還原資料庫的使用者可能會喪失已還原資料庫的存取權。 如果在執行備份時，使用者不是伺服器角色的成員，也不是擁有完整控制權 (管理員) 權限的資料庫角色成員，就可能會發生存取權喪失的情況。  
  
## <a name="see-also"></a>請參閱  
 [Backup 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [批次元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [Parallel 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)   
 [同步處理項目 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
