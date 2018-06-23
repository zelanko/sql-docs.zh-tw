---
title: MergePartitions 元素 (XMLA) |Microsoft 文件
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
- MergePartitions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#MergePartitions
- microsoft.xml.analysis.mergepartitions
- urn:schemas-microsoft-com:xml-analysis#MergePartitions
helpviewer_keywords:
- MergePartitions command
ms.assetid: cf538189-0629-49b3-8e01-32afba7b020d
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 80f94365da716e08c50a2b3e0ce8df82132ea99e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033096"
---
# <a name="mergepartitions-element-xmla"></a>MergePartitions 元素 (XMLA)
  將一個或多個來源資料分割的資料合併至目標資料分割中，然後刪除來源資料分割。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <MergePartitions>  
      <Sources>...</Sources>  
      <Target>...</Target>  
   </MergePartitions>  
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
|子元素|[來源](../xml-elements-properties/sources-element-xmla.md)，[目標](../xml-elements-properties/target-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Sources` 和 `Target` 元素中的所有物件參考都必須指向相同量值群組中的不同資料分割。 否則，系統將發生錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  