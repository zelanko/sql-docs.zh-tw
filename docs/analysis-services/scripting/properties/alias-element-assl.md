---
title: Alias 元素 (ASSL) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3668bc8272e961f1314832999706391f0f318f0b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34033949"
---
# <a name="alias-element-assl"></a>Alias 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義的別名[帳戶](../../../analysis-services/scripting/objects/account-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Aliases>  
      <Alias>...</Alias>  
</Aliases>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[別名](../../../analysis-services/scripting/collections/aliases-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值**別名**元素當做所定義之帳戶的替代名稱**帳戶**父項目，而且可協助識別使用者帳戶類型和彙總函式的組合介面。  
  
 對應目的父代的項目**別名**分析管理物件 (AMO) 物件模型中的集合是<xref:Microsoft.AnalysisServices.Account>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
