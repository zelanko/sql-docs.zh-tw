---
title: MiningModelColumn 資料類型 (ASSL) |Microsoft Docs
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
- MiningModelColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelColumn
helpviewer_keywords:
- MiningModelColumn data type
ms.assetid: de8bf815-43b4-4983-bdb9-b67e8563be0e
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 983c164d32408182d943e9509ce5a125efb25f9a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37259664"
---
# <a name="miningmodelcolumn-data-type-assl"></a>MiningModelColumn 資料類型 (ASSL)
  定義代表資料行中的相關資訊的基本資料類型[MiningModel](../objects/miningmodel-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningModelColumn>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</<Description>  
      <SourceColumnID>...</SourceColumnID>  
            <Usage>...</Usage>  
            <Translations>...</Translations>  
      <Columns>...</Columns>  
      <ModelingFlags>...</ModelingFlags>  
      <Annotations>...</Annotations>  
</MiningModelColumn>  
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
|子元素|[註釋](../collections/annotations-element-assl.md)，[資料行](../collections/columns-element-assl.md)，[描述](../properties/description-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [ModelingFlags](../collections/modelingflags-element-assl.md)，[名稱](../properties/name-element-assl.md)[SourceColumnID](../properties/sourcecolumnid-element-assl.md)，[翻譯](../collections/translations-element-assl.md)，[使用量](../properties/usage-element-dimensionattribute-assl.md)|  
|衍生的元素|[資料行](../objects/column-element-assl.md)([資料行](../collections/columns-element-assl.md)，集合[MiningModel](../objects/miningmodel-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.MiningModelColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
