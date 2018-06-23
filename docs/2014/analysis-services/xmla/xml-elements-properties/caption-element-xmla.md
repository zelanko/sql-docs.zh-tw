---
title: 標題元素 (XMLA) |Microsoft 文件
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
- Caption Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Caption
- http://schemas.microsoft.com/analysisservices/2003/engine#Caption
- microsoft.xml.analysis.caption
helpviewer_keywords:
- Caption element
ms.assetid: 3d10ee68-98ab-4da0-a409-800dea2f1c32
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 9a67a57b29bf014326848b49e40bdbe5bc283dd1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032165"
---
# <a name="caption-element-xmla"></a>Caption 元素 (XMLA)
  包含父代的標題資訊[HierarchyInfo](hierarchyinfo-element-xmla.md)或[成員](member-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <Caption>...</Caption>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[HierarchyInfo](hierarchyinfo-element-xmla.md)，[成員](member-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 若為 `HierarchyInfo` 元素，`Caption` 元素就會包含提供階層之成員標題的屬性名稱。 此值相當於針對 OLE DB for OLAP 規格中軸資料列集定義的 MEMBER_CAPTION 屬性。  
  
 若為 `Member` 元素，`Caption` 元素就會以針對 XML for Analysis (XMLA) 工作階段指定的語言包含 `Member` 父元素的標題。 如果沒有任何標題可用，這個元素就會包含成員的唯一名稱。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  