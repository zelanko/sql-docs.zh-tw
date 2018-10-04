---
title: DiscretizationMethod 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DiscretizationMethod Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DiscretizationMethod
helpviewer_keywords:
- DiscretizationMethod element
ms.assetid: 4cfe015f-ad6c-47e1-8aff-c9c7677867b1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 75308b5270eb762236be22fc0838a480474898dc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200470"
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*無*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)， [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `DiscretizationMethod` 元素的值會決定 `DimensionAttribute` 或 `ScalarMiningStructureColumn` 的值如何離散化或組織成特定群組集合。 如需有關離散化方法的詳細資訊，請參閱[離散化方法&#40;資料採礦&#41;](../../data-mining/discretization-methods-data-mining.md)。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*自動*|相當於採礦結構資料行的 AUTOMATIC 離散化方法。|  
|*EqualAreas*|相當於採礦結構資料行的 EQUAL_AREAS 離散化方法。|  
|*叢集*|相當於採礦結構資料行的 CLUSTERS 離散化方法。|  
|*臨界值*|相當於採礦結構資料行的 THRESHOLDS 離散化方法。|  
|*EqualRanges*|相當於採礦結構資料行的 EQUAL_RANGES 離散化方法。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `DiscretizationMethod` 允許值的列舉是 <xref:Microsoft.AnalysisServices.DiscretizationMethod>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
