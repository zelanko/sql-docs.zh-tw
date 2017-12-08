---
title: "Perspective 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
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
apiname: Perspective Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Perspective
helpviewer_keywords: Perspective element
ms.assetid: 0442334c-8b00-4451-ad81-02e58c735e8f
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 28368ffe071ae5139c4ea5245a0d9bea9222b7dc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="perspective-element-assl"></a>Perspective 元素 (ASSL)
  定義檢視方塊的詳細資料[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Perspectives>  
   <<Perspective>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Translations>...</Translations>  
      <DefaultMeasure>...</DefaultMeasure>  
      <Dimensions>...</Dimensions>  
            <MeasureGroups>...</MeasureGroups>  
      <Calculations>...</Calculations>  
      <Kpis>...</Kpis>  
            <Actions>...</Actions>  
      <Annotations>...</Annotations>  
   </Perspective>  
</Perspectives>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[檢視方塊](../../../analysis-services/scripting/collections/perspectives-element-assl.md)|  
|子元素|[動作](../../../analysis-services/scripting/collections/actions-element-assl.md)，[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[計算](../../../analysis-services/scripting/collections/calculations-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)， [DefaultMeasure](../../../analysis-services/scripting/properties/defaultmeasure-element-assl.md)， [描述](../../../analysis-services/scripting/properties/description-element-assl.md)，[維度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)，[識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)， [Kpi](../../../analysis-services/scripting/collections/kpis-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)， [MeasureGroups](../../../analysis-services/scripting/collections/measuregroups-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)，[翻譯](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 檢視方塊會提供 Cube 的子集，以便選取要包含的維度、階層、屬性和其他詳細資料，以及定義要包含的資料配量。 檢視方塊是由單一 Cube 所擁有。 您無法在檢視方塊內部覆寫或加入物件。所有維度、階層和其他詳細資料都必須存在基礎 Cube 中。 此外，您也無法加入物件並將它們標示為不顯示。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Perspective>。  
  
## <a name="see-also"></a>請參閱＜  
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
