---
title: "OrderBy 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- OrderBy Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- OrderBy
helpviewer_keywords:
- OrderBy element
ms.assetid: d7a0564b-430e-44eb-913a-fe1f98917d0f
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 35479ebb898200c9082a7e08369a3ae5d4c57ac3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="orderby-element-assl"></a>OrderBy 元素 (ASSL)
  描述如何排序屬性中包含的成員。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <OrderBy>...</OrderBy>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*名稱*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*名稱*|依據成員名稱來進行排序。|  
|*索引鍵*|依據成員索引鍵來進行排序。|  
|*AttributeKey*|Order by 中指定的屬性成員索引鍵的[OrderByAttributeID](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md)元素**DimensionAttribute**。|  
|*AttributeName*|Order by 中指定的屬性的成員名稱的**OrderByAttributeID**元素**DimensionAttribute**。|  
  
 列舉型別對應至允許的值**OrderBy**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.OrderBy>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

