---
title: CubeID 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CubeID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cubeid
- urn:schemas-microsoft-com:xml-analysis#CubeID
- http://schemas.microsoft.com/analysisservices/2003/engine#CubeID
helpviewer_keywords:
- CubeID element
ms.assetid: 9dba605a-c45e-4730-827b-b7c55c8110da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e7f70759df30cc3a8ee568456ca3225cbcfda207
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116204"
---
# <a name="cubeid-element-xmla"></a>CubeID 元素 (XMLA)
  識別父元素中包含物件參考的 Cube。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Object> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <CubeID>...</CubeID>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
  
## <a name="cardinality"></a>基數  
  
|上階或父系|基數|  
|------------------------|-----------------|  
|[Source](source-element-xmla.md)|1-1：只出現一次的必要元素。|  
|[Target](../xml-elements-properties/target-element-xmla.md)|1-1：只出現一次的必要元素。|  
|All others|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Object](object-element-xmla.md)、[ParentObject](parentobject-element-xmla.md)、[Source](source-element-xmla.md)、[Target](../xml-elements-properties/target-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
