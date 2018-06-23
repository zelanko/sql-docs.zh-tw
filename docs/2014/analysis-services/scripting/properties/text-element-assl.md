---
title: 文字元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Text Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- text
helpviewer_keywords:
- Text element
ms.assetid: 0edece73-236f-4661-8102-3fcc29326bf4
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8cfc13728fa8c6f73e14e8534dd911316bb4616f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030367"
---
# <a name="text-element-assl"></a>Text 元素 (ASSL)
  包含文字的[命令](../objects/command-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Text>...</Text>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../objects/command-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目`Text`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Command>。  
  
## <a name="see-also"></a>另請參閱  
 [命令元素&#40;ASSL&#41;](../collections/commands-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  