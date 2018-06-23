---
title: AggregationID 元素 (ASSL) |Microsoft 文件
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
- AggregationID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- AggregationID element
ms.assetid: 6056da1d-b6b4-4074-84db-45be719df49a
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5cc757076c638075466cd0d49ad4340c983a8294
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136499"
---
# <a name="aggregationid-element-assl"></a>AggregationID 元素 (ASSL)
  識別彙總定義[AggregationDesign](../objects/aggregationdesign-element-assl.md)用來建立彙總執行個體的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationInstance>  
   ...  
   <AggregationID>...</AggregationID>  
   ...  
</AggregationInstance>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationInstance](../objects/aggregationinstance-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如果這個元素遺漏或設定為空白字串，`AggregationInstance` 就代表使用者定義彙總。  
  
 對應目的父代的項目`AggregationID`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.AggregationInstance>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  