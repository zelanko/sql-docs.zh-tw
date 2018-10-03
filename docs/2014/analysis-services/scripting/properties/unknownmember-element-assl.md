---
title: UnknownMember 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dab3908376520a67e1192a0a4a2d52c76b6a88df
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48052328"
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
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*可見*|未知的成員存在並顯示出來。|  
|*隱藏*|未知的成員存在，但不顯示出來。|  
|*無*|沒有使用未知的成員。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `UnknownMember` 允許值的列舉是 <xref:Microsoft.AnalysisServices.UnknownMemberBehavior>。  
  
## <a name="see-also"></a>另請參閱  
 [UnknownMemberName 元素&#40;ASSL&#41;](name-element-assl.md)   
 [UnknownMemberTranslation 元素&#40;ASSL&#41;](../objects/translation-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
