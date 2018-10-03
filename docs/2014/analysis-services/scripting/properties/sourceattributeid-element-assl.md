---
title: SourceAttributeID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- SourceAttributeID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SourceAttributeID
helpviewer_keywords:
- SourceAttributeID element
ms.assetid: 8973eb62-6142-4ce2-ad42-c8be2b43c04f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8ce0ae2b0f417c9426821c2d5da0d03b0507b9f4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113458"
---
# <a name="sourceattributeid-element-assl"></a>SourceAttributeID 元素 (ASSL)
  包含來源屬性的識別碼 (ID)[層級](../objects/level-element-assl.md)項目為基礎。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Level>  
   ...  
   <SourceAttributeID>...</SourceAttributeID>  
   ...  
</Level>  
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
|父元素|[Level](../objects/level-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 對應的父代的項目`SourceAttributeID`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Level>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
