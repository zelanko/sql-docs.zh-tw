---
title: AggregationType 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- AggregationType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- AggregationType element
ms.assetid: c1393bc6-d715-4397-8bc5-82abdb275330
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7c95f9566f483ec7a047ceedd074237f9ff5f7e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37183215"
---
# <a name="aggregationtype-element-assl"></a>AggregationType 元素 (ASSL)
  定義所儲存的彙總的型別[分割區](../objects/partition-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationInstance>  
   ...  
   <AggregationType>...</AggregationType>  
   ...  
</AggregationInstance>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationInstance](../objects/aggregationinstance-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*IndexedView*|此彙總會儲存在索引檢視表中。|  
|*[資料表]*|此彙總會儲存在資料表中。|  
|*UserDefined*|此彙總是使用者定義的。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `AggregationType` 允許值的列舉是 <xref:Microsoft.AnalysisServices.AggregationInstance>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
