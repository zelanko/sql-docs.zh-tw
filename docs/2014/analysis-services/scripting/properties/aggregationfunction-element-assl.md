---
title: AggregationFunction 元素 (ASSL) |Microsoft Docs
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
- AggregationFunction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationFunction
helpviewer_keywords:
- AggregationFunction element
ms.assetid: 40cfc7f9-1089-45f9-be90-a29770ed9682
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90908001138f59d4270811376ac44025148889cf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37308438"
---
# <a name="aggregationfunction-element-assl"></a>AggregationFunction 元素 (ASSL)
  包含要用於帳戶類型的彙總函式。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Account>  
   ...  
   <AggregationFunction>...</AggregationFunction>  
   ...  
</Account>  
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
|父元素|[帳戶](../objects/account-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下列其中一個字串：  
  
|值|描述|  
|-----------|-----------------|  
|*Sum*|此量值是使用 `Sum` 函數進行彙總的。|  
|*計數*|此量值是使用 `Count` 函數進行彙總的。|  
|*Min*|此量值是使用 `Min` 函數進行彙總的。|  
|*Max*|此量值是使用 `Max` 函數進行彙總的。|  
|*DistinctCount*|此量值是使用 `DistinctCount` 函數進行彙總的。|  
|*無*|此量值不會進行彙總。|  
|*AverageOfChildren*|此量值是透過傳回其子系的平均值進行彙總的。|  
|*FirstChild*|此量值是透過傳回第一個子成員進行彙總的。|  
|*LastChild*|此量值是透過傳回最後一個子成員進行彙總的。|  
|*FirstNonEmpty*|此量值是透過傳回第一個非空白成員進行彙總的。|  
|*LastNonEmpty*|此量值是透過傳回最後一個非空白成員進行彙總的。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `AggregationFunction` 允許值的列舉是 <xref:Microsoft.AnalysisServices.AggregationFunction>。  
  
## <a name="see-also"></a>另請參閱  
 [帳戶項目&#40;ASSL&#41;](../collections/accounts-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
