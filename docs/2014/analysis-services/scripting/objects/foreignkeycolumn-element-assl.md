---
title: ForeignKeyColumn 元素 (ASSL) |Microsoft Docs
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
- ForeignKeyColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ForeignKeyColumn
helpviewer_keywords:
- ForeignKeyColumn element
ms.assetid: 6c00dcc6-8d5b-4293-8b72-c7a22e298c8d
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 824589905f1acf1834e971b8a049005ef1465c26
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37207878"
---
# <a name="foreignkeycolumn-element-assl"></a>ForeignKeyColumn 元素 (ASSL)
  識別關聯式資料來源之父資料表的聯結。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ForeignKeyColumns>  
   <ForeignKeyColumn xsi:type="DataItem">...</ForeignKeyColumn>  
</ForeignKeyColumns>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ForeignKeyColumns](../collections/columns-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如需詳細資訊`DataItem`型別，包括 Analysis Services 指令碼語言 (ASSL) 物件和屬性的資料表`DataItem`類型，請參閱[DataItem 資料類型&#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md)。  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `ForeignKeyColumns` 集合父系的元素是 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [TableMiningStructureColumn 資料類型&#40;ASSL&#41;](../data-type/miningstructurecolumn-data-type-assl.md)   
 [MiningStructureColumn 資料類型&#40;ASSL&#41;](../data-type/miningstructurecolumn-data-type-assl.md)   
 [MiningStructure 元素&#40;ASSL&#41;](miningstructure-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
