---
title: Distribution 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Distribution Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Distribution
helpviewer_keywords:
- Distribution element
ms.assetid: a1309b90-8ad8-431b-a918-67f0cdd4fd20
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f71addc3c9c793a19e88e52bb0b82519b5f33f1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166448"
---
# <a name="distribution-element-assl"></a>Distribution 元素 (ASSL)
  包含描述純量值如何提供者特定值的資料行內部散發[MiningStructure](../objects/miningstructure-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <Distribution>...</Distribution>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 可用的值`Distribution`項目，例如*正常*或是*統一，* 專屬於每個採礦演算法提供者。 如需有關有效 `Distribution` 值的詳細資訊，請參閱採礦演算法提供者文件集。  
  
 對應的父代的項目`Distribution`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
