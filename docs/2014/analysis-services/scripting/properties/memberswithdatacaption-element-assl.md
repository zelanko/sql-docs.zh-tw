---
title: MembersWithDataCaption 元素 (ASSL) |Microsoft Docs
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
- MembersWithDataCaption Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MembersWithDataCaption
helpviewer_keywords:
- MembersWithDataCaption element
ms.assetid: a5d59efd-5d67-485b-a360-67d54a1fe394
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd8884d67717267e44751841203ce2f73d07ecfb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202298"
---
# <a name="memberswithdatacaption-element-assl"></a>MembersWithDataCaption 元素 (ASSL)
  提供範本字串，該字串會用來建立系統所產生之資料成員的標題。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AttributeTranslation> <!-- or DimensionAttribute -->  
   ...  
   <MembersWithDataCaption>...</MembersWithDataCaption>  
   ...  
</AttributeTranslation>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributeTranslation](../data-type/translation-data-type-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值`MembersWithDataCaption`項目僅供父屬性 (亦即的值[使用量](usage-element-dimensionattribute-assl.md)項目`DimensionAttribute`父項目設定為*父*) 來判斷父屬性中的資料成員的標題。 如需資料成員的詳細資訊，請參閱 [父子式階層中的屬性](../../multidimensional-models/parent-child-dimension-attributes.md)。  
  
 對應至父系的元素`MembersWithDataCaption`在 「 分析管理物件 (AMO) 物件模型所<xref:Microsoft.AnalysisServices.AttributeTranslation>和<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [MembersWithData 元素&#40;ASSL&#41;](../objects/data-element-assl.md)   
 [AttributeTranslation 資料類型&#40;ASSL&#41;](../data-type/translation-data-type-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
