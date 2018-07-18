---
title: Name 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Name Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Name
- urn:schemas-microsoft-com:xml-analysis#Name
- microsoft.xml.analysis.name
helpviewer_keywords:
- Name element
ms.assetid: cc1a93df-0b1b-4c38-9183-4f11c26fea6a
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 088dd6aa9ce8d9ecae3e3a8f293f64b3ddc93c70
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194228"
---
# <a name="name-element-xmla"></a>Name 元素 (XMLA)
  包含父代之屬性成員的名稱[屬性](attribute-element-xmla.md)或是[轉譯](translation-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Attribute> <!-- or Translation -->  
   ...  
   <Name>...</Name>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|上階或父系：|基數|  
|[Attribute](attribute-element-xmla.md)|1-1：只出現一次的必要元素。|  
|[轉譯](translation-element-xmla.md)|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[屬性](attribute-element-xmla.md)，[轉譯](translation-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 若為 `Attribute` 元素，`Name` 元素會包含在進行 `Insert` 或 `Update` 命令期間要分別插入或更新之屬性成員的名稱。  
  
 若為 `Translation` 元素，`Name` 元素會包含屬性成員的標題，並以 `Language` 父物件之 `Translation` 元素指定的語言顯示。 如果您沒有指定 `Name` 元素或者它包含空字串，系統就會使用包含 `Name` 元素之 `Attribute` 元素的 `Translation` 元素。  
  
## <a name="see-also"></a>另請參閱  
 [插入項目&#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [語言項目&#40;XMLA&#41;](language-element-xmla.md)   
 [更新項目&#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
