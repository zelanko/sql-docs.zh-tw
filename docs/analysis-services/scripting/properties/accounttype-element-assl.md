---
title: "AccountType 元素 (ASSL) |Microsoft 文件"
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
apiname: AccountType Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AccountType
helpviewer_keywords: AccountType element
ms.assetid: 4fdf17d3-cd84-4bf6-9baf-21e15d4bf71e
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e59eeeebc216840a62266cda57da8bdf2838eeba
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="accounttype-element-assl"></a>AccountType 元素 (ASSL)
  包含名稱中所定義之帳戶類型的[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Account>  
   ...  
   <AccountType>...</AccountType>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[帳戶](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*收入*|此帳戶是收入帳戶。|  
|*費用*|此帳戶是支出帳戶。|  
|*資料流程*|此帳戶是現金流量帳戶。|  
|*平衡*|此帳戶是結餘帳戶。|  
|*資產*|此帳戶是資產帳戶。|  
|*責任*|此帳戶是負債帳戶。|  
|*統計*|此帳戶是統計帳戶。|  
  
 列舉型別對應至允許的值**AccountType**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.AccountTypes>。  
  
## <a name="see-also"></a>請參閱＜  
 [Accounts 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
