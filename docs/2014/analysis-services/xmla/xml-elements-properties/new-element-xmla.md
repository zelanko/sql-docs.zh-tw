---
title: New 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- New Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#New
- microsoft.xml.analysis.new
- urn:schemas-microsoft-com:xml-analysis#New
helpviewer_keywords:
- New element
ms.assetid: 1321adcb-67f7-40f0-8f20-b17c1d3e3f17
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 01f159352499625bf5065c96fcbd057590570610
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222378"
---
# <a name="new-element-xmla"></a>New 元素 (XMLA)
  包含所使用的新檔案系統儲存位置[資料夾](folder-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Folder>  
   ...  
   <New>...</New>  
   ...  
</Folder>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料夾](folder-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `New` 元素包含 UNC 路徑，它會在進行 `Original` 或 `Folder` 命令期間分別取代還原或同步處理之所有物件的 `Restore` 父元素所包含的 `Synchronize` 元素值。 系統會針對每個 Cube、量值群組或資料分割比較 `Original` 元素的值與 `StorageLocation` 元素的值，而且如果找到相符項目，就會在還原或同步處理期間使用這個元素的值來更新物件的 `StorageLocation`。  
  
 如需有關備份和還原物件的詳細資訊，請參閱 <<c0> [ 備份和還原物件 (XMLA)](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [原始項目&#40;XMLA&#41;](original-element-xmla.md)   
 [Restore 元素&#40;XMLA&#41;](../xml-elements-commands/restore-element-xmla.md)   
 [StorageLocation 元素&#40;ASSL&#41;](../../scripting/properties/storagelocation-element-assl.md)   
 [同步處理項目&#40;XMLA&#41;](../xml-elements-commands/synchronize-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
