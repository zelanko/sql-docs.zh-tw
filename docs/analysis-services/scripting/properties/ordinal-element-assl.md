---
title: "Ordinal 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Ordinal Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Ordinal
helpviewer_keywords:
- Ordinal element
ms.assetid: 64e68ad5-439c-4c1d-9df4-ee90c56761b4
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f82b14a571fad0753e3b8835a3e0829a4975c583
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="ordinal-element-assl"></a>Ordinal 元素 (ASSL)
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
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

