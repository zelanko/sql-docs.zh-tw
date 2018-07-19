---
title: OlapInfo 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- OlapInfo Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#OlapInfo
- microsoft.xml.analysis.olapinfo
- urn:schemas-microsoft-com:xml-analysis#OlapInfo
- OLAPInfo
helpviewer_keywords:
- OlapInfo element
ms.assetid: 8828fdd7-c0f7-48ce-a0d0-ab4bc1a995cf
caps.latest.revision: 27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0d1665a174cdff0d4afcd8bea69b9bdca9212d9d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37178385"
---
# <a name="olapinfo-element-xmla"></a>OlapInfo 元素 (XMLA)
  包含所包含的軸和資料格中繼資料[根](root-element-xmla.md)使用的項目[MDDataSet](../xml-data-types/mddataset-data-type-xmla.md)資料型別。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[根目錄](root-element-xmla.md)|  
|子元素|[AxesInfo](axesinfo-element-xmla.md)， [CellInfo](cellinfo-element-xmla.md)， [CubeInfo](cubeinfo-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 使用 `OLAPInfo` 資料類型之 `root` 元素的 `MDDataSet` 區段會提供 Cube、多維度結果的軸，以及包含結果之資料格的屬性的相關中繼資料。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
