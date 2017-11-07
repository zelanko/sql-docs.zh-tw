---
title: "標題元素 (XMLA) |Microsoft 文件"
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
- Caption Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Caption
- http://schemas.microsoft.com/analysisservices/2003/engine#Caption
- microsoft.xml.analysis.caption
helpviewer_keywords:
- Caption element
ms.assetid: 3d10ee68-98ab-4da0-a409-800dea2f1c32
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b2b9ece977da21b4e08124ca12cfafb1a7895f19
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="caption-element-xmla"></a>Caption 元素 (XMLA)
  包含父代的標題資訊[HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md)或[成員](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <Caption>...</Caption>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md)，[成員](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如**HierarchyInfo**項目，**標題**元素包含提供階層的標題的成員屬性的名稱。 此值相當於針對 OLE DB for OLAP 規格中軸資料列集定義的 MEMBER_CAPTION 屬性。  
  
 如**成員**項目，**標題**項目包含標題的父代**成員**中指定的 xml for Analysis (XMLA) 工作階段的語言項目。 如果沒有任何標題可用，這個元素就會包含成員的唯一名稱。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

