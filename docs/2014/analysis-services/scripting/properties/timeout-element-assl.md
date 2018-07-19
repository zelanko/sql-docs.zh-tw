---
title: Timeout 元素 (ASSL) |Microsoft Docs
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
- Timeout Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Timeout
helpviewer_keywords:
- Timeout element
ms.assetid: 7694872b-bd05-459f-b5dc-3cfbd92a9664
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a9069f5ec57d313b89342533d79e66f8c021604e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37269554"
---
# <a name="timeout-element-assl"></a>Timeout 元素 (ASSL)
  指定一段時間 (以秒為單位)，經過這段時間之後，嘗試擷取資料的行為就會回報逾時。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataSource>  
   ...  
   <Timeout>...</Timeout>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|Duration|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataSource](../objects/datasource-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`Timeout`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.DataSource>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
