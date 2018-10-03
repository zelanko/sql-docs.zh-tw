---
title: StatusGraphic 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- StatusGraphic Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- StatusGraphic
helpviewer_keywords:
- StatusGraphic element
ms.assetid: 14b365bc-924d-4791-ad4a-a38155fec42e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 98c1b9d076b6ed6981b02b8c4198c330bb0aca53
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190410"
---
# <a name="statusgraphic-element-assl"></a>StatusGraphic 元素 (ASSL)
  包含的狀態的建議圖形表示法[Kpi](../objects/kpi-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Kpi>  
   ...  
   <StatusGraphic>...</StatusGraphic>  
   ...  
</Kpi>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Kpi](../objects/kpi-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*號誌燈-單一*|號誌燈 (單一)|  
|*號誌燈-多個*|號誌燈 (多個)|  
|*道路標誌*|道路標誌|  
|*量測計-遞增*|量測計|  
|*量測計-遞減*|反向量測計|  
|*溫度計*|溫度計|  
|*磁柱*|圓柱|  
|*笑臉*|臉|  
  
 對應至父系的元素`StatusGraphic`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Kpi>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
