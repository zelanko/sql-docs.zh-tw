---
title: AggregateFunction 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- AggregateFunction Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregateFunction
helpviewer_keywords:
- AggregateFunction element
ms.assetid: 880b6bd0-d62a-4221-831c-39f748ee84f2
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2eb41e7a281d3ee343b8b96c339fb8baa1a5283e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="aggregatefunction-element-assl"></a>AggregateFunction 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義所使用的彙總函式的型別[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)項目。  
  
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
|父元素|[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*Sum*|使用彙總的量值**總和**函式。|  
|*計數*|使用彙總的量值**計數**函式。|  
|*Min*|使用彙總的量值**Min**函式。|  
|*Max*|使用彙總的量值**Max**函式。|  
|*DistinctCount*|使用彙總的量值**DistinctCount**函式。|  
|*無*|此量值不會進行彙總。|  
|*ByAccount*|此量值是由帳戶進行彙總的。|  
|*AverageOfChildren*|此量值是透過傳回其子系的平均值進行彙總的。|  
|*FirstChild*|此量值是透過傳回第一個子成員進行彙總的。|  
|*LastChild*|此量值是透過傳回最後一個子成員進行彙總的。|  
|*FirstNonEmpty*|此量值是透過傳回第一個非空白成員進行彙總的。|  
|*LastNonEmpty*|此量值是透過傳回最後一個非空白成員進行彙總的。|  
  
 列舉型別對應至允許的值**AggregateFunction**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.AggregationFunction>。  
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
