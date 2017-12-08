---
title: "AggregationFunction 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AggregationFunction Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AggregationFunction
helpviewer_keywords: AggregationFunction element
ms.assetid: 40cfc7f9-1089-45f9-be90-a29770ed9682
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 68f13efcbd341ce11f7529f9396753649099e237
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
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
  
|值|Description|  
|-----------|-----------------|  
|*Sum*|使用彙總的量值**總和**函式。|  
|*計數*|使用彙總的量值**計數**函式。|  
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
  
## <a name="see-also"></a>請參閱＜  
 [Accounts 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
