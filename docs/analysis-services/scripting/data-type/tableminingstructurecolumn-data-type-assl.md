---
title: TableMiningStructureColumn 資料類型 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 01d5afbc2d69985ab571ee55b2583f08d090a446
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34034459"
---
# <a name="tableminingstructurecolumn-data-type-assl"></a>TableMiningStructureColumn 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義衍生的資料類型，表示[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)包含巢狀的資料表，而不是與相關聯的純量值的項目[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)包含純量值的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<TableMiningStructureColumn>  
   <!-- The following elements extend MiningStructureColumn -->  
   <ForeignKeyColumn>..</ForeignKeyColumn>  
   <SourceMeasureGroup>..</SourceMeasureGroup>  
   <Columns>..</Columns>  
   <Translations>..</Translations>  
</TableMiningStructureColumn>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[資料行](../../../analysis-services/scripting/collections/columns-element-assl.md)， [ForeignKeyColumn](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md)， [SourceMeasureGroup](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)，[翻譯](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|衍生的元素|[資料行](../../../analysis-services/scripting/objects/column-element-assl.md)([資料行](../../../analysis-services/scripting/collections/columns-element-assl.md)集合[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.TableMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
