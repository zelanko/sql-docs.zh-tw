---
title: DefaultMember 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d050c0cb2209c855da35a7f1afd2fe028575edf7
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="defaultmember-element-assl"></a>DefaultMember 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含識別父元素之預設成員的多維度運算式 (MDX) 運算式。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AttributePermission> <!-- or DimensionAttribute, ManyToManyMeasureGroupDimension, PerspectiveAttribute -->  
      ...  
   <DefaultMember>...</DefaultMember>  
      ...  
</AttributePermission>  
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
|父元素|[AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)， [ManyToManyMeasureGroupDimension](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md)， [PerspectiveAttribute](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **DefaultMember**項目會定義父元素的預設成員。 如果**DefaultMember**未指定或設為空字串， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]就會選擇要做為預設成員。  
  
 如**ManyToManyMeasureGroupDimension**項目， **DefaultMember**項目包含指定成員在維度中識別的 MDX 運算式**CubeDimensionID**元素**ManyToManyMeasureGroupDimension**。 MDX 運算式是類似於[StrToMember](../../../mdx/strtomember-mdx.md) MDX 函數與含有 CONSTRAINED 關鍵字，因為它無法包含 MDX 或使用者定義函數。  
  
 如需預設成員的詳細資訊，請參閱 [定義預設成員](../../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)。  
  
 對應至父系的項目**DefaultMember**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.AttributePermission>， <xref:Microsoft.AnalysisServices.DimensionAttribute>，和<xref:Microsoft.AnalysisServices.PerspectiveAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
