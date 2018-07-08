---
title: 量值元素 (ASSL) |Microsoft Docs
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
- Measure Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Measure
helpviewer_keywords:
- Measure element
ms.assetid: 4c2c2ed1-7f78-4564-982a-132f13bea36f
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 80d59a5356bf1c0b5712e729f230fff9383603cc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159329"
---
# <a name="measure-element-assl"></a>Measure 元素 (ASSL)
  定義量值。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Measures>  
   <Measure> <!-- ancestor: MeasureGroup -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <AggregateFunction>...</AggregateFunction>  
            <DataType>...</DataType>  
            <Source>...</Source>  
      <Visible>...</Visible>  
      <MeasureExpression>...</MeasureExpression>  
      <DisplayFolder>...</DisplayFolder>  
      <FormatString>...</FormatString>  
      <BackColor>...</BackColor>  
      <ForeColor>...</ForeColor>  
            <FontName>...</FontName>  
            <FontSize>...</FontSize>  
            <FontFlags>...</FontFlags>  
            <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Measure>  
   <!-- or  -->  
   <Measure xsi:type="AggregationInstanceMeasure">...</Measure> <!-- parent: AggregationInstance -->  
      <!-- or  -->  
   <Measure xsi:type="MeasureBinding">...</Measure> <!-- ancestor: MeasureGroupBinding (out-of-line) -->  
   <!-- or  -->  
   <Measure xsi:type="PerspectiveMeasure">...</Measure> <!-- ancestor: PerspectiveMeasureGroup -->  
</Measures>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
|上階或父系|資料類型|  
|------------------------|---------------|  
|[AggregationInstance](../data-type/binding-data-type-assl.md)|  
|[MeasureGroup](group-element-assl.md)|無|  
|[MeasureGroupBinding （外的行）](../data-type/measurebinding-data-type-assl.md)|  
|[PerspectiveMeasureGroup](../data-type/perspectivemeasure-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[量值](../collections/measures-element-assl.md)|  
  
|上階或父系|子元素|  
|------------------------|--------------------|  
|[MeasureGroup](../properties/aggregatefunction-element-assl.md)，[註解](../collections/annotations-element-assl.md)， [BackColor](../properties/backcolor-element-assl.md)，[資料類型](../properties/datatype-element-assl.md)，[描述](../properties/description-element-assl.md)， [DisplayFolder](../properties/displayfolder-element-assl.md)， [FontFlags](../properties/fontflags-element-assl.md)， [FontName](../properties/name-element-assl.md)， [FontSize](../properties/fontsize-element-assl.md)， [ForeColor](../properties/forecolor-element-assl.md)， [FormatString](../properties/formatstring-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [MeasureExpression](../properties/expression-element-assl.md)，[名稱](../properties/name-element-assl.md)，[來源](../properties/source-element-measure-assl.md)，[翻譯](../collections/translations-element-assl.md)，[可見](../properties/visible-element-assl.md)|  
|All others|無|  
  
## <a name="remarks"></a>備註  
 繫結詳細資料可提供給量值。 然後，這些詳細資料會當做每個資料分割的預設值。  
  
 在較大的 Cube 中，可能會有數百個量值和階層。 `DisplayFolder` 屬性會定義用戶端的使用者外觀。 `DisplayFolder` 屬性的值可以包含下列任何一個選項：  
  
-   空白，表示量值不屬於資料夾。  
  
-   包含單一資料夾名稱，表示量值應該轉譯為屬於具有相同名稱的資料夾。  
  
-   包含反斜線分隔的多個資料夾名稱 (\\)，用來表示內嵌的資料夾階層。  
  
 `DisplayFolder` 屬性也會套用至導出量值和階層。  
  
 在「分析管理物件」(AMO) 物件模型中對應的元素是 <xref:Microsoft.AnalysisServices.Measure> 和 <xref:Microsoft.AnalysisServices.PerspectiveMeasure>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
