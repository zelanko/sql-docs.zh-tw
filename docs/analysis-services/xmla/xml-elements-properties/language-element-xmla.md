---
title: Language 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4b2e3a188a9681508473394a6323457cc4fa1726
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036826"
---
# <a name="language-element-xmla"></a>Language 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含地區設定識別碼 (LCID) 的父代[翻譯](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Translation>  
   ...  
   <Language>...</Language>  
   ...  
</Translation>  
```  
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|Integer|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[轉譯](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **語言**項目會指定父元素所使用的 LCID**轉譯**若要將指派的項目**名稱**項目之父代**轉譯**項目之屬性成員，指定的語言，期間**插入**或是**更新**命令。  
  
## <a name="see-also"></a>另請參閱
 [插入項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [名稱項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md)   
 [更新項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
