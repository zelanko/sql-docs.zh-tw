---
title: 輸入元素 (MeasureGroup) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Type Element (MeasureGroup)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 3a584baf-36bb-4e1d-9128-c4758c0b8f06
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 56824f759d6ab5de864a4b64d26371034a69585e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191288"
---
# <a name="type-element-measuregroup-assl"></a>Type 元素 (MeasureGroup) (ASSL)
  指定的型別[MeasureGroup](../objects/group-element-assl.md)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MeasureGroup>  
   ...  
   <Type>...</Type>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*規則*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MeasureGroup](../objects/group-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*規則*|包含一般量值。|  
|*ExchangeRate*|包含外部匯率量值。|  
|*銷售*|包含銷售量值。|  
|*預算*|包含預算量值。|  
|*FinancialReporting*|包含財務報表量值。|  
|*行銷*|包含行銷量值。|  
|*清查*|包含存貨量值。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Type` 允許值的列舉是 <xref:Microsoft.AnalysisServices.MeasureGroupType>。  
  
 對應至父系的元素`Type`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.MeasureGroup>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
