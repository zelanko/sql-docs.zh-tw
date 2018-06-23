---
title: 資料列元素 (XMLA) |Microsoft 文件
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
- row Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#row
- microsoft.xml.analysis.row
- http://schemas.microsoft.com/analysisservices/2003/engine#row
helpviewer_keywords:
- row element
ms.assetid: 4d9977a0-c396-44c7-9fd4-97f4c3d643aa
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: de6460bc6d51c4205752b7db186412e420438145
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033336"
---
# <a name="row-element-xmla"></a>row 元素 (XMLA)
  包含單一資料列之資料的[根](root-element-xmla.md)包含所傳回的表格式資料的項目[探索](../xml-elements-methods-discover.md)或[Execute](../xml-elements-methods-execute.md)方法呼叫。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <row>  
      <!-- One or more column elements -->  
   </row>  
</root>  
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
|父元素|[根](root-element-xmla.md)(使用[資料列集](../xml-data-types/rowset-data-type-xmla.md)資料類型)|  
|子元素|一個或多個資料行元素。|  
  
## <a name="remarks"></a>備註  
 包含表格式資料之 `root` 元素所傳回的每個資料列都具有對應的 `row` 元素。 `root` 元素中的每個資料行都由個別的 XML 元素表示。 `row` 元素之資料行的值是 XML 元素所包含的資料，而此資料行的名稱會對應至 XML 元素的名稱。  
  
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
  
 如果資料行元素包含錯誤，`Error` 元素就會提供錯誤的相關資訊，如下列範例所述：  
  
```  
<row>   <Store_name>  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception">  
         <ErrorCode>3238658054</ErrorCode>  
         <Description>The object [X] was not found in the cube when [X] was parsed.</Description>  
      </Error>  
   </Store_name>  
</row>  
```  
  
 如需有關命名資料行的資訊和表格式資料的結構描述資訊，請參閱[資料列集的資料型別&#40;XMLA&#41;](../xml-data-types/rowset-data-type-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  