---
title: Aliases 元素 (ASSL) |Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 677434b5ea6383e5905a703225edb5e56e3fb4e7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267684"
---
# <a name="aliases-element-assl"></a>Aliases 元素 (ASSL)
  包含的集合[別名](../properties/alias-element-assl.md)相關聯的項目[帳戶](../objects/account-element-assl.md)項目  
  
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
 對應的父代的項目`Aliases`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Account>。  
  
## <a name="see-also"></a>另請參閱  
 [帳戶項目&#40;ASSL&#41;](accounts-element-assl.md)   
 [資料庫項目&#40;ASSL&#41;](../objects/database-element-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
