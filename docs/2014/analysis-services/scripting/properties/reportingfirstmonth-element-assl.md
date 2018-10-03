---
title: ReportingFirstMonth 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ReportingFirstMonth Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportingFirstMonth
helpviewer_keywords:
- ReportingFirstMonth element
ms.assetid: cdce83ab-ac22-4f4a-b8f2-1739883be8dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 707efba16ae2583a87f48cc8c9b5627dd8e5e0ff
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101778"
---
# <a name="reportingfirstmonth-element-assl"></a>ReportingFirstMonth 元素 (ASSL)
  定義的第一個報表月份[TimeBinding](../data-type/binding-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<TimeBinding>  
   ...  
   <ReportingFirstMonth>...</ReportingFirstMonth>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|整數 (1 至 12，其中 1 = 一月而 12 = 十二月)|  
|預設值|`1`|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[TimeBinding](../data-type/binding-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`ReportingFirstMonth`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.TimeBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
