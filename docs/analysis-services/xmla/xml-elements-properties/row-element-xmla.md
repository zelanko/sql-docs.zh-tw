---
title: "資料列元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: row Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#row
- microsoft.xml.analysis.row
- http://schemas.microsoft.com/analysisservices/2003/engine#row
helpviewer_keywords: row element
ms.assetid: 4d9977a0-c396-44c7-9fd4-97f4c3d643aa
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2b38517cea700ac5fab6cdccbef77aaeea0dc969
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="row-element-xmla"></a>row 元素 (XMLA)
  包含單一資料列之資料的[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)包含所傳回的表格式資料的項目[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)或[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法呼叫。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <row>  
      <!-- One or more column elements -->  
   </row>  
</root>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)(使用[資料列集](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)資料類型)|  
|子元素|一個或多個資料行元素。|  
  
## <a name="remarks"></a>備註  
 所傳回的每個資料列**根**包含表格式資料的項目都有對應**列**項目。 在每個資料行**根**項目由個別的 XML 項目。 資料行值**列**項目是 XML 項目所包含的資料且資料行的名稱會對應至 XML 項目的名稱。  
  
 有兩種方式可表示資料列中資料行的 Null 值：  
  
-   遺漏的資料行元素表示該資料行為 Null。  
  
-   此資料行元素可能會使用 `xsi:nil='true'` 屬性來表示它具有 Null 值。  
  
 例如，如果資料列具有名為 Store_Name 的單一資料行而且其值為 NULL，它就可以表示成：  
  
```  
<row>  
</row>  
```  
  
 或：  
  
```  
<row>  
   <Store_name xsi:nil='true'/>  
</row>  
```  
  
 如果資料行元素包含錯誤，**錯誤**項目會提供資訊錯誤，如下列範例所述：  
  
```  
<row>   <Store_name>  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception">  
         <ErrorCode>3238658054</ErrorCode>  
         <Description>The object [X] was not found in the cube when [X] was parsed.</Description>  
      </Error>  
   </Store_name>  
</row>  
```  
  
 如需有關命名資料行的資訊和表格式資料的結構描述資訊，請參閱[資料列集資料類型 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md).  
  
## <a name="see-also"></a>請參閱＜  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
