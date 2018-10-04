---
title: LogFileName 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- LogFileName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LogFileName
helpviewer_keywords:
- LogFileName element
ms.assetid: 80c7530d-ef73-44c3-88b5-c11c0f290946
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 14f2ae0f1d90459bbe7d1fc1b80e43847c15c1b3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48174318"
---
# <a name="logfilename-element-assl"></a>LogFileName 元素 (ASSL)
  包含的記錄檔的檔名[追蹤](../objects/trace-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Trace>  
   ...  
   <LogFileName>...</LogFileName>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[追蹤](../objects/trace-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 記錄檔會儲存到執行個體的記錄檔資料夾[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 對應至父系的元素`LogFileName`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>另請參閱  
 [追蹤項目&#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
