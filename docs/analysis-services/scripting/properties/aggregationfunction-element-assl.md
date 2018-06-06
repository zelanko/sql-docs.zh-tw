---
title: AggregationFunction 元素 (ASSL) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0e465538b6528e26090f96786f98354b5253b9a7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="aggregationfunction-element-assl"></a>AggregationFunction 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*Sum*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[帳戶](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下列其中一個字串：  
  
|Value|Description|  
|-----------|-----------------|  
|*Sum*|使用彙總的量值**總和**函式。|  
|*Count*|使用彙總的量值**計數**函式。|  
|*Min*|使用彙總的量值**Min**函式。|  
|*Max*|使用彙總的量值**Max**函式。|  
|*DistinctCount*|使用彙總的量值**DistinctCount**函式。|  
|*無*|此量值不會進行彙總。|  
|*AverageOfChildren*|此量值是透過傳回其子系的平均值進行彙總的。|  
|*FirstChild*|此量值是透過傳回第一個子成員進行彙總的。|  
|*LastChild*|此量值是透過傳回最後一個子成員進行彙總的。|  
|*FirstNonEmpty*|此量值是透過傳回第一個非空白成員進行彙總的。|  
|*LastNonEmpty*|此量值是透過傳回最後一個非空白成員進行彙總的。|  
  
 列舉型別對應至允許的值**AggregationFunction**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.AggregationFunction>。  
  
## <a name="see-also"></a>另請參閱  
 [帳戶項目&#40;ASSL&#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
