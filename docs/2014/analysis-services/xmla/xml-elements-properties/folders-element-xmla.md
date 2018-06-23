---
title: Folders 元素 (XMLA) |Microsoft 文件
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
- Folders Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.folders
- http://schemas.microsoft.com/analysisservices/2003/engine#Folders
- urn:schemas-microsoft-com:xml-analysis#Folders
helpviewer_keywords:
- Folders element
ms.assetid: fefb0469-22ea-4804-8dc3-9c49825b32f1
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: c9042b2960a6efcce592779f5f17fd58fd98d693
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134455"
---
# <a name="folders-element-xmla"></a>Folders 元素 (XMLA)
  包含在進行 [Restore](folder-element-xmla.md) 或 [Synchronize](location-element-xmla.md) 命令期間由 [Location](../xml-elements-commands/restore-element-xmla.md) 父元素所使用之 [Folder](../xml-elements-commands/synchronize-element-xmla.md) 元素的集合。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Location>  
   ...  
   <Folders>  
      <Folder>...</Folder>  
   </Folders>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無 (集合)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[位置](location-element-xmla.md)|  
|子元素|[資料夾](folder-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [Restore 元素&#40;XMLA&#41;](../xml-elements-commands/restore-element-xmla.md)   
 [同步處理項目&#40;XMLA&#41;](../xml-elements-commands/synchronize-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  