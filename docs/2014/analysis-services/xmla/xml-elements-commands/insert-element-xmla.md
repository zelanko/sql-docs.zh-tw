---
title: Insert 元素 (XMLA) |Microsoft Docs
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
- Insert Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Insert
- http://schemas.microsoft.com/analysisservices/2003/engine#Insert
- microsoft.xml.analysis.insert
helpviewer_keywords:
- Insert command
ms.assetid: d1137033-cc19-4bcb-b93d-8575f17bea6b
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cfec9c9a5be2cc19c609bc9de788a4a0df388e5d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169289"
---
# <a name="insert-element-xmla"></a>Insert 元素 (XMLA)
  將屬性成員插入維度中。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Insert>  
      <Object>...</Object>  
      <Attributes>...</Attributes>  
   </Insert>  
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
|子元素|[屬性](../xml-elements-properties/attributes-element-xmla.md)，[物件](../xml-elements-properties/object-element-dimension-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Insert` 命令會將新的屬性成員插入可寫入維度中。  
  
 如需有關刪除成員的詳細資訊，請參閱 <<c0> [ 插入、 更新和卸除成員&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [卸除項目&#40;XMLA&#41;](drop-element-xmla.md)   
 [更新項目&#40;XMLA&#41;](update-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
