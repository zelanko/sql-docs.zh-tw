---
title: ScriptCacheProcessingMode 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ScriptCacheProcessingMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ScriptCacheProcessingMode
helpviewer_keywords:
- ScriptCacheProcessingMode element
ms.assetid: 95c0723c-69a4-43e7-b743-f712180a7681
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d74499d0678f920fe9f09b9cdc2d8626045a380
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48221338"
---
# <a name="scriptcacheprocessingmode-element-assl"></a>ScriptCacheProcessingMode 元素 (ASSL)
  指出伺服器應該在處理期間或處理之後建立指令碼快取。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Cube>  
   ...  
      <ScriptCacheProcessingMode>...</ScriptCacheProcessingMode>  
   ...  
</Cube>  
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
|父元素|[Cube](../objects/cube-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*規則*|伺服器會在處理期間建立指令碼快取。|  
|*延遲*|伺服器會在處理之後建立指令碼快取。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `ScriptCacheProcessingMode` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ScriptCacheProcessingMode>。  
  
 對應至父系的元素`ScriptCacheProcessingMode`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Cube>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
