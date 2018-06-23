---
title: Source 元素 (Measure) (ASSL) |Microsoft 文件
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
- Source Element (Measure)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 9bae7ba4-3065-4623-b3e0-d54cebea7503
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ed41316f62469268d86a89d0c0a5e59f07c8f726
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032172"
---
# <a name="source-element-measure-assl"></a>Source 元素 (Measure) (ASSL)
  包含詳細資料包含的值之來源的[量值](../objects/measure-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Measure>  
      ...  
   <Source xsi:type="DataItem">...</Source>  
      ...  
</Measure>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[量值](../objects/measure-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `Source`的`DataItem`，做為`Source`的`Measure`，接著可以屬於型別[RowBinding](../data-type/binding-data-type-assl.md)， [ColumnBinding](../data-type/columnbinding-data-type-assl.md)， [MeasureBinding](../data-type/measurebinding-data-type-assl.md)，或[CubeDimensionBinding](../data-type/dimensionbinding-data-type-assl.md)。  
  
 如需有關`DataItem`型別，包括資料表之 ASSL 物件和屬性的`DataItem`類型，請參閱[DataItem 資料類型&#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md)。  
  
 對應至父系的項目`Source`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Measure>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  