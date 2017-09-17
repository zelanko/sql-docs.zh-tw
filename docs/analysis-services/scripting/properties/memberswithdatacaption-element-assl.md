---
title: "MembersWithDataCaption 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MembersWithDataCaption Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MembersWithDataCaption
helpviewer_keywords:
- MembersWithDataCaption element
ms.assetid: a5d59efd-5d67-485b-a360-67d54a1fe394
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f254c1fb3c747a64e3e8e5df50bf30d532678d09
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值**MembersWithDataCaption**項目僅供父屬性 (換言之，值[使用量](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md)元素**DimensionAttribute**父元素會設定為*父*) 來判斷父屬性中的資料成員的標題。 如需資料成員的詳細資訊，請參閱 [父子式階層中的屬性](../../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)。  
  
 對應至父系的項目**MembersWithDataCaption**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.AttributeTranslation>和<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [MembersWithData 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md)   
 [AttributeTranslation 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
