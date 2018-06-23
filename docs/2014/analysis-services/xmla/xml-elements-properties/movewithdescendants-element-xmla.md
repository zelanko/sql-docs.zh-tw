---
title: MoveWithDescendants 元素 (XMLA) |Microsoft 文件
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
- MoveWithDescendants Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.movewithdescendants
- http://schemas.microsoft.com/analysisservices/2003/engine#MoveWithDescendants
- urn:schemas-microsoft-com:xml-analysis#MoveWithDescendants
helpviewer_keywords:
- MoveWithDescendants element
ms.assetid: d02285b6-1801-4da9-8e2b-9ab008e25558
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 975044359f2855f8cced46ca2045c2c397e4234b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036633"
---
# <a name="movewithdescendants-element-xmla"></a>MoveWithDescendants 元素 (XMLA)
  指出是否屬性成員的下階也會更新它的父系[更新](../xml-elements-commands/update-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Update>  
   ...  
   <MoveWithDescendants>...</MoveWithDescendants>  
   ...  
</Update>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|False|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Update](../xml-elements-commands/update-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `MoveWithDescendants`元素會決定是否`Update`命令應該不僅更新所識別的屬性成員[屬性](attributes-element-xmla.md)項目，但是，這些屬性成員的下階要一併更新。  
  
> [!NOTE]  
>  這個元素只會套用至父子式階層中的屬性成員。  
  
 如需有關更新成員的詳細資訊，請參閱[插入、 更新和卸除成員&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  