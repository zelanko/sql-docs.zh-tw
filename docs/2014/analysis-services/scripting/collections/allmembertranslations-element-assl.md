---
title: AllMemberTranslations 元素 (ASSL) |Microsoft 文件
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
- AllMemberTranslations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AllMemberTranslations
helpviewer_keywords:
- AllMemberTranslations element
ms.assetid: 982ee2bf-c88d-4da5-a679-7a6b08a48a0d
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b2a1a8b9b72895c69cb8d415d00d633be99ebc99
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135701"
---
# <a name="allmembertranslations-element-assl"></a>AllMemberTranslations 元素 (ASSL)
  包含集合[轉譯](../objects/translation-element-assl.md)元素之 All 成員標題[階層](../objects/hierarchy-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Hierarchy>  
   ...  
   <AllMemberTranslations>  
      <AllMemberTranslation xsi:type="Translation">...  
            </AllMemberTranslation>  
   </AllMemberTranslations>  
      ...  
</Hierarchy>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無 (集合)|  
|預設值|無 (集合)|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Hierarchy](../objects/hierarchy-element-assl.md)|  
|子元素|[AllMemberTranslation](../objects/allmembertranslation-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目`AllMemberTranslations`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Hierarchy>。  
  
## <a name="see-also"></a>另請參閱  
 [Translation 元素&#40;ASSL&#41;](../objects/translation-element-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  