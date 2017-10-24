---
title: "DrillThroughAction 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DrillThroughAction Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DrillThroughAction
helpviewer_keywords:
- DrillThroughAction data type
ms.assetid: e212d575-a0d7-4548-92b4-33542ef59034
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8859e7c9187bdbb491d3e67c812268e648aa1173
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drillthroughaction-data-type-assl"></a>DrillThroughAction 資料類型 (ASSL)
  定義代表鑽研動作的衍生資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DrillThroughAction>  
   <!-- The following elements extend Action -->  
   <Default>...</Default>  
   <Columns>...</Columns>  
</DrillThroughAction>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|[動作](../../../analysis-services/scripting/data-type/action-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[資料行](../../../analysis-services/scripting/collections/columns-element-assl.md)，[預設](../../../analysis-services/scripting/properties/default-element-assl.md)|  
|衍生的元素|[動作](../../../analysis-services/scripting/objects/action-element-assl.md)([動作](../../../analysis-services/scripting/collections/actions-element-assl.md)，集合[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)，或[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.DrillThroughAction>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

