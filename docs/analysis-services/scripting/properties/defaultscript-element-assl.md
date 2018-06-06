---
title: DefaultScript 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e21b89833edf744a6e47474e9c438be74530479c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="defaultscript-element-assl"></a>DefaultScript 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
