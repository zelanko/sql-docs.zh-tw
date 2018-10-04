---
title: MdxScript 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MdxScript Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MdxScript
helpviewer_keywords:
- MdxScript element
ms.assetid: 0c59a550-dc95-4d50-948a-bb99348bdd86
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f1e138b4112a96bc6cdd5e08af0dbd0941a422d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106528"
---
# <a name="mdxscript-element-assl"></a>MdxScript 元素 (ASSL)
  包含相關聯的多維度運算式 (MDX) 指令碼的相關資訊[Cube](cube-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MdxScripts>  
   <MdxScript>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Annotations>...</Annotations>  
      <Commands>...</Commands>  
      <DefaultScript>...</DefaultScript>  
      <CalculationProperties>...</CalculationProperties>  
   </MdxScript>  
</MdxScripts>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MdxScripts](../collections/mdxscripts-element-assl.md)|  
|子元素|[註釋](../collections/annotations-element-assl.md)， [CalculationProperties](../collections/calculationproperties-element-assl.md)，[命令](../collections/commands-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [DefaultScript](../properties/defaultscript-element-assl.md)， [描述](../properties/description-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)，[名稱](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 根據預設，指令碼的 `DefaultScript` 元素會設定為 `True`。 將特定指令碼的 `DefaultScript` 設定為 `True` 就會將所有其他指令碼的 `DefaultScript` 設定為 `False`。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.MdxScript>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
