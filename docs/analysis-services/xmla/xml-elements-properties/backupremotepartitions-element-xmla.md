---
title: BackupRemotePartitions 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b13cf011fda2d72b2c013da53753cf34238f46b5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="backupremotepartitions-element-xmla"></a>BackupRemotePartitions 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  決定是否父[備份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)命令會備份與物件相關聯的遠端資料分割。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Backup>  
   ...  
   <BackupRemotePartitions>...</BackupRemotePartitions>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|False|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[備份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如果**BackupRemotePartitions**設**True**、**位置**包含一或多個項目**位置**元素必須包含在**備份**命令或發生錯誤時。 如需有關備份和還原遠端資料分割的詳細資訊，請參閱[備份、 還原，並同步處理資料庫 & #40;XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>另請參閱  
 [Locations 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md)   
 [Location 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)   
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
