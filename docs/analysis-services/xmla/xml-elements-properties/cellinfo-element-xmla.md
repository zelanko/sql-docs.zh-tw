---
title: "CellInfo 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CellInfo Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cellinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#CellInfo
- urn:schemas-microsoft-com:xml-analysis#CellInfo
helpviewer_keywords: CellInfo element
ms.assetid: 8b6420f1-e9a7-4975-b580-1439fa11f5ca
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b2e26f0b4adb6872fed90fcab1a84b2ff83c90a1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="cellinfo-element-xmla"></a>CellInfo 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]表示父系所包含的資料格中繼資料[OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)項目。  
  
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
|父元素|[OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|子元素|一個或多個資料格屬性定義|  
  
## <a name="remarks"></a>備註  
 **CellInfo**元素包含所傳回之多維度資料集內包含的資料格的資料格屬性集合**根**項目使用**MDDataSet**資料型別。 中的每一個資料格屬性**CellInfo**項目由個別的 XML 項目，每個都有定義**名稱**屬性和**類型**屬性。 **名稱**資料格屬性的屬性對應至 OLE DB 的 XML 項目所表示的 OLAP 資料格屬性的名稱和**類型**屬性代表 XML 資料類型的資料格屬性。 XML 項目的名稱用來識別資料格屬性中所包含的資料格的值**CellData**元素**根**項目。  
  
 下列語法將描述資料格屬性定義：  
  
```  
<CellPropertyDefinition name="string" type"string" />  
```  
  
 您可以使用 DISCOVER_PROPERTIES 要求類型搭配 **Discover** 方法來取得可用的屬性及其值。 **PropertyList** 元素中所列的屬性沒有必要的順序。  
  
 提供者可以選擇性地指定個別的成員或資料格屬性中的預設值**AxisInfo**或**CellInfo** > 一節。 如果屬性一律或幾乎一律具有相同的值，預設值可以提供較小的結果。 若要表示屬性的預設值**預設**元素可以選擇性地指定為其中一個資料格屬性定義元素的子元素。 因此，如果成員或資料格屬性不存在結果中，就表示上述預設值為資料格屬性的值。  
  
## <a name="example"></a>範例  
 下列範例會示範如何在呈現的值、 FORMATTED_VALUE 和 FORMAT_STRING 資料格屬性**CellInfo**項目。  
  
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
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
