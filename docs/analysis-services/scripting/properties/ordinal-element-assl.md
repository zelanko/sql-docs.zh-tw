---
title: Ordinal 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 88c2409d42fc23f017989218d8ea87172d1b8d3d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="ordinal-element-assl"></a>Ordinal 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指出索引鍵和翻譯等集合中要繫結的目標序號。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AttributeBinding> <!-- or CubeAttributeBinding -->  
   ...  
   <Ordinal>...</Ordinal>  
   ...  
</AttributeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|Integer|  
|預設值|**0**|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **AttributeBinding**和**CubeAttributeBinding**所在的項目[類型](../../../analysis-services/scripting/properties/type-element-binding-assl.md)屬性會設為*金鑰*或*轉譯*可繫結的屬性，會接著繫結至資料來源檢視中的資料行的集合。 值**序數**元素會決定哪一個資料行**AttributeBinding**或**CubeAttributeBinding**是指在該集合中。  
  
 對應至父系的項目**序數**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.AttributeBinding>和<xref:Microsoft.AnalysisServices.CubeAttributeBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
