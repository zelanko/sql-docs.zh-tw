---
title: MeasureGroupBinding 資料類型 (非正規-out-of-line) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroupBinding Data Type (out-of-line)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroupBinding
helpviewer_keywords:
- MeasureGroupBinding data type
ms.assetid: e6c65597-89ac-457e-a0e5-01d85449a1b7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a31e1d49636fc74f28639d898b18f26838ff389
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180138"
---
# <a name="measuregroupbinding-data-type-out-of-line-assl"></a>MeasureGroupBinding 資料類型 (out-of-line) (ASSL)
  定義代表量值群組之繫結的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MeasureGroupBinding>  
   <ID>...</ID>  
   <Source>...</Source>  
   <EstimatedRows>...</EstimatedRows>  
   <Dimensions>...</Dimensions>  
   <Measures>...</Measures>  
      <Partitions>...</Partitions>  
</MeasureGroupBinding>  
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
|子元素|[維度](../collections/dimensions-element-assl.md)， [EstimatedRows](../properties/estimatedrows-element-assl.md)，[識別碼](../properties/id-element-assl.md)，[量值](../collections/measures-element-assl.md)，[分割](../collections/partitions-element-assl.md)，[來源](../properties/source-element-binding-assl.md)|  
|衍生的元素|請參閱[繫結](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 如需詳細資訊，請參閱一節，共線的繫結，在[資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
