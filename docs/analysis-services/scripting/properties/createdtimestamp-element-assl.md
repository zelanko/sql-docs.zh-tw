---
title: CreatedTimestamp 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- CreatedTimestamp Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CreatedTimestamp
helpviewer_keywords:
- CreatedTimestamp element
ms.assetid: 35f5dd33-ea82-4be3-a117-69136aa9d1a4
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7b241b7cc65f9bffa687a7d589bc6cb3faa08688
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="createdtimestamp-element-assl"></a>CreatedTimestamp 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含父元素的唯讀建立時間戳記。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Assembly> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <CreatedTimestamp>...</CreatedTimestamp>  
   ...  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|DateTime|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[組件](../../../analysis-services/scripting/objects/assembly-element-assl.md)， [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)，[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)， [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)， [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)，[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)， [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)， [資料分割](../../../analysis-services/scripting/objects/partition-element-assl.md)，[權限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)，[檢視方塊](../../../analysis-services/scripting/objects/perspective-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **CreatedTimestamp**元素包含一個唯讀**DateTime**值，表示指定的執行個體建立物件的時間與日期[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. 這個元素的值不得為空白。  
  
 對應至父系的項目**CreatedTimestamp**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Assembly>， <xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.Database>， <xref:Microsoft.AnalysisServices.DataSource>， <xref:Microsoft.AnalysisServices.DataSourceView>， <xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.MdxScript>， <xref:Microsoft.AnalysisServices.MeasureGroup>， <xref:Microsoft.AnalysisServices.MiningModel>， <xref:Microsoft.AnalysisServices.MiningStructure>， <xref:Microsoft.AnalysisServices.Partition>， <xref:Microsoft.AnalysisServices.Permission>，和<xref:Microsoft.AnalysisServices.Perspective>。  
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
