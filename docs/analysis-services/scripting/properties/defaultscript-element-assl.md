---
title: "DefaultScript 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
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
ms.openlocfilehash: 7560b3ce0fe03700f73be4d0ef34817c03619950
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="defaultscript-element-assl"></a>DefaultScript 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]識別預設[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)中的項目[MdxScripts](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)集合。  
  
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
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
