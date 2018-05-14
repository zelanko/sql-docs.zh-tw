---
title: Synchronize 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5c3a4d20c7799281f40fa6ae13e89010cebe1ec6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="synchronize-element-xmla"></a>Synchronize 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  同步處理[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫與另一個現有的資料庫。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Synchronize>  
      <Source>...</Source>  
      <SynchronizeSecurity>...</SynchronizeSecurity>  
      <ApplyCompression>...</ApplyCompression>  
      <Locations>...</Locations>  
   </Synchronize>  
</Command>  
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
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[ApplyCompression](../../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md)，[位置](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md)，[來源](../../../analysis-services/xmla/xml-elements-properties/source-element-synchronize-xmla.md)， [SynchronizeSecurity](../../../analysis-services/xmla/xml-elements-properties/synchronizesecurity-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **Synchronize**命令會在目標資料庫同步處理來源執行個體和資料庫中指定**來源**項目。 （選擇性） **Synchronize**命令會同步處理來源資料庫上定義的遠端資料分割。  
  
 根據儲存在備份檔案中，物件所使用的儲存模式**Synchronize**命令在下表所列，會同步處理資訊。  
  
|儲存模式|資訊|  
|------------------|-----------------|  
|多維度 OLAP (MOLAP)|來源資料、彙總和中繼資料|  
|混合式 OLAP (HOLAP)|彙總和中繼資料|  
|關聯式 OLAP (ROLAP)|中繼資料|  
  
 期間**Synchronize**命令時，讀取的鎖定放在來源資料庫和目標資料庫上放置寫入鎖定。 發行後發行兩種鎖定**Synchronize**命令已完成。  
  
 如需有關同步處理資料庫的詳細資訊，請參閱[備份、 還原及同步處理資料庫&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Backup 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [批次元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [Parallel 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)   
 [Restore 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
