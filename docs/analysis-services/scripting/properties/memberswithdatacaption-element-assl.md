---
title: MembersWithDataCaption 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cc13b853943806854dd4dbc453922f6a4f26dcf7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34035389"
---
# <a name="memberswithdatacaption-element-assl"></a>MembersWithDataCaption 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [MembersWithData 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md)   
 [AttributeTranslation 資料類型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
