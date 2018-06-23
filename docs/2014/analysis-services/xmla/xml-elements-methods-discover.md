---
title: Discover 方法 (XMLA) |Microsoft 文件
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
- Discover Method
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#
- http://schemas.microsoft.com/analysisservices/2003/engine#
- microsoft.xml.analysis.discover
- urn:schemas-microsoft-com:xml-analysis#Discover
- Discover
helpviewer_keywords:
- Discover method
ms.assetid: 0eb52d88-c081-416e-a229-610e4373b0b3
caps.latest.revision: 36
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: ead875bbe88ea71c8741450f8a3127efcf4b313d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132281"
---
# <a name="discover-method-xmla"></a>Discover 方法 (XMLA)
  擷取執行個體中的資訊，例如可用的資料庫或有關特定物件的詳細資料清單[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 使用 `Discover` 方法所擷取的資料取決於傳遞給它的參數值。  
  
 **命名空間**描述 urn:-microsoft-schemas-microsoft-com:-分析  
  
 **SOAP 動作**」 描述 urn:-microsoft-schemas-microsoft-com:-分析： 探索 」  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Discover>  
   <RequestType>...</RequestType>  
   <Restrictions>...</Restrictions>  
   <Properties>...</Properties>  
</Discover>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[屬性](xml-elements-properties/properties-element-xmla.md)， [RequestType](xml-elements-properties/type-element-xmla.md)，[限制](xml-elements-properties/restrictions-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Discover` 方法會要求有關 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體和物件的中繼資料。 使用 XMLA 來傳回中繼資料[資料列集](xml-data-types/rowset-data-type-xmla.md)資料型別。  
  
## <a name="example"></a>範例  
 在下列程式碼範例中，用戶端會傳送 `Discover` 呼叫，以便從 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 範例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中要求 Cube 清單。  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>MDSCHEMA_CUBES</RequestType>  
   <Restrictions>  
      <RestrictionList>  
         <CATALOG_NAME>Adventure Works DW Multidimensional 2012</CATALOG_NAME>  
      </RestrictionList>  
   </Restrictions>  
   <Properties>  
      <PropertyList>  
         <DataSourceInfo>Provider=MSOLAP;Data Source=local;</DataSourceInfo>  
         <Catalog>Adventure Works DW Multidimensional 2012</Catalog>  
         <Format>Tabular</Format>  
      </PropertyList>  
   </Properties>  
</Discover>  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料型別&#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [Execute 方法&#40;XMLA&#41;](xml-elements-methods-execute.md)   
 [方法&#40;XMLA&#41;](xml-elements-methods.md)   
 [XML 項目&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [Analysis Services 結構描述資料列集](../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  