---
title: Ordinal 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Ordinal Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Ordinal
helpviewer_keywords:
- Ordinal element
ms.assetid: 64e68ad5-439c-4c1d-9df4-ee90c56761b4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 87957fdfa3adf85081c0a2ca6a6539917b9f9b81
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198738"
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|Integer|  
|預設值|`0`|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributeBinding](../data-type/binding-data-type-assl.md)， [CubeAttributeBinding](../data-type/cubeattributebinding-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `AttributeBinding` 並`CubeAttributeBinding`所在的項目[型別](type-element-binding-assl.md)屬性會設為*金鑰*或*轉譯*可以繫結至屬性接著會繫結至的集合資料行中的資料來源檢視。 `Ordinal` 元素的值會決定 `AttributeBinding` 或 `CubeAttributeBinding` 在該集合中所參考的資料行。  
  
 對應至父系的元素`Ordinal`在 「 分析管理物件 (AMO) 物件模型所<xref:Microsoft.AnalysisServices.AttributeBinding>和<xref:Microsoft.AnalysisServices.CubeAttributeBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
