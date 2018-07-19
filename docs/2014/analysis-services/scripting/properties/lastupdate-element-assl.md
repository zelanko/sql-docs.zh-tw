---
title: LastUpdate 元素 (ASSL) |Microsoft Docs
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
- LastUpdate Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- LastUpdate element
ms.assetid: 639db733-a082-4f57-868d-a3bcd5e7a4f6
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 01429b3086f6de62b7ad0b921ad89f042c341891
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37302778"
---
# <a name="lastupdate-element-assl"></a>LastUpdate 元素 (ASSL)
  包含唯讀時間時間戳記，指出上次相關聯[資料庫](../objects/database-element-assl.md)或任何資料庫包含主要物件遭變更。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Database> <!-- or one of the elements that are listed in the Element Relationships table -->  
   ...  
   <LastUpdate>...</LastUpdate>  
   ...  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|DateTime|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[[資料庫]](../objects/database-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應至 `LastUpdate` 父系的元素是 <xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
