---
title: ScriptCacheProcessingMode 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0566ea0411eb3f6574d03e738017d8ca6a5bdf2f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36147032"
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
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*規則*|伺服器會在處理期間建立指令碼快取。|  
|*延遲*|伺服器會在處理之後建立指令碼快取。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `ScriptCacheProcessingMode` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ScriptCacheProcessingMode>。  
  
 對應目的父代的項目`ScriptCacheProcessingMode`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Cube>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  