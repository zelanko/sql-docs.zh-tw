---
title: DefaultMember 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DefaultMember Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DefaultMember
helpviewer_keywords:
- DefaultMember element
ms.assetid: db4eea9f-f7cf-40de-abd0-b62014e7ec2d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c90abe48fc1d3bfa099e39234d22df822a03782
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055291"
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributePermission](../objects/attributepermission-element-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)， [ManyToManyMeasureGroupDimension](../data-type/dimension-data-type-assl.md)， [PerspectiveAttribute](../data-type/perspectiveattribute-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `DefaultMember` 元素會定義父元素的預設成員。 如果`DefaultMember`未指定或設為空字串， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]會選擇要做為預設成員。  
  
 若為 `ManyToManyMeasureGroupDimension` 元素，`DefaultMember` 元素就會包含 MDX 運算式，以便在 `CubeDimensionID` 的 `ManyToManyMeasureGroupDimension` 元素中識別的維度內指定成員。 MDX 運算式是類似[StrToMember](/sql/mdx/strtomember-mdx) MDX 函數與 CONSTRAINED 關鍵字，因為它無法包含 MDX 或使用者定義函數。  
  
 如需預設成員的詳細資訊，請參閱 [定義預設成員](../../multidimensional-models/attribute-properties-define-a-default-member.md)。  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `DefaultMember` 父系的元素是 <xref:Microsoft.AnalysisServices.AttributePermission>、<xref:Microsoft.AnalysisServices.DimensionAttribute> 和 <xref:Microsoft.AnalysisServices.PerspectiveAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
