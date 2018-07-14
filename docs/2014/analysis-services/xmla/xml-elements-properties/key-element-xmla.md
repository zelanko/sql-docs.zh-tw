---
title: 索引鍵元素 (XMLA) |Microsoft Docs
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
- Key Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Key
- urn:schemas-microsoft-com:xml-analysis#Key
- microsoft.xml.analysis.key
helpviewer_keywords:
- Key element
ms.assetid: 09d3cd48-49f7-4b58-b8bb-ca75b81bb02f
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1f98ae6863f0aab25149ee4f8a69ef13b65da974
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37213758"
---
# <a name="key-element-xmla"></a>Key 元素 (XMLA)
  包含屬性成員的成員索引鍵值。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Keys>  
   ...  
   <Key>...</Key>  
   ...  
</Keys>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|任意|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[索引鍵](keys-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素所使用的資料類型應該與指定屬性之適當索引鍵資料行的資料類型相符。 如果沒有針對 `Key` 父元素指定 `Attribute` 元素，則 `AttributeName` 父元素中指定的 `Name` 和 `Attribute` 元素就會用來識別要修改的屬性成員。  
  
## <a name="see-also"></a>另請參閱  
 [屬性項目&#40;XMLA&#41;](attribute-element-xmla.md)   
 [AttributeName 元素&#40;XMLA&#41;](name-element-xmla.md)   
 [卸除項目&#40;XMLA&#41;](../xml-elements-commands/drop-element-xmla.md)   
 [插入項目&#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [KeyColumn 元素&#40;ASSL&#41;](../../scripting/objects/column-element-assl.md)   
 [更新項目&#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [其中的項目&#40;XMLA&#41;](where-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
