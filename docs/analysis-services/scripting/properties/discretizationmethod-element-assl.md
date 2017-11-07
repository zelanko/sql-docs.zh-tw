---
title: "DiscretizationMethod 元素 (ASSL) |Microsoft 文件"
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
- DiscretizationMethod Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DiscretizationMethod
helpviewer_keywords:
- DiscretizationMethod element
ms.assetid: 4cfe015f-ad6c-47e1-8aff-c9c7677867b1
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e2bbf548ba16ccc81d1536c5c64a22e9c69d96d1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="discretizationmethod-element-assl"></a>DiscretizationMethod 元素 (ASSL)
  定義用於進行離散化的方法。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationMethod>...</DiscretizationMethod>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*無*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)， [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值**DiscretizationMethod**元素會決定如何值**DimensionAttribute**或**ScalarMiningStructureColumn**是離散化或組織成一組特定的群組。 如需有關離散化方法的詳細資訊，請參閱[離散化方法 &#40; 資料採礦 &#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md)。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*自動*|相當於採礦結構資料行的 AUTOMATIC 離散化方法。|  
|*EqualAreas*|相當於採礦結構資料行的 EQUAL_AREAS 離散化方法。|  
|*叢集*|相當於採礦結構資料行的 CLUSTERS 離散化方法。|  
|*臨界值*|相當於採礦結構資料行的 THRESHOLDS 離散化方法。|  
|*EqualRanges*|相當於採礦結構資料行的 EQUAL_RANGES 離散化方法。|  
  
 列舉型別對應至允許的值**DiscretizationMethod**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.DiscretizationMethod>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

