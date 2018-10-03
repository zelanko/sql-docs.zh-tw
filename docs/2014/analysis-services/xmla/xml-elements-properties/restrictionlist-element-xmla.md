---
title: RestrictionList 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- RestrictionList Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#RestrictionList
- microsoft.xml.analysis.restrictionlist
- http://schemas.microsoft.com/analysisservices/2003/engine#RestrictionList
helpviewer_keywords:
- RestrictionList element
ms.assetid: 2297c005-381e-49a4-a207-826f7f9ea93a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cad57213c69c63dbc45e476d0163a46c111bc8a9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48067948"
---
# <a name="restrictionlist-element-xmla"></a>RestrictionList 元素 (XMLA)
  包含 [Discover](../xml-elements-methods-discover.md) 方法所使用之限制資料行和值的集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Restrictions>  
   <RestrictionList>  
      <!-- Zero or more restriction columns and values -->  
   </RestrictionList>  
</Restrictions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[限制](restrictions-element-xmla.md)|  
|子元素|限制資料行和值 (請參閱「備註」)。|  
  
## <a name="remarks"></a>備註  
 `RestrictionList` 元素包含可用來篩選 `Discover` 方法所傳回之資料的限制資料行集合。 `RestrictionList` 元素中的每個限制資料行都由不同的 XML 元素所定義。 限制資料行的值是 XML 元素所包含的資料，而限制資料行的名稱會對應至 XML 元素的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
