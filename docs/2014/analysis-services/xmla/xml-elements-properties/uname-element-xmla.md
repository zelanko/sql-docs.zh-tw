---
title: UName 元素 (XMLA) |Microsoft Docs
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
- UName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#UName
- urn:schemas-microsoft-com:xml-analysis#UName
- microsoft.xml.analysis.uname
helpviewer_keywords:
- UName element
ms.assetid: b4916d44-cf77-4d4c-b4e5-a0a98192d057
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fa8df2d964db3c8131b9566e04b05c106638d62e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185125"
---
# <a name="uname-element-xmla"></a>UName 元素 (XMLA)
  包含唯一的名稱之父代[HierarchyInfo](hierarchyinfo-element-xmla.md)或是[成員](member-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <UName>...</UName>  
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
 若為 `HierarchyInfo` 元素，`UName` 元素就會包含提供階層之唯一成員名稱的屬性名稱。 此值相當於針對 OLE DB for OLAP 規格中軸資料列集定義的 MEMBER_UNIQUE_NAME 屬性。  
  
 若為 `Member` 元素，`UName` 元素就會包含 `Member` 父元素的唯一名稱。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
