---
title: AggregationStorage 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationStorage Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationStorage
helpviewer_keywords:
- AggregationStorage element
ms.assetid: dd082388-534d-4847-9232-8f80fc9fe96e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e3ec001116b63816d0b1e2831a266ec3029a38a9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187068"
---
# <a name="aggregationstorage-element-assl"></a>AggregationStorage 元素 (ASSL)
  識別彙總的儲存方法。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <AggregationStorage>...</AggregationStorage>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*規則*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下列其中一個字串：  
  
|值|描述|  
|-----------|-----------------|  
|*規則*|以預設方式儲存彙總資料。|  
|*MolapOnly*|單獨使用多維度 OLAP (MOLAP) 儲存來儲存彙總資料。|  
  
 *MolapOnly*選項，僅適用於[分割區](../objects/partition-element-assl.md)項目。  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `AggregationStorage` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ProactiveCachingAggregationStorage>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
