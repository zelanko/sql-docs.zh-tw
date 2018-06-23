---
title: 帳戶元素 (ASSL) |Microsoft 文件
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
- Account Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Account
helpviewer_keywords:
- Account element
ms.assetid: 0bb7d06c-0158-4ab2-b2b1-cb50ba24f7c0
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0a99dbaee6e1eaec95385295cf1842ffcc336adf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145485"
---
# <a name="account-element-assl"></a>Account 元素 (ASSL)
  包含內部帳戶類型的詳細[資料庫](database-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Accounts>  
   <Account>  
      <AccountType>...</AccountType>  
      <AggregationFunction>...</AggregationFunction>  
            <Aliases>...</Aliases>  
            <Annotations>...</Annotations>  
   </Account>  
</Accounts>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[帳戶](../collections/accounts-element-assl.md)|  
|子元素|[AccountType](../properties/accounttype-element-assl.md)， [AggregationFunction](../properties/aggregationfunction-element-assl.md)，[別名](../collections/aliases-element-assl.md)，[註解](../collections/annotations-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 維度，其[類型](../properties/type-element-dimension-assl.md)元素設定為*帳戶*可以在維度中有由成員之指定帳戶類型，例如 Income、 Expense 等等，表示屬性。 接著會使用帳戶類型[量值](measure-element-assl.md)項目，其[AggregationFunction](../properties/aggregatefunction-element-assl.md)元素設定為*ByAccount*，以決定時要使用的彙總函式彙總該維度成員。 `Account` 元素代表單一帳戶類型以及這類量值應該使用的彙總函式。  
  
 如果彙總函式所使用的預設值不同，就必須列出帳戶類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]每一個帳戶類型。  
  
 有效的帳戶類型集合是固定的。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Account>。  
  
## <a name="see-also"></a>另請參閱  
 [Database 元素&#40;ASSL&#41;](database-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  