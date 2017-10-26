---
title: "AggregationInstanceSource 元素 (ASSL) |Microsoft 文件"
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
- AggregationInstanceSource Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- AggregationInstanceSource element
ms.assetid: ab58c817-eb2b-4974-8470-2946ca5affea
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 67ba06344f0f8c816c41b6788763fa1a93f70798
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="aggregationinstancesource-element-assl"></a>AggregationInstanceSource 元素 (ASSL)
  識別的使用者定義彙總執行個體繫結至資料來源[分割](../../../analysis-services/scripting/objects/partition-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Partition>  
   ...  
   <AggregationInstanceSource xsi:type="DataSourceViewBinding">...</AggregationInstanceSource>  
   ...  
</Partition>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|[DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料分割](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如果這個元素遺漏或設定為空白字串，系統預設會使用擁有資料分割之 Cube 的資料來源檢視。  
  
 如需有關**繫結**型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表**繫結**型別和繼承階層架構的**繫結**類型，請參閱[繫結資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 如需 ASSL 中資料繫結的概觀，請參閱[資料來源和繫結 & #40;SSAS 多維度 & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

