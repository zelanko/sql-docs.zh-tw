---
title: CreatedTimestamp 元素 (ASSL) |Microsoft 文件
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
- CreatedTimestamp Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CreatedTimestamp
helpviewer_keywords:
- CreatedTimestamp element
ms.assetid: 35f5dd33-ea82-4be3-a117-69136aa9d1a4
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 60e59f981f5430e74d3c83a3586f39f5538f3bae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136498"
---
# <a name="createdtimestamp-element-assl"></a>CreatedTimestamp 元素 (ASSL)
  包含父元素的唯讀建立時間戳記。  
  
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
|父元素|[Assembly](../objects/assembly-element-assl.md), [Cube](../objects/cube-element-assl.md), [Database](../objects/database-element-assl.md), [DataSource](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [Dimension](../objects/dimension-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [Partition](../objects/partition-element-assl.md), [Permission](../data-type/permission-data-type-assl.md), [Perspective](../objects/perspective-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `CreatedTimestamp`元素包含一個唯讀`DateTime`值，表示指定的執行個體建立物件的時間與日期[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 這個元素的值不得為空白。  
  
 對應至父系的項目`CreatedTimestamp`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Assembly>， <xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.Database>， <xref:Microsoft.AnalysisServices.DataSource>， <xref:Microsoft.AnalysisServices.DataSourceView>， <xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.MdxScript>， <xref:Microsoft.AnalysisServices.MeasureGroup>， <xref:Microsoft.AnalysisServices.MiningModel>， <xref:Microsoft.AnalysisServices.MiningStructure>， <xref:Microsoft.AnalysisServices.Partition>， <xref:Microsoft.AnalysisServices.Permission>，和<xref:Microsoft.AnalysisServices.Perspective>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  