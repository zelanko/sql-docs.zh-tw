---
title: ReportingWeekToMonthPattern 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ReportingWeekToMonthPattern Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportingWeekToMonthPattern
helpviewer_keywords:
- ReportingWeekToMonthPattern element
ms.assetid: 8d7c694d-d5c5-4faa-af78-155779e84fe9
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fcbbf8a7783d152c66ec4f222ba79b00181b60f5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37324818"
---
# <a name="reportingweektomonthpattern-element-assl"></a>ReportingWeekToMonthPattern 元素 (ASSL)
  定義的報表週至月份模式[TimeBinding](../data-type/binding-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<TimeBinding>  
   ...  
   <ReportingWeekToMonthPattern>...</ReportingWeekToMonthPattern>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*445*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[TimeBinding](../data-type/binding-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*445*|在當季 4 週，在第二個月和第三個月有 5 週的第一個月中的 4 週。|  
|*454*|在當季 5 週，在第二個月和第三個月中的 4 週的第一個月中的 4 週。|  
|*544*|該季的第一個月有 5 週、第二個月有 4 週，而第三個月有 4 週。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `ReportingWeekToMonthPattern` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ReportingWeekToMonthPattern>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
