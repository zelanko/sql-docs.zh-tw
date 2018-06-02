---
title: Drop 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e9230180eae63b204d6441b08eb9a81dae240d15
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575450"
---
# <a name="drop-element-xmla"></a>Drop 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  從維度中刪除屬性成員。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Drop>  
      <Object>...</Object>  
      <DeleteWithDescendants>...</DeleteWithDescendants>  
      <Where>...</Where>  
   </Drop>  
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
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[DeleteWithDescendants](../../../analysis-services/xmla/xml-elements-properties/deletewithdescendants-element-xmla.md)，[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)，[位置](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **卸除**命令刪除從已啟用寫入的維度屬性成員。  
  
 如需有關刪除成員的詳細資訊，請參閱[插入、 更新和卸除成員&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
## <a name="see-also"></a>另請參閱
 [插入項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [更新項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
