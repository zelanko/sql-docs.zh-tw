---
title: "帳戶元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
apiname:
- Account Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Account
helpviewer_keywords:
- Account element
ms.assetid: 0bb7d06c-0158-4ab2-b2b1-cb50ba24f7c0
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7a8e821817e523d518410c70028fd3a34a18e442
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="account-element-assl"></a>Account 元素 (ASSL)
  包含內部帳戶類型的詳細[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。  
  
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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[帳戶](../../../analysis-services/scripting/collections/accounts-element-assl.md)|  
|子元素|[AccountType](../../../analysis-services/scripting/properties/accounttype-element-assl.md)， [AggregationFunction](../../../analysis-services/scripting/properties/aggregationfunction-element-assl.md)，[別名](../../../analysis-services/scripting/collections/aliases-element-assl.md)，[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 維度，其[類型](../../../analysis-services/scripting/properties/type-element-dimension-assl.md)元素設定為*帳戶*可以在維度中有由成員之指定帳戶類型，例如 Income、 Expense 等等，表示屬性。 接著會使用帳戶類型[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)項目，其[AggregationFunction](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md)元素設定為*ByAccount*，以決定時要使用的彙總函式彙總該維度成員。 **帳戶**元素代表單一帳戶類型以及應該使用這類量值的彙總函式。  
  
 如果彙總函式所使用的預設值不同，就必須列出帳戶類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]每一個帳戶類型。  
  
 有效的帳戶類型集合是固定的。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Account>。  
  
## <a name="see-also"></a>另請參閱  
 [Database 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

