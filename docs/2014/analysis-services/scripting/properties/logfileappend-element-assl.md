---
title: LogFileAppend 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- LogFileAppend Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LogFileAppend
helpviewer_keywords:
- LogFileAppend element
ms.assetid: f85e94a9-e5c5-478a-a5a0-fc99ed19b582
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bea470af9f145be58e9a6e0d2645f2173097a587
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200448"
---
# <a name="logfileappend-element-assl"></a>LogFileAppend 元素 (ASSL)
  決定是否[追蹤](../objects/trace-element-assl.md)元素會將其記錄輸出附加至現有的記錄檔，還是覆寫它。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Trace>  
  
   <LogFileAppend>...</LogFileAppend>  
  
</Trace>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|False|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[追蹤](../objects/trace-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`LogFileAppend`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>另請參閱  
 [追蹤項目&#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
