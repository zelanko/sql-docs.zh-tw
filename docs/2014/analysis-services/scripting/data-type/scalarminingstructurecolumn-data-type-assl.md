---
title: ScalarMiningStructureColumn 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ScalarMiningStructureColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ScalarMiningStructureColumn
helpviewer_keywords:
- ScalarMiningStructureColumn data type
ms.assetid: 8f4afc15-601c-4189-bc45-f5a216aed879
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 00ef1218cf9dcd6029f72b6a0b9384ddb0e8c9eb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048869"
---
# <a name="scalarminingstructurecolumn-data-type-assl"></a>ScalarMiningStructureColumn 資料類型 (ASSL)
  定義衍生的資料類型，表示[MiningStructureColumn](miningstructurecolumn-data-type-assl.md)包含純量值，而不是巢狀資料表與相關聯的項目[TableMiningStructureColumn](tableminingstructurecolumn-data-type-assl.md)項目包含巢狀的資料表。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ScalarMiningStructureColumn>  
   <!-- The following elements extend MiningStructureColumn -->  
   <IsKey>...</IsKey>  
   <Source>...</Source>  
   <Distribution>...</Distribution>  
   <ModelingFlags>...</ModelingFlags>  
   <Content>...</Content>  
   <ClassifiedColumnID>...</<ClassifiedColumnI  
   <DiscretizationMethod>...</DiscretizationMethod>  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   <KeyColumns>...</KeyColumns>  
   <NameColumn>...</NameColumn>  
   <Translations>...</Translations>  
</ScalarMiningStructureColumn>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[MiningStructureColumn](miningstructurecolumn-data-type-assl.md)|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[ClassifiedColumnID](../properties/id-element-assl.md)，[內容](../properties/content-element-assl.md)， [DiscretizationBucketCount](../properties/discretizationbucketcount-element-assl.md)， [DiscretizationMethod](../properties/discretizationmethod-element-assl.md)，[發佈](../properties/distribution-element-assl.md)，[IsKey](../properties/iskey-element-assl.md)， [KeyColumns](../collections/columns-element-assl.md)， [ModelingFlags](../collections/modelingflags-element-assl.md)， [NameColumn](../objects/column-element-assl.md)，[來源](../properties/source-element-binding-assl.md)， [翻譯](../collections/translations-element-assl.md)|  
|衍生的元素|[資料行](../objects/column-element-assl.md)([資料行](../collections/columns-element-assl.md)的集合[MiningStructure](../objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
