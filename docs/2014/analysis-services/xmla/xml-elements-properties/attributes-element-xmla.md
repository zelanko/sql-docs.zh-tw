---
title: 屬性元素 (XMLA) |Microsoft 文件
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
- Attributes Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Attributes
- microsoft.xml.analysis.attributes
- urn:schemas-microsoft-com:xml-analysis#Attributes
helpviewer_keywords:
- Attributes element
ms.assetid: c0393de8-44e8-46de-af78-1fd66c218521
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: bad3c0949f4c6c241a81bf4a8b90834aadfdfdf3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035306"
---
# <a name="attributes-element-xmla"></a>Attributes 元素 (XMLA)
  包含集合[屬性](attribute-element-xmla.md)父元素所使用[插入](../xml-elements-commands/insert-element-xmla.md)或[更新](../xml-elements-commands/update-element-xmla.md)命令，或父系[其中](where-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Insert > <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Attributes>  
      <Attribute>...</Attribute>  
   </Attributes>  
   ...  
</Insert>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[插入](../xml-elements-commands/insert-element-xmla.md)，[更新](../xml-elements-commands/update-element-xmla.md)，[位置](where-element-xmla.md)|  
|子元素|[Attribute](attribute-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  