---
title: Aliases 元素 (ASSL) |Microsoft 文件
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
- Aliases Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Aliases
helpviewer_keywords:
- Aliases element
ms.assetid: 9de9e683-d30d-4d61-b32d-c5a946825742
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 60673c26bf4a430c842da0fb61c98de7242ccd1c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132296"
---
# <a name="aliases-element-assl"></a>Aliases 元素 (ASSL)
  包含集合[別名](../properties/alias-element-assl.md)與相關聯的項目[帳戶](../objects/account-element-assl.md)項目  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Account>  
      ...  
   <Aliases>  
      <Alias>...</Alias>  
      </Aliases>  
      ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無 (集合)|  
|預設值|無 (集合)|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[帳戶](../objects/account-element-assl.md)|  
|子元素|[別名](../properties/alias-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目`Aliases`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Account>。  
  
## <a name="see-also"></a>另請參閱  
 [帳戶項目&#40;ASSL&#41;](accounts-element-assl.md)   
 [Database 元素&#40;ASSL&#41;](../objects/database-element-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  