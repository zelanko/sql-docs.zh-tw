---
title: CurrentTimeMember 元素 (ASSL) |Microsoft 文件
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
- CurrentTimeMember Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CurrentTimeMember
helpviewer_keywords:
- CurrentTimeMember element
ms.assetid: 2e73009c-9f2b-441c-bdf0-ca19b160da4f
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b516ab5286366ad9b339dd13ab798ce0c2b897c1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="currenttimemember-element-assl"></a>CurrentTimeMember 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義的時間維度相關聯的目前成員[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Kpi>  
   ...  
   <CurrentTimeMember>...</CurrentTimeMember>  
   ...  
</AggregationDimension>  
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
|父元素|[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值是評估為時間維度之單一成員的多維度運算式 (MDX) 陳述式，可在評估關鍵效能指標 (KPI) 時用來擷取目前的時間範圍。  
  
 對應目的父代的項目**CurrentTimeMember**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Kpi>。  
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
