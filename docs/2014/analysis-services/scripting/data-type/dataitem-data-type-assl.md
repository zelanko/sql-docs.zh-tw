---
title: DataItem 資料類型 (ASSL) |Microsoft Docs
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
- DataItem Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataItem
helpviewer_keywords:
- DataItem data type
ms.assetid: f4f5155f-9c3d-49a1-a390-a9c734fafbce
caps.latest.revision: 44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b2646dcce64672d98d33ecff3575016269379325
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37300888"
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
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[註釋](../collections/annotations-element-assl.md)，[定序](../properties/collation-element-assl.md)， [DataSize](../properties/datasize-element-assl.md)，[資料類型](../properties/datatype-element-assl.md)，[格式](../properties/format-element-assl.md)， [InvalidXmlCharacters](../properties/invalidxmlcharacters-element-assl.md)， [MimeType](../properties/mimetype-element-assl.md)， [NullProcessing](../properties/nullprocessing-element-assl.md)，[來源](../properties/source-element-binding-assl.md)，[修剪](../properties/trimming-element-assl.md)|  
|衍生的元素|請參閱「備註」中的表格。|  
  
## <a name="remarks"></a>備註  
 `DataItem` 資料類型會用於可繫結的任何資料項目。例如，量值、屬性索引鍵和屬性名稱。 相關的詳細資料和適用的預設值會因使用方式而不同。例如，屬性名稱必須是字串。  
  
 執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]僅接受特定集合的資料型別。 使用其他資料類型會產生錯誤，而不會隱含轉換成其中一種有效的類型。  
  
 下表列出 `DataItem` 類型的元素。  
  
|父元素|`DataItem` 類型的元素|註解|  
|--------------------|----------------------------------|--------------|  
|[AttributeTranslation](../objects/column-element-assl.md)|`Source` 項目`DataItem`必須是型別[ColumnBinding](binding-data-type-assl.md)或[AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/customrollupcolumn-element-assl.md)|`Source` 項目`DataItem`必須是型別[ColumnBinding](binding-data-type-assl.md)或[AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/customrolluppropertiescolumn-element-assl.md)|`Source` 項目`DataItem`必須是型別[ColumnBinding](binding-data-type-assl.md)或[AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/keycolumn-element-assl.md)|`Source` 項目`DataItem`必須是型別[ColumnBinding](binding-data-type-assl.md)， [AttributeBinding](attributebinding-data-type-assl.md)或[TimeBinding](timebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/namecolumn-element-assl.md)|`Source` 項目`DataItem`必須是型別[ColumnBinding](binding-data-type-assl.md)或[AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/skippedlevelscolumn-element-assl.md)|`Source` 項目`DataItem`必須是型別[ColumnBinding](binding-data-type-assl.md)或[AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/unaryoperatorcolumn-element-assl.md)|`Source` 項目`DataItem`必須是型別[ColumnBinding](binding-data-type-assl.md)或[AttributeBinding](attributebinding-data-type-assl.md)|  
|[量值](../objects/measure-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|`Source` 項目`DataItem`必須是型別[RowBinding](rowbinding-data-type-assl.md)， [ColumnBinding](binding-data-type-assl.md)， [MeasureBinding](measurebinding-data-type-assl.md)，或[CubeDimensionBinding](dimensionbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)|[KeyColumn](../objects/keycolumn-element-assl.md)|`Source` 項目`DataItem`必須是型別[ColumnBinding](binding-data-type-assl.md)， [AttributeBinding](attributebinding-data-type-assl.md)或[InheritedBinding](inheritedbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[KeyColumn](../objects/keycolumn-element-assl.md)|`Source` 項目`DataItem`必須是型別[ColumnBinding](binding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[[Namecolumn]](../objects/namecolumn-element-assl.md)|`Source` 項目`DataItem`必須是型別[ColumnBinding](binding-data-type-assl.md)|  
|[TableMiningStructureColumn](../objects/foreignkeycolumn-element-assl.md)|`Source` 項目`DataItem`必須是型別[ColumnBinding](binding-data-type-assl.md)|  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.DataItem>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
