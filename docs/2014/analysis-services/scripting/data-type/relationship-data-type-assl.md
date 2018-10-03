---
title: Relationship 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 73d7c48d-d8e0-4119-849d-b5f912d449e4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 601cd7311cd3d78f1714ab881130d96231d60241
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165588"
---
# <a name="relationship-data-type-assl"></a>Relationship 資料類型 (ASSL)
  定義代表維度中某個關聯性的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Relationship>  
   <ID>...</ID>  
   <Visible>...</Visible>  
   <FromRelationshipEnd>...</FromRelationshipEnd>  
   <ToRelationshipEnd>...</ToRelationshipEnd>  
</Relationship>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|None|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[ID](../properties/id-element-assl.md)，[可見](../properties/visible-element-assl.md)， [FromRelationshipEnd](relationshipend-data-type-assl.md)， [ToRelationshipEnd](relationshipend-data-type-assl.md)|  
|衍生的元素||  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.Relationship>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
