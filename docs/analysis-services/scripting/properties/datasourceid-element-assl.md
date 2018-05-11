---
title: DataSourceID 元素 (ASSL) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 39787445a1efb693bdfcc9b8285050800ac06b7c
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="datasourceid-element-assl"></a>DataSourceID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  識別[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)與父元素相關聯的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeBinding> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <DataSourceID>...</DataSourceID>  
   ...  
</CubeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|取決於內容|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubeBinding](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)， [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)， [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)， [QueryBinding](../../../analysis-services/scripting/data-type/querybinding-data-type-assl.md)， [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)， [TableBinding](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目**DataSourceID**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.CubeDimensionBinding>， <xref:Microsoft.AnalysisServices.DimensionBinding>， <xref:Microsoft.AnalysisServices.MeasureGroupBinding>， <xref:Microsoft.AnalysisServices.QueryBinding>， <xref:Microsoft.AnalysisServices.DataSourceView>，和<xref:Microsoft.AnalysisServices.TableBinding>.  
  
## <a name="see-also"></a>另請參閱  
 [ID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/id-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
