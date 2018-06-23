---
title: AttributeName 元素 (XMLA) |Microsoft 文件
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
- AttributeName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#AttributeName
- http://schemas.microsoft.com/analysisservices/2003/engine#AttributeName
- microsoft.xml.analysis.attributename
helpviewer_keywords:
- AttributeName element
ms.assetid: 4dc8260b-522e-46d9-9bd8-22a5a0068982
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 1251de0a3f81a0b3a25d44de5bfbe2e41fa0f90a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037094"
---
# <a name="attributename-element-xmla"></a>AttributeName 元素 (XMLA)
  包含父代所代表之屬性的名稱[屬性](attribute-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Attribute>  
   ...  
   <AttributeName>...</AttributeName>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Attribute](attribute-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [Drop 元素&#40;XMLA&#41;](../xml-elements-commands/drop-element-xmla.md)   
 [插入項目&#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [更新項目&#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [其中的項目&#40;XMLA&#41;](where-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  