---
title: DataSourceID 元素 (ASSL) |Microsoft Docs
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
- DataSourceID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataSourceID
helpviewer_keywords:
- DataSourceID element
ms.assetid: 2d71ba53-1684-4da0-8da4-fb75033c971b
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 86a5e07518097e01509f24f2969580dec7ba0c34
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263584"
---
# <a name="datasourceid-element-assl"></a>DataSourceID 元素 (ASSL)
  識別[DataSource](../objects/datasource-element-assl.md)與父元素相關聯的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeBinding> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <DataSourceID>...</DataSourceID>  
   ...  
</CubeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|取決於內容|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md)， [CubeDimensionBinding](../data-type/binding-data-type-assl.md)， [DimensionBinding](../data-type/dimensionbinding-data-type-assl.md)， [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)， [QueryBinding](../data-type/querybinding-data-type-assl.md)，[DataSourceView](../objects/datasourceview-element-assl.md)， [TableBinding](../data-type/tablebinding-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應至 `DataSourceID` 父系的元素是 <xref:Microsoft.AnalysisServices.CubeDimensionBinding>、<xref:Microsoft.AnalysisServices.DimensionBinding>、<xref:Microsoft.AnalysisServices.MeasureGroupBinding>、<xref:Microsoft.AnalysisServices.QueryBinding>、<xref:Microsoft.AnalysisServices.DataSourceView> 和 <xref:Microsoft.AnalysisServices.TableBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [ID 項目&#40;ASSL&#41;](id-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
