---
title: Discover 方法 (XMLA) |Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 921afc6d17a0eddcba48e5a6a6064810a3b3b6ef
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979100"
---
# <a name="xml-elements---methods---discover"></a>XML 元素-方法-探索
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  從 Analysis Services 的執行個體中擷取資訊，例如可用的資料庫或有關特定物件的詳細資料的清單。 使用擷取的資料**探索**方法取決於傳遞給它的參數值。  
  
 **命名空間**urn: schemas-microsoft-microsoft-schemas-microsoft-com:-分析  
  
 **SOAP 動作**"urn: schemas-microsoft-microsoft-schemas-microsoft-com:-分析： 探索 」  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Discover>  
   <RequestType>...</RequestType>  
   <Restrictions>...</Restrictions>  
   <Properties>...</Properties>  
</Discover>  
```  
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[屬性](../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)， [RequestType](../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)，[限制](../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **探索**方法會要求有關執行個體和物件的中繼資料。 傳回中繼資料是使用 XMLA[資料列集](../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)資料型別。  
 
> [!TIP] 
> 如果您不熟悉 XML 命令，按一下 上 XMLA 查詢範本**查詢**在 Management Studio 的 建立查詢，並將參數加入至工具列。 如需詳細資訊，請參閱 [在 SQL Server Management Studio 中使用 Analysis Services 範本](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)。 
  
## <a name="example"></a>範例  
 在下列程式碼範例中，用戶端會傳送**Discover**要求一份 cube 與呼叫[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]範例 Analysis Services 資料庫：  
  
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
 [XML 資料型別&#40;XMLA&#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Execute 方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)   
 [方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods.md)   
 [XML 項目&#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Analysis Services 結構描述資料列集](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
