---
title: "OlapInfo 元素 (XMLA) |Microsoft 文件"
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
- OlapInfo Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#OlapInfo
- microsoft.xml.analysis.olapinfo
- urn:schemas-microsoft-com:xml-analysis#OlapInfo
- OLAPInfo
helpviewer_keywords:
- OlapInfo element
ms.assetid: 8828fdd7-c0f7-48ce-a0d0-ab4bc1a995cf
caps.latest.revision: 27
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e52aed18729c213c1084c8d0943725f3d390ce4b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="olapinfo-element-xmla"></a>OlapInfo 元素 (XMLA)
  包含所包含的軸和資料格中繼資料[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)項目，會使用[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)資料型別。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <OlapInfo>  
      <CubeInfo>...</CubeInfo>  
      <AxesInfo>...</AxesInfo>  
      <CellInfo>...</CellInfo>  
   </OlapInfo>  
   ...  
</root>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|子元素|[AxesInfo](../../../analysis-services/xmla/xml-elements-properties/axesinfo-element-xmla.md)， [CellInfo](../../../analysis-services/xmla/xml-elements-properties/cellinfo-element-xmla.md)， [CubeInfo](../../../analysis-services/xmla/xml-elements-properties/cubeinfo-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **OLAPInfo**區段**根**項目使用**MDDataSet**資料類型會提供有關 cube 的中繼資料、 多維度結果，以及屬性軸資料格包含結果。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

