---
title: AccountType 元素 (ASSL) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5258ff60c8dfafefbf81f87d3538c396c085ccac
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34035179"
---
# <a name="accounttype-element-assl"></a>AccountType 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|Value|Description|  
|-----------|-----------------|  
|*Income*|此帳戶是收入帳戶。|  
|*費用*|此帳戶是支出帳戶。|  
|*流量*|此帳戶是現金流量帳戶。|  
|*結餘*|此帳戶是結餘帳戶。|  
|*資產*|此帳戶是資產帳戶。|  
|*負債*|此帳戶是負債帳戶。|  
|*統計*|此帳戶是統計帳戶。|  
  
 列舉型別對應至允許的值**AccountType**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.AccountTypes>。  
  
## <a name="see-also"></a>另請參閱  
 [帳戶項目&#40;ASSL&#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
