---
title: 值元素 (ASSL) |Microsoft 文件
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
- Value Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Value
helpviewer_keywords:
- Value element
ms.assetid: a2fad411-73fd-42df-b4e1-df2cb8454182
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f350c559e78613df5e0a357b8f87dca073e1d248
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037324"
---
# <a name="value-element-assl"></a>Value 元素 (ASSL)
  包含父元素的值。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AlgorithmParameter> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Value>...</Value>  
   ...  
</AlgorithmParameter>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
|上階或父系|資料類型|  
|------------------------|---------------|  
|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)|任何 simpleType|  
|[ServerProperty](../objects/serverproperty-element-assl.md)|任何 simpleType|  
|All others|String|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)，[註解](../objects/annotation-element-assl.md)， [Kpi](../objects/kpi-element-assl.md)， [ReportFormatParameter](../objects/reportformatparameter-element-asl.md)， [ReportParameter](../objects/reportparameter-element-assl.md)， [ServerProperty](../objects/serverproperty-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `Value` 元素包含與父物件相關聯的值。 `Value` 元素的預期值會因父元素而不同，如下表所述。  
  
|父元素|預期的值|  
|--------------------|--------------------|  
|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)|演算法參數的值。|  
|[註解](../objects/annotation-element-assl.md)|註解的值。|  
|[Kpi](../objects/kpi-element-assl.md)|用來計算關鍵效能指標 (KPI) 之值的多維度運算式 (MDX) 運算式。|  
|[ReportFormatParameter](../objects/reportformatparameter-element-asl.md)|報表格式參數的值。|  
|[ReportParameter](../objects/reportparameter-element-assl.md)|用來計算報表參數值的 MDX 運算式。|  
|[ServerProperty](../objects/serverproperty-element-assl.md)|目前執行中執行個體之伺服器屬性的值。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Value` 父系的元素是 <xref:Microsoft.AnalysisServices.AlgorithmParameter>、<xref:Microsoft.AnalysisServices.Annotation>、<xref:Microsoft.AnalysisServices.Kpi>、<xref:Microsoft.AnalysisServices.ReportParameter> 和 <xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  