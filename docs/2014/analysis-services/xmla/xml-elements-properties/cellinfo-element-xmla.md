---
title: CellInfo 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CellInfo Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cellinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#CellInfo
- urn:schemas-microsoft-com:xml-analysis#CellInfo
helpviewer_keywords:
- CellInfo element
ms.assetid: 8b6420f1-e9a7-4975-b580-1439fa11f5ca
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fda3576bb50314c28dd01474e576ff2b5b333cb8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37176385"
---
# <a name="cellinfo-element-xmla"></a>CellInfo 元素 (XMLA)
  表示父元素所包含的資料格中繼資料[OlapInfo](olapinfo-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<OlapInfo>  
   ...  
   <CellInfo>  
      <!-- One or more cell property definitions -->  
   </CellInfo>  
   ...  
</OlapInfo>  
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
|父元素|[OlapInfo](olapinfo-element-xmla.md)|  
|子元素|一個或多個資料格屬性定義|  
  
## <a name="remarks"></a>備註  
 `CellInfo` 元素包含使用 `root` 資料類型由 `MDDataSet` 元素傳回之多維度資料集內包含的資料格的資料格屬性集合。 `CellInfo` 元素中的每個資料格屬性 (Property) 都由個別的 XML 元素所定義，而且每個元素都具有 `name` 屬性 (Attribute) 和 `type` 屬性 (Attribute)。 資料格屬性 (Property) 的 `name` 屬性 (Attribute) 會對應至 XML 元素所代表之 OLE DB for OLAP 資料格屬性 (Property) 的名稱，而且 `type` 屬性 (Attribute) 會代表資料格屬性 (Property) 的 XML 資料類型。 XML 元素的名稱可用來識別 `CellData` 元素之 `root` 元素中所包含之資料格的資料格屬性值。  
  
 下列語法將描述資料格屬性定義：  
  
```  
<CellPropertyDefinition name="string" type"string" />  
```  
  
 可用的屬性和其值可以使用 DISCOVER_PROPERTIES 要求類型，搭配取得`Discover`方法。 `PropertyList` 元素中所列的屬性沒有必要的順序。  
  
 提供者可以選擇性地針對 `AxisInfo` 或 `CellInfo` 區段中的個別成員或資料格屬性指定預設值。 如果屬性一律或幾乎一律具有相同的值，預設值可以提供較小的結果。 若要表示屬性的預設值`Default`元素可以選擇性地指定為其中一個資料格屬性定義元素的子項目。 因此，如果成員或資料格屬性不存在結果中，就表示上述預設值為資料格屬性的值。  
  
## <a name="example"></a>範例  
 下列範例將示範如何在 `CellInfo` 元素中表示 VALUE、FORMATTED_VALUE 和 FORMAT_STRING 資料格屬性。  
  
```  
<OlapInfo>  
   ...  
      <CellInfo>  
         <Value name="VALUE"></Value>  
         <FmtValue name="FORMATTED_VALUE"></FmtValue>  
         <FormatString name="FORMAT_STRING"></FormatString>  
      </CellInfo>  
</OlapInfo>  
```  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
