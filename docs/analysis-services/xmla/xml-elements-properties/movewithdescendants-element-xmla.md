---
title: MoveWithDescendants 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 518c95efa36c6a234036a1c7f293c3df8283749a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37969188"
---
# <a name="movewithdescendants-element-xmla"></a>MoveWithDescendants 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  指出是否屬性成員的下階也會更新它的父系[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Update>  
   ...  
   <MoveWithDescendants>...</MoveWithDescendants>  
   ...  
</Update>  
```  
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|False|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **MoveWithDescendants**元素會決定是否**更新**命令應該不僅更新所識別的屬性成員[屬性](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)項目，但也會一併更新這些屬性成員的子系。  
  
> [!NOTE]  
>  這個元素只會套用至父子式階層中的屬性成員。  
  
 如需有關更新成員的詳細資訊，請參閱 <<c0> [ 插入、 更新和卸除成員&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。</c0>  
  
## <a name="see-also"></a>另請參閱
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
