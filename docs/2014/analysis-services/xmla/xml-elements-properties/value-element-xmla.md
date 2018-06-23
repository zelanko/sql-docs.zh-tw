---
title: 值元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Value Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.value
- urn:schemas-microsoft-com:xml-analysis#Value
- http://schemas.microsoft.com/analysisservices/2003/engine#Value
helpviewer_keywords:
- Value element
ms.assetid: f87ca7f8-d9fe-4730-a706-5d50fcfe21df
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 7a422298e8d1b77f3d036b4cea5761dc6dc6dde4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023402"
---
# <a name="value-element-xmla"></a>Value 元素 (XMLA)
  包含所需的值的[屬性](attribute-element-xmla.md)要新增的項目[插入](../xml-elements-commands/insert-element-xmla.md)命令，或[儲存格](cell-element-xmla.md)更新的項目[UpdateCells](../xml-elements-commands/updatecells-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Attribute> <!-- or Cell --!>  
   ...  
   <Value>...</Value>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|任意|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[屬性](attribute-element-xmla.md)，[資料格](cell-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 若為 `Attribute` 元素，`Value` 元素會包含認可 `Insert` 命令之後此成員應該包含的所需值。 如需有關插入成員的詳細資訊，請參閱[插入、 更新和卸除成員&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
 若為 `Cell` 元素，`Value` 元素會包含認可 `UpdateCells` 命令之後此資料格應該包含的所需值。 針對該資料格儲存於回寫資料表中的實際值就是資料格之原始值與資料格之所需值之間的差異。  
  
 這個元素所使用的資料類型應該與要更新之資料格的資料類型相符。  
  
 如需更新資料格的詳細資訊，請參閱[更新資料格 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CellOrdinal 元素&#40;XMLA&#41;](cellordinal-element-xmla.md)   
 [插入項目&#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [UpdateCells 元素&#40;XMLA&#41;](../xml-elements-commands/updatecells-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  