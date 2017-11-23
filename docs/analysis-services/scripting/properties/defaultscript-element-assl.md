---
title: "DefaultScript 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
apiname: DefaultScript Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DefaultScript
helpviewer_keywords: DefaultScript element
ms.assetid: 60716e63-2d64-4774-9ac9-253efe612fa5
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 72a8171e9dedf77983c685d3081a0525a1d4015c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="defaultscript-element-assl"></a>DefaultScript 元素 (ASSL)
  識別預設[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)中的項目[MdxScripts](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)集合。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MdxScript>  
   ...  
   <DefaultScript>...</DefaultScript>  
   ...  
</MdxScript>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|**True**|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值設定**DefaultScript**至**True**的一個指令碼設定的值**DefaultScript**至**False**的所有其他**MdxScript**中的項目**MdxScripts**集合。  
  
 對應目的父代的項目**DefaultScript**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.MdxScript>。  
  
## <a name="see-also"></a>請參閱＜  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
