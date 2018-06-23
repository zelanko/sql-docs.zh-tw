---
title: UnknownMember 元素 (ASSL) |Microsoft 文件
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
- UnknownMember Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- UnknownMember
helpviewer_keywords:
- UnknownMember element
ms.assetid: 5558961e-e3c6-4f4e-817d-5b12b0734c03
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 85bc7a517642ccc5b4386f65e7b4a9c89d757ce6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031099"
---
# <a name="unknownmember-element-assl"></a>UnknownMember 元素 (ASSL)
  指出未知的成員是否可見。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Dimension>  
      ...  
   <UnknownMember>...</UnknownMember>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*無*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Dimension](../objects/dimension-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*可見*|未知的成員存在並顯示出來。|  
|*隱藏*|未知的成員存在，但不顯示出來。|  
|*無*|沒有使用未知的成員。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `UnknownMember` 允許值的列舉是 <xref:Microsoft.AnalysisServices.UnknownMemberBehavior>。  
  
## <a name="see-also"></a>另請參閱  
 [UnknownMemberName 元素&#40;ASSL&#41;](name-element-assl.md)   
 [UnknownMemberTranslation 元素&#40;ASSL&#41;](../objects/translation-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  