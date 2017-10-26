---
title: "DeleteWithDescendants 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DeleteWithDescendants Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#DeleteWithDescendants
- microsoft.xml.analysis.deletewithdescendants
- urn:schemas-microsoft-com:xml-analysis#DeleteWithDescendants
helpviewer_keywords:
- DeleteWithDescendants element
ms.assetid: adfc9437-aaa7-4364-bcdb-128fcc9a410d
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6d0a75a3cb5de9aba6cd6aeccd90d8342442847c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="deletewithdescendants-element-xmla"></a>DeleteWithDescendants 元素 (XMLA)
  指出是否屬性成員的下階也會一併刪除父代[卸除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Drop>  
   ...  
   <DeleteWithDescendants>...</DeleteWithDescendants>  
   ...  
</Drop>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|False|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[卸除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **DeleteWithDescendants**元素會決定是否**卸除**命令應該刪除所識別的屬性成員[其中](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)項目，但是，這些屬性成員的子系會一併卸除。  
  
> [!NOTE]  
>  這個元素只會套用至父子式階層中的屬性成員。  
  
 如需刪除和更新屬性成員的詳細資訊，請參閱[插入、更新和卸除成員 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

