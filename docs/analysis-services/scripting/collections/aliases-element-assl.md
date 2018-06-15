---
title: Aliases 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fb37f0a7393b6055621e9575aef3c20a50313ff9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032399"
---
# <a name="aliases-element-assl"></a>Aliases 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含集合[別名](../../../analysis-services/scripting/properties/alias-element-assl.md)與相關聯的項目[帳戶](../../../analysis-services/scripting/objects/account-element-assl.md)項目  
  
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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無 (集合)|  
|預設值|無 (集合)|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[帳戶](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|子元素|[別名](../../../analysis-services/scripting/properties/alias-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目**別名**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Account>。  
  
## <a name="see-also"></a>另請參閱  
 [帳戶項目&#40;ASSL&#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [Database 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [集合 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
