---
title: OnlineMode 元素 (ASSL) |Microsoft 文件
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
- OnlineMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- OnlineMode
helpviewer_keywords:
- OnlineMode element
ms.assetid: 0bbac4e2-002f-4be4-8dd6-ccd7034f5f93
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3efda242b0563f4b6b853d3bf87b831da1ea8e00
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145482"
---
# <a name="onlinemode-element-assl"></a>OnlineMode 元素 (ASSL)
  指定資料庫會在起始快取的重建作業時立即返回線上狀態，還是只有在快取的重建作業完成時才返回線上狀態。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <OnlineMode>...</OnlineMode>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*即時運算*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*即時運算*|資料庫會在起始快取的重建作業時立即返回線上狀態。|  
|*OnCacheComplete*|只有在快取的重建作業完成時，資料庫才會返回線上狀態。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `OnlineMode` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ProactiveCaching>。  
  
## <a name="see-also"></a>另請參閱  
 [ProactiveCaching 元素&#40;ASSL&#41;](../objects/proactivecaching-element-assl.md)  
  
  