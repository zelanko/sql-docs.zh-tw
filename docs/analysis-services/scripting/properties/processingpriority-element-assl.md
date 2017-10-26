---
title: "ProcessingPriority 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ProcessingPriority Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ProcessingPriority element
ms.assetid: 95d07f1c-ef8d-4e38-9682-ebb7719dbe52
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9b7c417953e755171f5baeba30539372f82c0244
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="processingpriority-element-assl"></a>ProcessingPriority 元素 (ASSL)
  決定背景作業期間父物件的處理優先權 (例如，延遲彙總、索引或叢集)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Dimension> <!-- or MeasureGroup, Partition -->  
   ...  
   <ProcessingPriority>...</ProcessingPriority>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|Integer|  
|預設值|**0**|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[維度](../../../analysis-services/scripting/data-type/dimension-data-type-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)，[磁碟分割](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目**ProcessingPriority**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.MeasureGroup>，和<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

