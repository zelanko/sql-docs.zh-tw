---
title: "SilenceOverrideInterval 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SilenceOverrideInterval Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: SilenceOverrideInterval
helpviewer_keywords: SilenceOverrideInterval element
ms.assetid: 0dcd2db4-9bc0-4460-b1dd-def0b38c4617
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 807afbc1cabae00efacb04f7389d841e26849e27
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="silenceoverrideinterval-element-assl"></a>SilenceOverrideInterval 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義在收到初始通知之後多維度 OLAP (MOLAP) 影像處理無條件開始之前必須經過的時間量。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <SilenceOverrideInterval>...</SilenceOverrideInterval>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|duration|  
|預設值|P0s|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值**SilenceOverrideInterval**的值會覆寫**SilenceInterval**如果無回應期間收到通知。  
  
 對應目的父代的項目**SilenceOverrideInterval**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ProactiveCaching>。  
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
