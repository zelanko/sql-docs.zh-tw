---
title: AggregationDesignID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationDesignID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationDesignID
helpviewer_keywords:
- AggregationDesignID element
ms.assetid: e7f1f7ae-3169-4c0c-aadb-f7465155d652
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 61ca8f81002e28ca60a301ca49c307d9eeb6ef45
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185678"
---
# <a name="aggregationdesignid-element-assl"></a>AggregationDesignID 元素 (ASSL)
  識別[AggregationDesign](../objects/aggregationdesign-element-assl.md)相關聯的項目[分割區](../objects/partition-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Partition>  
      ...  
   <AggregationDesignID>...</AggregationDesignID>  
   ...  
</Partition>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料分割](../objects/partition-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`AggregationDesignID`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Partition>。 另請參閱<xref:Microsoft.AnalysisServices.AggregationDesign>。  
  
## <a name="see-also"></a>另請參閱  
 [AggregationDesign 元素&#40;ASSL&#41;](../objects/aggregationdesign-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
