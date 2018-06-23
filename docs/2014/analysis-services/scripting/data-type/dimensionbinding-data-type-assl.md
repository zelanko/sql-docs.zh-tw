---
title: DimensionBinding 資料類型 (ASSL) |Microsoft 文件
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
- DimensionBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DimensionBinding
helpviewer_keywords:
- DimensionBinding data type
ms.assetid: 6163d86b-0f6c-4237-b07b-47bc7e2962c4
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ac0dfce6e5c21ee901e065561b161c2d66cdd8c1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032641"
---
# <a name="dimensionbinding-data-type-assl"></a>DimensionBinding 資料類型 (ASSL)
  定義代表資料來源之間的繫結的衍生的資料類型和[維度](../objects/dimension-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionBinding>  
   <!-- The following elements extend Binding -->  
      <DataSourceID>...</DataSourceID>  
   <DimensionID>...</DimensionID>  
      <Persistence>...</Persistence>  
      <RefreshPolicy>...</RefreshPolicy>  
   <RefreshInterval>...</RefreshInterval>  
</DimensionBinding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[繫結](binding-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[DataSourceID](../properties/id-element-assl.md)， [DimensionID](../properties/dimensionid-element-assl.md)，[持續性](../properties/persistence-element-assl.md)， [RefreshInterval](../properties/refreshinterval-element-assl.md)， [RefreshPolicy](../properties/refreshpolicy-element-assl.md)|  
|衍生的元素|請參閱[繫結](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 如需有關`Binding`型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表`Binding`型別和繼承階層架構的`Binding`類型，請參閱[繫結資料型別&#40;ASSL&#41; ](binding-data-type-assl.md)項目。  
  
 如需 ASSL 中資料繫結的概觀，請參閱[資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.DimensionBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  