---
title: 檔案元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb80a091c9b9585a6efc29088d15139db7033efb
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34575190"
---
# <a name="file-element-xmla"></a>File 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  識別要父系所使用的檔案[備份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)或[還原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)命令，或父系[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element relationships table -->  
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
|父元素|[備份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)，[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)，[還原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **檔案**元素包含 UNC 檔案名稱，而且父元素會決定使用**檔案**項目。  
  
 如**備份**命令，**檔案**元素會決定所建立之備份檔案的名稱**備份**命令。 如果路徑未指定檔案名稱的一部分，在指定的路徑**BackupDir**使用 Analysis Services 執行個體的組態屬性。 如果指定的檔案已經存在，除非發生錯誤**AllowOverwrite**父元素之**備份**命令設定為**True**。  
  
 如**還原**命令，**檔案**元素會決定要還原的備份檔案的名稱**還原**命令。  
  
 如**位置**項目，**檔案**元素描述遠端備份檔案[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]包含遠端資料分割的執行個體。 如需有關備份和還原遠端資料分割的詳細資訊，請參閱[備份、 還原及同步處理資料庫&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>另請參閱
 [AllowOverwrite 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md)   
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
