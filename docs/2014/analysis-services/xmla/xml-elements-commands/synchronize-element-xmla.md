---
title: Synchronize 元素 (XMLA) |Microsoft Docs
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
- Synchronize Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.synchronize
- urn:schemas-microsoft-com:xml-analysis#Synchronize
- http://schemas.microsoft.com/analysisservices/2003/engine#Synchronize
helpviewer_keywords:
- Synchronize command
ms.assetid: 9401323c-feff-409a-a9da-94aee47e0563
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f88b07721d391c1f834ed93d21039753728081d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187095"
---
# <a name="synchronize-element-xmla"></a>Synchronize 元素 (XMLA)
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[ApplyCompression](../xml-elements-properties/applycompression-element-xmla.md)，[位置](../xml-elements-properties/locations-element-xmla.md)，[來源](../xml-elements-properties/source-element-synchronize-xmla.md)， [SynchronizeSecurity](../xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Synchronize` 命令會同步處理目標資料庫與 `Source` 元素中指定的來源執行個體和資料庫。 另外，`Synchronize` 命令會同步處理來源資料庫上定義的遠端資料分割。  
  
 根據儲存在備份檔案中之物件所使用的儲存模式，`Synchronize` 命令會同步處理資訊，如下表所列。  
  
|儲存模式|資訊|  
|------------------|-----------------|  
|多維度 OLAP (MOLAP)|來源資料、彙總和中繼資料|  
|混合式 OLAP (HOLAP)|彙總和中繼資料|  
|關聯式 OLAP (ROLAP)|中繼資料|  
  
 在 `Synchronize` 命令執行期間，系統會在來源資料庫上放置讀取鎖定，而在目標資料庫上放置寫入鎖定。 當 `Synchronize` 命令完成時，系統就會釋放這兩個鎖定。  
  
 如需有關同步處理資料庫的詳細資訊，請參閱 <<c0> [ 備份、 還原和同步處理資料庫&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [備份項目&#40;XMLA&#41;](backup-element-xmla.md)   
 [批次項目&#40;XMLA&#41;](batch-element-xmla.md)   
 [平行項目的&#40;XMLA&#41;](../xml-elements-properties/parallel-element-xmla.md)   
 [Restore 元素&#40;XMLA&#41;](restore-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
