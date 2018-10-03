---
title: Update 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Update Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Update
- microsoft.xml.analysis.update
- http://schemas.microsoft.com/analysisservices/2003/engine#Update
helpviewer_keywords:
- Update command [XMLA]
ms.assetid: 324dcc16-865d-4d0a-b393-2b06c18ac807
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b9663fa3d44b91f53ac20a5a1b1dba117f7a2574
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200128"
---
# <a name="update-element-xmla"></a>Update 元素 (XMLA)
  更新維度中的屬性成員。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Update>  
      <Object>...</Object>  
      <MoveWithDescendants>...</MoveWithDescendants>  
      <Attributes>...</Attributes>  
      <Where>...</Where>  
   </Update>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[屬性](../xml-elements-properties/attributes-element-xmla.md)， [MoveWithDescendants](../xml-elements-properties/movewithdescendants-element-xmla.md)，[物件](../xml-elements-properties/object-element-dimension-xmla.md)，[位置](../xml-elements-properties/where-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Update` 命令會在可寫入維度內部移動屬性成員。  
  
 如需有關更新成員的詳細資訊，請參閱 <<c0> [ 插入、 更新和卸除成員&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [卸除項目&#40;XMLA&#41;](drop-element-xmla.md)   
 [插入項目&#40;XMLA&#41;](insert-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
