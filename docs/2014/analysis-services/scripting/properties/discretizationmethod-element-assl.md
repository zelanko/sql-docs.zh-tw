---
title: DiscretizationMethod 元素 (ASSL) |Microsoft 文件
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
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c22387c74c49446c74b06125da02bda11acd0b7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031105"
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
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `DiscretizationMethod` 元素的值會決定 `DimensionAttribute` 或 `ScalarMiningStructureColumn` 的值如何離散化或組織成特定群組集合。 如需有關離散化方法的詳細資訊，請參閱[離散化方法&#40;資料採礦&#41;](../../data-mining/discretization-methods-data-mining.md)。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*自動*|相當於採礦結構資料行的 AUTOMATIC 離散化方法。|  
|*EqualAreas*|相當於採礦結構資料行的 EQUAL_AREAS 離散化方法。|  
|*叢集*|相當於採礦結構資料行的 CLUSTERS 離散化方法。|  
|*臨界值*|相當於採礦結構資料行的 THRESHOLDS 離散化方法。|  
|*EqualRanges*|相當於採礦結構資料行的 EQUAL_RANGES 離散化方法。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `DiscretizationMethod` 允許值的列舉是 <xref:Microsoft.AnalysisServices.DiscretizationMethod>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  