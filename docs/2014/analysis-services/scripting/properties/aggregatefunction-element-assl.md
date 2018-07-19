---
title: AggregateFunction 元素 (ASSL) |Microsoft Docs
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
- AggregateFunction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregateFunction
helpviewer_keywords:
- AggregateFunction element
ms.assetid: 880b6bd0-d62a-4221-831c-39f748ee84f2
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bc2eccf4ca6e41ffba52424c4f45edb71c9c1c46
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37261204"
---
# <a name="aggregatefunction-element-assl"></a>AggregateFunction 元素 (ASSL)
  定義所使用的彙總函式的型別[量值](../objects/measure-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Measure>  
   ...  
   <AggregateFunction>...</AggregateFunction>  
   ...  
</Measure>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*Sum*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[量值](../objects/measure-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*Sum*|此量值是使用 `Sum` 函數進行彙總的。|  
|*計數*|此量值是使用 `Count` 函數進行彙總的。|  
|*Min*|此量值是使用 `Min` 函數進行彙總的。|  
|*Max*|此量值是使用 `Max` 函數進行彙總的。|  
|*DistinctCount*|此量值是使用 `DistinctCount` 函數進行彙總的。|  
|*無*|此量值不會進行彙總。|  
|*ByAccount*|此量值是由帳戶進行彙總的。|  
|*AverageOfChildren*|此量值是透過傳回其子系的平均值進行彙總的。|  
|*FirstChild*|此量值是透過傳回第一個子成員進行彙總的。|  
|*LastChild*|此量值是透過傳回最後一個子成員進行彙總的。|  
|*FirstNonEmpty*|此量值是透過傳回第一個非空白成員進行彙總的。|  
|*LastNonEmpty*|此量值是透過傳回最後一個非空白成員進行彙總的。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `AggregateFunction` 允許值的列舉是 <xref:Microsoft.AnalysisServices.AggregationFunction>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
