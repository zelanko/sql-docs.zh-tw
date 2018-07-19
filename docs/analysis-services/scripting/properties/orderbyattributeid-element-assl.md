---
title: OrderByAttributeID 元素 (ASSL) |Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2e6ab7a00961d4e5b925556d107eec32b7ddb9c9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38018212"
---
# <a name="orderbyattributeid-element-assl"></a>OrderByAttributeID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  識別排序的成員所依據的另一個屬性[維度](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)屬性。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <OrderByAttributeID>...</OrderByAttributeID>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **OrderByAttributeID**項目時才會使用值[OrderBy](../../../analysis-services/scripting/properties/orderby-element-assl.md)項目**DimensionAttribute**設為*AttributeKey*或是*AttributeName*。  
  
 對應至父系的元素**OrderByAttributeID**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
