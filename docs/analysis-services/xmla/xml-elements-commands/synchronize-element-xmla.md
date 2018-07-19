---
title: Synchronize 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 11804b9b6ca9ac430bdb47c0b9050b8c6995cf7f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38007179"
---
# <a name="synchronize-element-xmla"></a>Synchronize 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  同步處理 Analysis Services 資料庫與另一個現有的資料庫。  
  
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
|子元素|[ApplyCompression](../../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md)，[位置](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md)，[來源](../../../analysis-services/xmla/xml-elements-properties/source-element-synchronize-xmla.md)， [SynchronizeSecurity](../../../analysis-services/xmla/xml-elements-properties/synchronizesecurity-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **Synchronize**命令與來源執行個體同步處理目標資料庫，並在指定的資料庫**來源**項目。 （選擇性）**同步處理**命令會同步處理在來源資料庫上定義的遠端資料分割。  
  
 根據儲存在備份檔案中，物件所使用的儲存模式**同步處理**命令在下表所示，會同步處理資訊。  
  
|儲存模式|資訊|  
|------------------|-----------------|  
|多維度 OLAP (MOLAP)|來源資料、彙總和中繼資料|  
|混合式 OLAP (HOLAP)|彙總和中繼資料|  
|關聯式 OLAP (ROLAP)|中繼資料|  
  
 期間**同步處理**命令中，在來源資料庫上設定讀取的鎖定，並在目標資料庫上放置寫入鎖定。 之後便會釋放這兩個鎖定**同步處理**命令已完成。  
  
 如需有關同步處理資料庫的詳細資訊，請參閱 <<c0> [ 備份、 還原和同步處理資料庫&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。</c0>  
  
## <a name="see-also"></a>另請參閱
 [備份項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [批次項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [平行項目的&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)   
 [Restore 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
