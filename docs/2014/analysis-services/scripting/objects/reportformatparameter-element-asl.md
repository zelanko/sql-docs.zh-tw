---
title: ReportFormatParameter 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ReportFormatParameter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportFormatParameter
helpviewer_keywords:
- ReportFormatParameter element
ms.assetid: 064a8683-c44b-4261-be4d-32226d3d3119
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7f3dd567a88a76837e13d051988620eb1886ef40
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48188018"
---
# <a name="reportformatparameter-element-assl"></a>ReportFormatParameter 元素 (ASSL)
  包含名稱和指定之參數的值如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]報表的格式在執行階段。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ReportFormatParameters>  
   <ReportFormatParameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </ReportFormatParameter>  
</ReportFormatParameters>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ReportFormatParameters](../collections/reportformatparameters-element-assl.md)|  
|子元素|[名稱](../properties/name-element-assl.md)，[值](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`ReportFormatParameter`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.ReportAction>。  
  
## <a name="see-also"></a>另請參閱  
 [ReportAction 資料類型&#40;ASSL&#41;](../data-type/action-data-type-assl.md)   
 [動作項目&#40;ASSL&#41;](action-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
