---
title: HierarchyInfo 元素 (XMLA) |Microsoft Docs
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
- HierarchyInfo Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#HierarchyInfo
- microsoft.xml.analysis.hierarchyinfo
- urn:schemas-microsoft-com:xml-analysis#HierarchyInfo
helpviewer_keywords:
- HierarchyInfo element
ms.assetid: b4472251-1f1d-4233-a8e6-407397862ab4
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ff2da32b09833d425f49f47769a98d01e888264a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180799"
---
# <a name="hierarchyinfo-element-xmla"></a>HierarchyInfo 元素 (XMLA)
  表示父代所包含的單一階層[AxisInfo](axisinfo-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AxisInfo>  
   ...  
   <HierarchyInfo name="string">  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </HierarchyInfo>  
   ...  
</AxisInfo>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AxisInfo](axisinfo-element-xmla.md)|  
|子元素|[Caption](caption-element-xmla.md)， [DisplayInfo](displayinfo-element-xmla.md)， [LName](name-element-xmla.md)， [LNum](lnum-element-xmla.md)， [UName](uname-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|名稱|所需`String`屬性。 階層的名稱。|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
