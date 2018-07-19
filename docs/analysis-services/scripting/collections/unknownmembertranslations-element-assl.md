---
title: UnknownMemberTranslations 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ebcb9ac03a2b8765946c2cd26e913ec541245bb4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031129"
---
# <a name="unknownmembertranslations-element-assl"></a>UnknownMemberTranslations 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含標題的翻譯集合[UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md)維度的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Dimension>  
   ...  
   <UnknownMemberTranslations>  
      <UnknownMemberTranslation xsi:type="Translation ">...</UnknownMemberTranslation>  
      </UnknownMemberTranslations>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|子元素|[UnknownMemberTranslation](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md)型別的[轉譯](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**UnknownMemberTranslations**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>另請參閱  
 [Translation 資料類型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)   
 [集合 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
