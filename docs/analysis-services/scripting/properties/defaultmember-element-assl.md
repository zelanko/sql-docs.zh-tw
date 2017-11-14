---
title: "DefaultMember 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DefaultMember Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DefaultMember
helpviewer_keywords:
- DefaultMember element
ms.assetid: db4eea9f-f7cf-40de-abd0-b62014e7ec2d
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 411fbf97001ee719e144edfdd6de685e984da021
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="defaultmember-element-assl"></a>DefaultMember 元素 (ASSL)
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
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

