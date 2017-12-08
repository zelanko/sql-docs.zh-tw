---
title: "ReportingFirstWeekOfMonth 元素 (ASSL) |Microsoft 文件"
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
apiname: ReportingFirstWeekOfMonth Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ReportingFirstWeekOfMonth
helpviewer_keywords: ReportingFirstWeekOfMonth element
ms.assetid: 29818404-ad45-403f-8fd9-3e3246d301ad
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6c771c7747dba88fd6cbf6e6a70e52a8d74b6280
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="reportingfirstweekofmonth-element-assl"></a>ReportingFirstWeekOfMonth 元素 (ASSL)
  定義之報表月份的第一週[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<TimeBinding>  
   ...  
   <ReportingFirstWeekOfMonth>...</ReportingFirstWeekOfMonth>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|整數 (1 至 4)|  
|預設值|**1**|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**ReportingFirstWeekOfMonth**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.TimeBinding>。  
  
## <a name="see-also"></a>請參閱＜  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
