---
title: "PropertyList 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
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
apiname: PropertyList Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#PropertyList
- microsoft.xml.analysis.propertylist
- urn:schemas-microsoft-com:xml-analysis#PropertyList
helpviewer_keywords: PropertyList element
ms.assetid: 58e63bd9-8aac-438d-adba-1868b4d123f5
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cc793c573a9044ba4dc711cb8912c589e076ac13
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="propertylist-element-xmla"></a>PropertyList 元素 (XMLA)
  包含的 XML for Analysis (XMLA) 所用的屬性集合[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)和[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Properties>  
   <PropertyList>  
      <!-- Zero or more XMLA properties -->  
   </PropertyList>  
</Properties>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[屬性](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)|  
|子元素|XMLA 屬性 (請參閱「備註」)|  
  
## <a name="remarks"></a>備註  
 **PropertyList** 元素包含 XMLA 屬性的集合。 每個屬性都可讓使用者控制 **Discover** 或 **Execute** 方法的某些層面，例如定義連接至資料來源所需的資訊、指定結果集的傳回格式，或指定資料格式化應該採用的地區設定。 **PropertyList** 元素中的每個 XMLA 屬性都由不同的 XML 元素所定義。 XMLA 屬性的值是 XML 元素所包含的資料，而 XMLA 屬性的名稱會對應至 XML 元素的名稱。  
  
 您可以使用 DISCOVER_PROPERTIES 要求類型搭配 **Discover** 方法來取得可用的屬性及其值。 **PropertyList** 元素中所列的屬性沒有必要的順序。  
  
 如需有關所支援之 XMLA 屬性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，請參閱[支援 XMLA 屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
## <a name="example"></a>範例  
  
```  
<Properties>  
   <PropertyList>  
      <DataSourceInfo>  
         Provider=MSOLAP;Data Source=local;  
      </DataSourceInfo>  
      <Catalog>  
         Foodmart 2000  
      </Catalog>  
      <Format>  
         Multidimensional  
      </Format>  
   </PropertyList>  
</Properties>  
```  
  
## <a name="see-also"></a>請參閱＜  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
