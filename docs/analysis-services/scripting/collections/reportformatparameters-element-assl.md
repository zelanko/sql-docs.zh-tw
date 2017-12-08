---
title: "ReportFormatParameters 元素 (ASSL) |Microsoft 文件"
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
apiname: ReportFormatParameters Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ReportFormatParameters
helpviewer_keywords: ReportFormatParameters element
ms.assetid: f2e677bf-7b6b-4ce4-b0ec-75a4999306c9
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7ea5c18474cbce5e243b1a5aa569b0afee85aacc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="reportformatparameters-element-assl"></a>ReportFormatParameters 元素 (ASSL)
  包含集合[ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)元素[ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action xsi:type="ReportAction">  
   ...  
   <ReportFormatParameters>  
      <ReportFormatParameter>...</ReportFormatParameter>  
   </ReportFormatParameters>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../../../analysis-services/scripting/objects/action-element-assl.md)型別的[ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)|  
|子元素|[ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**ReportFormatParameters**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ReportAction>。  
  
## <a name="see-also"></a>請參閱＜  
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
