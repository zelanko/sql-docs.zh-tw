---
title: DegenerateMeasureGroupDimension 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DegenerateMeasureGroupDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DegenerateMeasureGroupDimension
helpviewer_keywords:
- DegenerateMeasureGroupDimension data type
ms.assetid: a64fe908-154d-4fea-b435-afb6ee37a6fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aac39fb97d6f078b6ff5441c6b84da370d90600f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082738"
---
# <a name="degeneratemeasuregroupdimension-data-type-assl"></a>DegenerateMeasureGroupDimension 資料類型 (ASSL)
  定義代表變質維度 (亦即，事實維度) 與量值群組之間關聯性的衍生資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DegenerateMeasureGroupDimension>  
   <!-- DegenerateMeasureGroupDimension does not have any elements that extend RegularMeasureGroupDimension -->  
</DegenerateMeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[RegularMeasureGroupDimension](dimension-data-type-assl.md)|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|None|  
|衍生的元素|None|  
  
## <a name="remarks"></a>備註  
 如需有關事實維度的詳細資訊，請參閱 <<c0> [ 維度關聯性](../../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.DegenerateMeasureGroupDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
