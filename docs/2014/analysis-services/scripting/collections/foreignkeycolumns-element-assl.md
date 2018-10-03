---
title: ForeignKeyColumns 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ForeignKeyColumns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ForeignKeyColumns
helpviewer_keywords:
- ForeignKeyColumns element
ms.assetid: 0a673c1a-73dd-4217-aa41-56b340b5e1ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: faefae483593b1c4e4369d3e61347a5c7528c001
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153413"
---
# <a name="foreignkeycolumns-element-assl"></a>ForeignKeyColumns 元素 (ASSL)
  包含可識別關聯式資料來源父資料表之聯結的資料行集合。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningStructureColumn xsi:type="TableMiningStructureColumn">  
   ...  
   <ForeignKeyColumns>  
      <ForeignKeyColumn xsi:type="DataItem">...</ForeignKeyColumn>  
...</ForeignKeyColumns>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)型別的[TableMiningStructureColumn](../data-type/tableminingstructurecolumn-data-type-assl.md)|  
|子元素|[ForeignKeyColumn](../objects/column-element-assl.md)型別的[DataItem](../data-type/dataitem-data-type-assl.md)|  
  
## <a name="see-also"></a>另請參閱  
 [MiningStructure 元素&#40;ASSL&#41;](../objects/miningstructure-element-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
