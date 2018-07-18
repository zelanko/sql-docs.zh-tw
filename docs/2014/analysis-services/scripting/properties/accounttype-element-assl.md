---
title: AccountType 元素 (ASSL) |Microsoft Docs
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
- AccountType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AccountType
helpviewer_keywords:
- AccountType element
ms.assetid: 4fdf17d3-cd84-4bf6-9baf-21e15d4bf71e
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b79eec0531cf2ab9451a93df2e5f1bf0eb2adf0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243428"
---
# <a name="accounttype-element-assl"></a>AccountType 元素 (ASSL)
  包含名稱中所定義之帳戶類型的[資料庫](../objects/database-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Account>  
   ...  
   <AccountType>...</AccountType>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[帳戶](../objects/account-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*收入*|此帳戶是收入帳戶。|  
|*費用*|此帳戶是支出帳戶。|  
|*流程*|此帳戶是現金流量帳戶。|  
|*資產負債*|此帳戶是結餘帳戶。|  
|*資產*|此帳戶是資產帳戶。|  
|*責任*|此帳戶是負債帳戶。|  
|*統計*|此帳戶是統計帳戶。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `AccountType` 允許值的列舉是 <xref:Microsoft.AnalysisServices.AccountTypes>。  
  
## <a name="see-also"></a>另請參閱  
 [帳戶項目&#40;ASSL&#41;](../collections/accounts-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
