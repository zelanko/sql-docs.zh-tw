---
title: "Discover 方法 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 09/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Discover Method
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#
- http://schemas.microsoft.com/analysisservices/2003/engine#
- microsoft.xml.analysis.discover
- urn:schemas-microsoft-com:xml-analysis#Discover
- Discover
helpviewer_keywords:
- Discover method
ms.assetid: 0eb52d88-c081-416e-a229-610e4373b0b3
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 60a101afa2953d62e2910b4523a0213e4e786490
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="xml-elements---methods---discover"></a>XML 項目-方法-探索
  擷取執行個體中的資訊，例如可用的資料庫或有關特定物件的詳細資料清單[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 與擷取的資料**探索**方法取決於參數傳遞給它的值。  
  
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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[屬性](../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)， [RequestType](../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)，[限制](../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **探索**方法會要求有關的中繼資料[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體和物件。 使用 XMLA 來傳回中繼資料[資料列集](../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)資料型別。  
 
> [!TIP] 
> 如果您不熟悉 XML 命令，請按一下 XMLA 查詢範本**查詢**在 Management Studio，來建立查詢，以及將參數加入工具列。 如需詳細資訊，請參閱 [在 SQL Server Management Studio 中使用 Analysis Services 範本](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)。 
  
## <a name="example"></a>範例  
 在下列程式碼範例中，用戶端會傳送**探索**要求一份 cube 與呼叫[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]範例[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫：  
  
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
 [XML 資料類型 &#40;XMLA &#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [執行方法 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)   
 [方法 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-methods.md)   
 [XML 項目 &#40;XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Analysis Services 結構描述資料列集](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  

