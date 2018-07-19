---
title: NotificationTechnique 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 23b8d193c3039a9606c0d0a0912829534e9673a3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34042542"
---
# <a name="notificationtechnique-element-assl"></a>NotificationTechnique 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指定是否[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或外部用戶端應用程式會處理通知。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ProactiveCachingBinding>  
   <NotificationTechnique>...</NotificationTechnique>  
</ProactiveCachingBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*用戶端*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*用戶端*|外部用戶端應用程式會處理通知。|  
|*Server*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會處理通知。|  
  
 對應目的父代的項目**NotificationTechnique**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ProactiveCachingBinding>。  
  
 列舉型別對應至允許的值**NotificationTechnique**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.NotificationTechnique>。  
  
## <a name="see-also"></a>另請參閱  
 [ProactiveCachingBinding 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)  
  
  
