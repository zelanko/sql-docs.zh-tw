---
title: "DataItem 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DataItem Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DataItem
helpviewer_keywords:
- DataItem data type
ms.assetid: f4f5155f-9c3d-49a1-a390-a9c734fafbce
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3986d23e02287fcf1d411df19a7b46a8768489b7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dataitem-data-type-assl"></a>DataItem 資料類型 (ASSL)
  定義代表某個資料項目 (例如資料行或屬性) 之資料相關特性的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataItem>  
   <DataType>...</DataType>  
   <DataSize>...</DataSize>  
   <MimeType>...</MimeType>  
   <NullProcessing>...</NullProcessing>  
   <Trimming>...</Trimming>  
   <InvalidXmlCharacters>...</InvalidXmlCharacters>  
      <Collation>...</Collation>  
   <Format>...</Format>  
   <Source>...</Source>  
   <Annotations>...</Annotations>  
</DataItem>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[定序](../../../analysis-services/scripting/properties/collation-element-assl.md)， [DataSize](../../../analysis-services/scripting/properties/datasize-element-assl.md)， [DataType](../../../analysis-services/scripting/properties/datatype-element-assl.md)，[格式](../../../analysis-services/scripting/properties/format-element-assl.md)， [InvalidXmlCharacters](../../../analysis-services/scripting/properties/invalidxmlcharacters-element-assl.md)， [MimeType](../../../analysis-services/scripting/properties/mimetype-element-assl.md)， [NullProcessing](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md)，[來源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)，[修剪](../../../analysis-services/scripting/properties/trimming-element-assl.md)|  
|衍生的元素|請參閱「備註」中的表格。|  
  
## <a name="remarks"></a>備註  
 **DataItem**資料型別用於任何資料的項目，可以繫結; 例如，量值、 屬性索引鍵和屬性名稱。 相關的詳細資料和適用的預設值會因使用方式而不同。例如，屬性名稱必須是字串。  
  
 執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]接受只有特定的一組資料類型。 使用其他資料類型會產生錯誤，而不會隱含轉換成其中一種有效的類型。  
  
 下表列出類型的項目**DataItem**。  
  
|父元素|類型的項目**DataItem**|註解|  
|--------------------|----------------------------------|--------------|  
|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|[CaptionColumn](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md)|**來源**元素**DataItem**必須是型別[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)或[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[CustomRollupColumn](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)|**來源**元素**DataItem**必須是型別[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)或[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[CustomRollupPropertiesColumn](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md)|**來源**元素**DataItem**必須是型別[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)或[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|**來源**元素**DataItem**必須是型別[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)或[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[[Namecolumn]](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|**來源**元素**DataItem**必須是型別[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)或[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[SkippedLevelsColumn](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md)|**來源**元素**DataItem**必須是型別[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)或[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[UnaryOperatorColumn](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md)|**來源**元素**DataItem**必須是型別[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)或[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|**來源**元素**DataItem**必須是型別[RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)， [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)，或[CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|**來源**元素**DataItem**必須是型別[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)或[InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|**來源**元素**DataItem**必須是型別[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[[Namecolumn]](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|**來源**元素**DataItem**必須是型別[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|[ForeignKeyColumn](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md)|**來源**元素**DataItem**必須是型別[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.DataItem>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

