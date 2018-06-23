---
title: 其中元素 (XMLA) |Microsoft 文件
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
- Where Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Where
- microsoft.xml.analysis.where
- http://schemas.microsoft.com/analysisservices/2003/engine#Where
helpviewer_keywords:
- Where element
ms.assetid: 81fb4190-3379-4ddf-8795-a0772f3b92bb
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 4e63d2ecd6f20d374c6746c7d3bc77ad455f1ef6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146377"
---
# <a name="where-element-xmla"></a>Where 元素 (XMLA)
  定義 [Drop](../xml-elements-commands/drop-element-xmla.md) 或 [Update](../xml-elements-commands/update-element-xmla.md) 父命令所使用的篩選條件。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Drop> <!-- or Update -->  
   ...  
   <Where>  
      <Attributes>...</Attributes>  
   </Where>  
   ...  
</Insert>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Drop](../xml-elements-commands/drop-element-xmla.md)、 [Update](../xml-elements-commands/update-element-xmla.md)|  
|子元素|[屬性](attributes-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 如`Drop`命令，`Where`元素結合[DeleteWithDescendants](deletewithdescendants-element-xmla.md)元素會識別要卸除的屬性成員的範圍。  
  
 若為 `Update` 命令，`Where` 元素會識別要更新之屬性成員的範圍。 您可以使用 `Attributes` 父命令之 `Update` 集合和 `Attributes` 元素之 `Where` 集合中包含的屬性組合來更新多個屬性成員。  
  
 如需刪除和更新屬性成員的詳細資訊，請參閱[插入、更新和卸除成員 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  