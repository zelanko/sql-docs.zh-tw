---
title: Folder 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 184ae189e07a76eaf4fa3d68914c209927f48ff7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="folder-element-xmla"></a>Folder 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含更新的檔案系統儲存位置[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)項目期間[還原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)或[Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Folders>  
   ...  
   <Folder>  
      <Original>...</Original>  
      <New>...</New>  
   </Folder>  
   ...  
</Folders>  
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
|父元素|[資料夾](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
|子元素|[新](../../../analysis-services/xmla/xml-elements-properties/new-element-xmla.md)，[原始](../../../analysis-services/xmla/xml-elements-properties/original-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **資料夾**項目，如果指定，會變更儲存體位置的物件所包含的備份檔案 (如**還原**命令) 或來源執行個體上的資料庫 (如**同步處理**命令)，會比對值**原始**元素的值**新增**項目。  
  
 如需有關備份和還原物件的詳細資訊，請參閱[備份、 還原，並同步處理資料庫 & #40;XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>另請參閱  
 [StorageLocation 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)   
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
