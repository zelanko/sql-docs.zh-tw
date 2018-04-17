---
title: Collation 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
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
- Collation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Collation
helpviewer_keywords:
- Collation element
ms.assetid: 9b6dbe19-543e-43e6-abe9-1e8b4dfaa275
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: db1cdb33f9fffe6c9a28269a12cc83ca9419bd8e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="collation-element-assl"></a>Collation 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]決定父元素所使用的定序。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Database> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Collation>...</Collation>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)，[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)， [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)，[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **定序**字串包含地區設定識別碼 (LCID) 和比較旗標，以底線字元分隔。 例如，Latin1_General_CI_AS 是可接受的字串。  
  
 對應至父系的項目**定序**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.Database>， <xref:Microsoft.AnalysisServices.DataItem>， <xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.MiningModel>，和<xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
