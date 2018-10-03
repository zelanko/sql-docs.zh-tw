---
title: AccountType 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c412993422eb963265f99274544ce6f673d5ad9a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075978"
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
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[帳戶](../objects/account-element-assl.md)|  
|子元素|None|  
  
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
  
  
