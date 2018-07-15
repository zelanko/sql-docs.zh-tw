---
title: LNum 元素 (XMLA) |Microsoft Docs
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
- LNum Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.lnum
- urn:schemas-microsoft-com:xml-analysis#LNum
- http://schemas.microsoft.com/analysisservices/2003/engine#LNum
helpviewer_keywords:
- LNum element
ms.assetid: 7b9cc143-0c5e-4a8c-a288-8921bfcfd103
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e19f8f362fad80ce7940eccb59d8170b393abc28
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306098"
---
# <a name="lnum-element-xmla"></a>LNum 元素 (XMLA)
  包含父層級序數位置的相關資訊[HierarchyInfo](hierarchyinfo-element-xmla.md)或是[成員](member-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <LNum>...</LNum>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|ssNoversion|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[HierarchyInfo](hierarchyinfo-element-xmla.md)，[成員](member-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 若為 `HierarchyInfo` 元素，`LNum` 元素就會包含提供階層之層級序數位置的屬性名稱。 此值相當於針對 OLE DB for OLAP 規格中軸資料列集定義的 LEVEL_NUMBER 屬性。  
  
 針對`Member`項目，`LNum`項目包含以零為起始的序數位置，在階層的根層級從父元素所代表之成員[成員](member-element-xmla.md)項目。 值為零代表階層的根層級。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
