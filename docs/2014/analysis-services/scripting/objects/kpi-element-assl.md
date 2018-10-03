---
title: Kpi 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Kpi Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Kpi
helpviewer_keywords:
- Kpi element
ms.assetid: 1979a58f-97a8-4c1a-aa65-dcfb6d2404cf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 63b7947785976d41cda112b1c14b3829e3f98e3a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124148"
---
# <a name="kpi-element-assl"></a>Kpi 元素 (ASSL)
  定義關鍵效能指標 (KPI) 內[Cube](cube-element-assl.md)項目或有[觀點來看](perspective-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Kpis>  
   <Kpi> <!-- ancestor: Cube -->  
            <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <Translations>...</Translations>  
      <DisplayFolder>...</DisplayFolder>  
      <AssociatedMeasureGroupID>...</AssociatedMeasureGroupID>  
      <Value>...</Value>  
            <Goal>...</Goal>  
      <Status>...</Status>  
      <Trend>...</Trend>  
      <TrendGraphic>...</TrendGraphic>  
      <StatusGraphic>...</StatusGraphic>  
      <CurrentTimeMember>...</CurrentTimeMember>  
      <Annotations>...</Annotations>  
   </Kpi>  
   <!-- or -->  
   <Kpi xsi:type="PerspectiveKpi">...</Kpi> <!-- ancestor: Perspective -->  
   </Kpi>  
</Kpis>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
|上階或父系|資料類型|  
|------------------------|---------------|  
|[Cube](cube-element-assl.md)|None|  
|[檢視方塊](../data-type/perspectivekpi-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Kpi](../collections/kpis-element-assl.md)|  
  
## <a name="child-elements"></a>子元素  
  
|上階或父系|子元素|  
|------------------------|--------------------|  
|[Cube](../collections/annotations-element-assl.md)， [AssociatedMeasureGroupID](../properties/id-element-assl.md)， [CurrentTimeMember](member-element-assl.md)，[描述](../properties/description-element-assl.md)， [DisplayFolder](../properties/displayfolder-element-assl.md)， [目標](../properties/goal-element-assl.md)，[識別碼](../properties/id-element-assl.md)，[名稱](../properties/name-element-assl.md)，[狀態](../properties/status-element-assl.md)， [StatusGraphic](../properties/statusgraphic-element-assl.md)，[翻譯](../collections/translations-element-assl.md)，[趨勢](../properties/trend-element-assl.md)， [TrendGraphic](../properties/trendgraphic-element-assl.md)，[值](../properties/value-element-assl.md)|  
|[檢視方塊](perspective-element-assl.md)|None|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應的元素是 <xref:Microsoft.AnalysisServices.Kpi> 和 <xref:Microsoft.AnalysisServices.PerspectiveKpi>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
