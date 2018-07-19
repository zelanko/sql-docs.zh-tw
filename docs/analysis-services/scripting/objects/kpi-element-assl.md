---
title: Kpi 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 01a1bb3f725979ce1b398f1c177d4851276e425f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34037059"
---
# <a name="kpi-element-assl"></a>Kpi 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義關鍵效能指標 (KPI) 內[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目或[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。  
  
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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|請參閱下表。|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
|上階或父系|資料類型|  
|------------------------|---------------|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|無|  
|[檢視方塊](../../../analysis-services/scripting/objects/perspective-element-assl.md)|[PerspectiveKpi](../../../analysis-services/scripting/data-type/perspectivekpi-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Kpi](../../../analysis-services/scripting/collections/kpis-element-assl.md)|  
|子元素|請參閱下表。|  
  
|上階或父系|子元素|  
|------------------------|--------------------|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [AssociatedMeasureGroupID](../../../analysis-services/scripting/properties/associatedmeasuregroupid-element-assl.md)， [CurrentTimeMember](../../../analysis-services/scripting/properties/currenttimemember-element-assl.md)，[描述](../../../analysis-services/scripting/properties/description-element-assl.md)， [DisplayFolder](../../../analysis-services/scripting/properties/displayfolder-element-assl.md)，[目標](../../../analysis-services/scripting/properties/goal-element-assl.md)，[識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)，[狀態](../../../analysis-services/scripting/properties/status-element-assl.md)， [StatusGraphic](../../../analysis-services/scripting/properties/statusgraphic-element-assl.md)，[翻譯](../../../analysis-services/scripting/collections/translations-element-assl.md)，[趨勢](../../../analysis-services/scripting/properties/trend-element-assl.md)， [TrendGraphic](../../../analysis-services/scripting/properties/trendgraphic-element-assl.md)，[值](../../../analysis-services/scripting/properties/value-element-assl.md)|  
|[檢視方塊](../../../analysis-services/scripting/objects/perspective-element-assl.md)|無|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應的元素是 <xref:Microsoft.AnalysisServices.Kpi> 和 <xref:Microsoft.AnalysisServices.PerspectiveKpi>。  
  
## <a name="see-also"></a>另請參閱  
 [物件 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
