---
title: ScalarMiningStructureColumn 資料類型 (ASSL) |Microsoft 文件
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
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 15e88a5e82dc960e3428587b8d74a046781b90ef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134711"
---
# <a name="scalarminingstructurecolumn-data-type-assl"></a>ScalarMiningStructureColumn 資料類型 (ASSL)
  定義衍生的資料類型，表示[MiningStructureColumn](miningstructurecolumn-data-type-assl.md)包含純量值，而不是巢狀資料表與相關聯的項目[TableMiningStructureColumn](tableminingstructurecolumn-data-type-assl.md)項目其中包含巢狀的資料表。  
  
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
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[ClassifiedColumnID](../properties/id-element-assl.md)，[內容](../properties/content-element-assl.md)， [DiscretizationBucketCount](../properties/discretizationbucketcount-element-assl.md)， [DiscretizationMethod](../properties/discretizationmethod-element-assl.md)，[發佈](../properties/distribution-element-assl.md)，[IsKey](../properties/iskey-element-assl.md)， [KeyColumns](../collections/columns-element-assl.md)， [ModelingFlags](../collections/modelingflags-element-assl.md)， [NameColumn](../objects/column-element-assl.md)，[來源](../properties/source-element-binding-assl.md)， [翻譯](../collections/translations-element-assl.md)|  
|衍生的元素|[資料行](../objects/column-element-assl.md)([資料行](../collections/columns-element-assl.md)集合[MiningStructure](../objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  