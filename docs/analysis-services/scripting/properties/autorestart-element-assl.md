---
title: "AutoRestart 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AutoRestart Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AutoRestart
helpviewer_keywords: AutoRestart element
ms.assetid: 4c6a0e40-8e13-4d63-bf98-9470ffe95d02
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 128defdc7641fe84fbe4f1b253f464ea647a72be
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="autorestart-element-assl"></a>AutoRestart 元素 (ASSL)
  決定是否[追蹤](../../../analysis-services/scripting/objects/trace-element-assl.md)項目應該自動重新啟動[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]服務停止並重新啟動。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Trace>  
   ...  
   <AutoRestart>...</AutoRestart>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|**False**|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[追蹤](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**AutoRestart**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>請參閱＜  
 [Traces 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/traces-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
