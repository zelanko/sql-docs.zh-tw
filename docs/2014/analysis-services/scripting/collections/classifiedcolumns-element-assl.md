---
title: ClassifiedColumns 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ClassifiedColumns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ClassifiedColumns
helpviewer_keywords:
- ClassifiedColumns element
ms.assetid: f16b4f51-c38d-4601-98b8-1497dbf12d02
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e2624c2d944af873fe6a34cbd9ca3684050bf92
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209828"
---
# <a name="classifiedcolumns-element-assl"></a>ClassifiedColumns 元素 (ASSL)
  包含相關的資料行所分類的集合[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningStructureColumn xsi:type="ScalarMiningStructureColumn">  
   ...  
   <ClassifiedColumns>  
      <ClassifiedColumnID>...</ClassifiedColumnID>  
   </ClassifiedColumns>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)型別的[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|[ClassifiedColumnID](../properties/id-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`ClassifiedColumns`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [MiningStructureColumn 資料類型&#40;ASSL&#41;](../data-type/miningstructurecolumn-data-type-assl.md)   
 [MiningStructure 元素&#40;ASSL&#41;](../objects/miningstructure-element-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
