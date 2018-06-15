---
title: OrderBy 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2d2c8caf392e5d80d82b06a7d7fd9b5cd724a35e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34038512"
---
# <a name="orderby-element-assl"></a>OrderBy 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
