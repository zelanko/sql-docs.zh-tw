---
title: TimeBinding 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- TimeBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TimeBinding
helpviewer_keywords:
- TimeBinding data type
ms.assetid: f3c06978-c181-4a73-9b57-8fc30358faab
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7102bbea8eb516b93eb2e539a74b2110f22c6694
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37183335"
---
# <a name="timebinding-data-type-assl"></a>TimeBinding 資料類型 (ASSL)
  定義代表時間週期之繫結的衍生資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<TimeBinding>  
   <!-- The following elements extend Binding -->  
      <CalendarStartDate>...</CalendarStartDate>  
      <CalendarEndDate>...</CalendarEndDate>  
      <FirstDayOfWeek>...</FirstDayOfWeek>  
   <CalendarLanguage>...</CalendarLanguage>  
   <FiscalFirstMonth>...</FiscalFirstMonth>  
   <FiscalFirstDayOfMonth>...</FiscalFirstDayOfMonth>  
   <FiscalYearName>...</FiscalYearName>  
   <ReportingFirstMonth>...</ReportingFirstMonth>  
   <ReportingFirstWeekOfMonth>...</ReportingFirstWeekOfMonth>  
   <ReportingWeekToMonthPattern>...</ReportingWeekToMonthPattern>  
   <ManufacturingFirstMonth>...</ManufacturingFirstMonth>  
   <ManufacturingFirstWeekOfMonth>...</ManufacturingFirstWeekOfMonth>  
   <ManufacturingExtraMonthQuarter>...</ManufacturingExtraMonthQuarter>  
</TimeBinding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[繫結](binding-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[CalendarEndDate](../properties/calendarenddate-element-assl.md)， [CalendarLanguage](../properties/language-element-assl.md)， [CalendarStartDate](../properties/calendarstartdate-element-assl.md)， [FirstDayOfWeek](../properties/firstdayofweek-element-assl.md)， [FiscalFirstDayOfMonth](../properties/fiscalfirstdayofmonth-element-assl.md)[FiscalFirstMonth](../properties/fiscalfirstmonth-element-assl.md)， [FiscalYearName](../properties/name-element-assl.md)， [ManufacturingExtraMonthQuarter](../properties/manufacturingextramonthquarter-element-assl.md)， [ManufacturingFirstMonth](../properties/manufacturingfirstmonth-element-assl.md)，[ManufacturingFirstWeekOfMonth](../properties/manufacturingfirstweekofmonth-element-assl.md)， [ReportingFirstMonth](../properties/reportingfirstmonth-element-assl.md)， [ReportingFirstWeekOfMonth](../properties/reportingfirstweekofmonth-element-assl.md)， [ReportingWeekToMonthPattern](../properties/reportingweektomonthpattern-element-assl.md)|  
|衍生的元素|請參閱[繫結](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 如需詳細資訊`Binding`型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表`Binding`型別和繼承階層`Binding`類型，請參閱[繫結資料類型 &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 如需 ASSL 中資料繫結的概觀，請參閱 <<c0> [ 資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。</c0>  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.TimeBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
