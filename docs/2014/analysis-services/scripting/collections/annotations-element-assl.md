---
title: Annotations 元素 (ASSL) |Microsoft 文件
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
- Annotations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Annotations
helpviewer_keywords:
- Annotations element
ms.assetid: b2236075-6a48-470d-8182-b0de112e258a
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b673e7f9edd199d32f7bd89d082d39b6d58f876a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132006"
---
# <a name="annotations-element-assl"></a>Annotations 元素 (ASSL)
  包含集合[註解](../objects/annotation-element-assl.md)元素與父元素相關聯。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Account>  
<!-- or another object in the Analysis Services Scripting Language -->  
   ...  
   <Annotations>  
      <Annotation>...</Annotation>  
   </Annotations>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|大部分使用 Analysis Services 指令碼語言的物件|  
|子元素|[註解](../objects/annotation-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.AnnotationCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  