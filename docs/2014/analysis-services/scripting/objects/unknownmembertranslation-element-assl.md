---
title: UnknownMemberTranslation 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- UnknownMemberTranslation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- UnknownMemberTranslation
helpviewer_keywords:
- UnknownElementTranslation element
ms.assetid: a4b8cdac-b065-4a44-b251-c5ac1cfe5e6f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7fa7aacc82e91396496a0fd5405c70e9643372c2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48125298"
---
# <a name="unknownmembertranslation-element-assl"></a>UnknownMemberTranslation 元素 (ASSL)
  包含標題的翻譯[UnknownMember](member-element-assl.md)項目[維度](dimension-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<UnknownMemberTranslations>  
   <UnknownMemberTranslation xsi:type="Translation">...</UnknownMemberTranslation>  
</UnknownMemberTranslations>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[轉譯](../data-type/translation-data-type-assl.md)|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[UnknownMemberTranslations](../collections/translations-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`UnknownMemberTranslation`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>另請參閱  
 [Translation 元素&#40;ASSL&#41;](translation-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
