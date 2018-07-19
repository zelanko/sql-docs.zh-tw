---
title: StopTime 元素 (ASSL) |Microsoft Docs
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
- StopTime Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- StopTime
helpviewer_keywords:
- StopTime element
ms.assetid: 6f863d53-033b-46e0-9837-e891e739b4b0
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a0a646cf736afbf78b656a2e891b6dafbcfead5c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37302668"
---
# <a name="stoptime-element-assl"></a>StopTime 元素 (ASSL)
  指定的日期和時間[追蹤](../objects/trace-element-assl.md)元素應該停止。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Trace>  
   ...  
   <StopTime>...</StopTime>  
   ...  
</Trace>  
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
|父元素|[追蹤](../objects/trace-element-assl.md)|  
|子元素|無|  
  
 對應至父系的元素`StopTime`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>另請參閱  
 [追蹤項目&#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
