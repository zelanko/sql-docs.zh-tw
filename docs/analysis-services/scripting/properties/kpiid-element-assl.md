---
title: "KpiID 元素 (ASSL) |Microsoft 文件"
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
- KpiID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- KpiID
helpviewer_keywords:
- KpiID element
ms.assetid: a76395bc-bc84-40f8-9770-6275842f93b5
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c464e68cab5ba1f4e9ae87b6ae11fb185068373e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="kpiid-element-assl"></a>KpiID 元素 (ASSL)
  包含產生關聯的識別項 (ID) [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)具有項目[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<PerspectiveKpi>  
      ...  
   <KpiID>...</KpiID>  
   ...  
</PerspectiveKpi>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[PerspectiveKpi](../../../analysis-services/scripting/data-type/perspectivekpi-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**KpiID**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.PerspectiveKpi>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 (ASSL)](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

