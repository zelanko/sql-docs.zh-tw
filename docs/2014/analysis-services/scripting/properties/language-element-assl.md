---
title: Language 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Language Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LANGUAGE
helpviewer_keywords:
- Language element
ms.assetid: 4d745d23-6b1f-4a85-97cf-d034cc41356f
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 09a51320df0cf5d4246fbc14307f488c2d754e3c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145038"
---
# <a name="language-element-assl"></a>Language 元素 (ASSL)
  包含父元素的語言識別碼。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Cube> <!-- or Database, Dimension, MiningModel, MiningStructure, Translation -->  
   ...  
   <Language>...</Language>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|Integer|  
|預設值|無|  
  
 **基數**  
  
|上階或父系|基數|  
|------------------------|-----------------|  
|[轉譯](../objects/translation-element-assl.md)|1-1：只出現一次的必要元素。|  
|All others|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Cube](../objects/cube-element-assl.md)，[資料庫](../objects/database-element-assl.md)，[維度](../objects/dimension-element-assl.md)， [MiningModel](../objects/miningmodel-element-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)，[轉譯](../objects/translation-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `Language` 元素包含父元素所使用的預設語言識別碼，或 `Translation` 元素的特定語言識別碼。 語言應該使用地區設定識別碼 (LCID) 代碼定義。 例如，LCID 1033 是用來表示英文 (美國) 語言。  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Language` 父系的元素是 <xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.MiningModel>、<xref:Microsoft.AnalysisServices.MiningStructure> 和 <xref:Microsoft.AnalysisServices.Translation>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  