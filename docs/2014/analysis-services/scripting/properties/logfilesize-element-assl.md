---
title: LogFileSize 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- LogFileSize Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LogFileSize
helpviewer_keywords:
- LogFileSize element
ms.assetid: d2135e68-57a9-4144-8403-9627041f2a58
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bca304c55b352f68a3d5699f20b000f08831ab89
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061238"
---
# <a name="logfilesize-element-assl"></a>LogFileSize 元素 (ASSL)
  指定最大記錄檔大小 (以 MB 為單位)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Trace>  
  
   <LogFileSize>...</LogFileSize>  
  
</Trace>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|Integer|  
|預設值|`5` (MB)|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[追蹤](../objects/trace-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`LogFileSize`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>另請參閱  
 [追蹤項目&#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
