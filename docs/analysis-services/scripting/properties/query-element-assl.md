---
title: 查詢元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ceda2f1af0cacd96375fcc6b51f15ff012a8a46e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="query-element-assl"></a>Query 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含要針對通知執行之查詢的文字。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<QueryNotification>  
   <Query>...</Query>  
</QueryNotification>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**查詢**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.QueryNotification>。  
  
## <a name="see-also"></a>另請參閱  
 [ProactiveCachingQueryBinding 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
