---
title: Folder 元素 (XMLA) |Microsoft Docs
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
- Folder Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.folder
- http://schemas.microsoft.com/analysisservices/2003/engine#Folder
- urn:schemas-microsoft-com:xml-analysis#Folder
helpviewer_keywords:
- Folder element
ms.assetid: 87b305b0-57e3-4ec3-9d80-f1bcf3ce7540
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9bc961679619f15211689b4f118f511edbadac8c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37283914"
---
# <a name="folder-element-xmla"></a>Folder 元素 (XMLA)
  包含更新的檔案系統儲存位置[位置](location-element-xmla.md)項目期間[還原](../xml-elements-commands/restore-element-xmla.md)或是[同步處理](../xml-elements-commands/synchronize-element-xmla.md)命令。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料夾](folders-element-xmla.md)|  
|子元素|[新](new-element-xmla.md)，[原始](original-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 如果您指定了 `Folder` 元素，它會將備份檔案 (適用於 `Restore` 命令) 或來源執行個體上的資料庫 (適用於 `Synchronize` 命令) 所包含而且符合 `Original` 元素之值的物件儲存位置變更為 `New` 元素的值。  
  
 如需有關備份和還原物件的詳細資訊，請參閱 <<c0> [ 備份、 還原和同步處理資料庫&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [StorageLocation 元素&#40;ASSL&#41;](../../scripting/properties/storagelocation-element-assl.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
