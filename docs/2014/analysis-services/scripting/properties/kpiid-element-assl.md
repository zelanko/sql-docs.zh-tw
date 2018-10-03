---
title: KpiID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- KpiID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KpiID
helpviewer_keywords:
- KpiID element
ms.assetid: a76395bc-bc84-40f8-9770-6275842f93b5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f89e393249215ebf700cfde543f8b645a268536b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090498"
---
# <a name="kpiid-element-assl"></a>KpiID 元素 (ASSL)
  包含產生關聯的識別碼 (ID) [Kpi](../objects/kpi-element-assl.md)項目[觀點來看](../objects/perspective-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<PerspectiveKpi>  
      ...  
   <KpiID>...</KpiID>  
   ...  
</PerspectiveKpi>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[PerspectiveKpi](../data-type/perspectivekpi-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`KpiID`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.PerspectiveKpi>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 (ASSL)](properties-assl.md)  
  
  
