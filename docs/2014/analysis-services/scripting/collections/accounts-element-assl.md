---
title: 帳戶元素 (ASSL) |Microsoft Docs
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
- Accounts Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Accounts
helpviewer_keywords:
- Accounts element
ms.assetid: 3ec62f58-c19b-4b15-b040-8941521a389b
caps.latest.revision: 44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 94e167c6eb804f3372fab6974403f0303f21a13a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277964"
---
# <a name="accounts-element-assl"></a>Accounts 元素 (ASSL)
  包含帳戶類型中所定義的集合[資料庫](../objects/database-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Database>  
   ...  
   <Accounts>  
      <Account>...</Account>  
   </Accounts>  
   ...  
</Database>  
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
|父元素|[[資料庫]](../objects/database-element-assl.md)|  
|子元素|[帳戶](../objects/account-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 維度，其[型別](../properties/type-element-dimension-assl.md)元素設定為*帳戶*、 可以有屬性，指定帳戶類型，例如 Income、 Expense 等等，由維度中的成員。 然後會使用帳戶類型[量值](../objects/measure-element-assl.md)項目，其[AggregationFunction](../properties/aggregatefunction-element-assl.md)元素設定為*ByAccount*，以決定時要使用的彙總函式彙總該維度成員。 `Accounts` 元素會保存 `Account` 元素的集合，代表帳戶類型以及應該用於每種帳戶類型的彙總函式。  
  
 如果彙總函式所使用的預設值不同，就必須列出帳戶類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]每一個帳戶類型。  
  
 有效的帳戶類型集合是固定的。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.AccountCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [AccountType 元素&#40;ASSL&#41;](../properties/accounttype-element-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
