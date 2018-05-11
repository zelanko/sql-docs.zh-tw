---
title: 資料列元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 78745ed581642092c17190c4b81eb3f9ab6df853
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="row-element-xmla"></a>row 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
 如需有關命名資料行的資訊和表格式資料的結構描述資訊，請參閱[資料列集資料類型 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md).  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
