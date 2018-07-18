---
title: DiscretizationMethod 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 81064689788574061f103b973a5435beb3e83893
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036409"
---
# <a name="discretizationmethod-element-assl"></a>DiscretizationMethod 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 值**DiscretizationMethod**元素會決定如何值**DimensionAttribute**或**ScalarMiningStructureColumn**是離散化或組織成一組特定的群組。 如需有關離散化方法的詳細資訊，請參閱[離散化方法&#40;資料採礦&#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md)。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|Value|描述|  
|-----------|-----------------|  
|*Automatic*|相當於採礦結構資料行的 AUTOMATIC 離散化方法。|  
|*EqualAreas*|相當於採礦結構資料行的 EQUAL_AREAS 離散化方法。|  
|*群集*|相當於採礦結構資料行的 CLUSTERS 離散化方法。|  
|*臨界值*|相當於採礦結構資料行的 THRESHOLDS 離散化方法。|  
|*EqualRanges*|相當於採礦結構資料行的 EQUAL_RANGES 離散化方法。|  
  
 列舉型別對應至允許的值**DiscretizationMethod**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.DiscretizationMethod>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
