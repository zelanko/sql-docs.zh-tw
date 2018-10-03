---
title: DefaultScript 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DefaultScript Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DefaultScript
helpviewer_keywords:
- DefaultScript element
ms.assetid: 60716e63-2d64-4774-9ac9-253efe612fa5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a1eef79aabede1198c45c9f5481f13bd597db42c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48152738"
---
# <a name="defaultscript-element-assl"></a>DefaultScript 元素 (ASSL)
  識別預設[MdxScript](../objects/mdxscript-element-assl.md)中的項目[MdxScripts](../collections/mdxscripts-element-assl.md)集合。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MdxScript>  
   ...  
   <DefaultScript>...</DefaultScript>  
   ...  
</MdxScript>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|`True`|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MdxScript](../objects/mdxscript-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 如果您針對某個指令碼將 `DefaultScript` 的值設定為 `True`，系統就會針對 `DefaultScript` 集合中的所有其他 `False` 元素將 `MdxScript` 設定為 `MdxScripts`。  
  
 對應至父系的元素`DefaultScript`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.MdxScript>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
