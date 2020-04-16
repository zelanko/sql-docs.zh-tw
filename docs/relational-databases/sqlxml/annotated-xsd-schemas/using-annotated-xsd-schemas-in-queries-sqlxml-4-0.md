---
title: 在查詢 (SQLXML) 中使用註解的 XSD 架構
description: 瞭解如何針對 SQLXML 4.0 中的帶註釋的 XSD 架構指定 XPath 查詢,以便從資料庫中檢索數據。
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML]
- inline schemas [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- queries [SQLXML], annotated XSD schemas
- retrieving data
- mapping schema [SQLXML], queries
- multiple inline schemas
- annotated XSD schemas, queries
- XSD schemas [SQLXML], queries
- templates [SQLXML], annotated XSD schemas in queries
ms.assetid: 927a30a2-eae8-420d-851d-551c5f884f3c
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e9ecd9d65d0f70f7c25328c15bb886ca52122de2
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388686"
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>在查詢中使用註解式 XSD 結構描述 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  您可以針對 XSD 結構描述指定範本中的 XPath 查詢，藉以針對註解式結構描述指定查詢來擷取資料庫中的資料。  
  
 sql:xpath 查詢>元素允許您根據由註釋的架構定義的 XML 檢視指定 XPath 查詢。 ** \< ** 使用**\<sql:xpath**查詢>元素的**映射架構**屬性標識要執行 XPath 查詢的註釋架構。  
  
 範本是包含一或多個查詢的有效 XML 文件。 FOR XML 和 XPath 查詢會傳回文件片段。 範本對於文件片段就像是容器一樣；因此，範本會提供一種方式來指定單一的上層元素。  
  
 本主題中的範例會使用範本，針對註解式結構描述指定 XPath 查詢來擷取資料庫中的資料。  
  
 例如，請考慮下列註解式結構描述：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact" >  
     <xsd:complexType>  
       <xsd:attribute name="ContactID" type="xsd:string" />   
       <xsd:attribute name="FirstName" type="xsd:string" />   
       <xsd:attribute name="LastName"  type="xsd:string" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 基於圖解用途，此 XSD 結構描述會以檔案名稱 Schema2.xml 儲存。 接著，您可以針對註解式結構描述，在下列範本檔 (Schema2T.xml) 中指定 XPath 查詢：  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql"  
     >  
          Person.Contact[@ContactID="1"]  
</sql:xpath-query>  
```  
  
 然後，您可以建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs)，將查詢當做範本檔的一部分執行。 有關詳細資訊,請參閱在[SQLXML 4.0&#41;中&#40;棄用的註釋 XDR 架構](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="using-inline-mapping-schemas"></a>使用內嵌的對應結構描述  
 註解式結構描述可以直接包含在範本中，接著就可以針對內嵌的結構描述指定範本中的 XPath 查詢。 範本也可以是一個 Updategram。  
  
 一個範本可以包含多個內嵌結構描述。 要使用範本中包含的內聯架構,請在**\<xsd:schema>** 元素上指定具有唯一值的**id**屬性,然後使用 **#idvalue**引用內聯架構。 **id**屬性的行為與 XDR 架構中使用的**sql:id(\urn:** 架構-微軟-com:xml-sql_id)相同。  
  
 例如，下列範本指定兩個內嵌的註解式結構描述：  
  
```  
<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema1' sql:is-mapping-schema='1'>  
  <xsd:element name='Employees' ms:relation='HumanResources.Employee'>  
    <xsd:complexType>  
      <xsd:attribute name='LoginID'   
                     type='xsd:string'/>  
      <xsd:attribute name='Title'   
                     type='xsd:string'/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema2' sql:is-mapping-schema='1'>  
  <xsd:element name='Contacts' ms:relation='Person.Contact'>  
    <xsd:complexType>  
  
      <xsd:attribute name='ContactID'   
                     type='xsd:string' />  
      <xsd:attribute name='FirstName'   
                     type='xsd:string' />  
      <xsd:attribute name='LastName'   
                     type='xsd:string' />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema1'>  
    /Employees[@LoginID='adventure-works\guy1']  
</sql:xpath-query>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema2'>  
    /Contacts[@ContactID='1']  
</sql:xpath-query>  
</ROOT>  
```  
  
 範本也會指定兩個 XPath 查詢。 每個**\<xpath 查詢>** 元素使用映射架構屬性來唯一地識別**映射架構**。  
  
 在範本中指定內聯架構時,還必須在**\<xsd:schema>** 元素上指定**sql:is 映射-架構**註釋。 **sql:is 映射架構**採用布爾值(0=false,1=true)。 具有**sql:is-map-架構="1"** 的內聯架構被視為內聯註釋架構,不會在 XML 文檔中返回。  
  
 **sql:is 映射-架構**註解屬於範本命名空間**urn:架構-微軟-com:xml-sql**。  
  
 若要測試此範例，將範本 (InlineSchemaTemplate.xml) 儲存在本機目錄中，然後建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 來執行範本。 有關詳細資訊,請參閱使用[ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 除了在樣本中的**\<sql:xpath 查詢>** 元素(當有 XPath 查詢時)或更新圖中的**\<updg:sync>** 元素上指定**映射架構**屬性外,還可以執行以下操作:  
  
-   在範本中的**\<ROOT>** 元素(全域聲明)上指定**映射架構**屬性。 然後,此映射架構將成為預設架構,所有沒有顯式**映射架構**註釋的 XPath 和 updategram 節點都將使用該架構。  
  
-   使用 ADO**命令**物件指定**映射架構**屬性。  
  
 在**\<xpath 查詢>** 或**\<updg:sync>** 元素上指定的**映射-架構**屬性具有最高的優先順序;ADO**命令**物件具有最低的優先順序。  
  
 請注意,如果在範本中指定 XPath 查詢,並且不指定執行 XPath 查詢的映射架構,則 XPath 查詢將被視為**dbobject**類型查詢。 例如，假設有以下的範本：  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 此範本會指定一個 XPath 查詢，但不會指定對應結構描述。 因此,此查詢被視為**dbobject**類型查詢,其中 Production.ProductPhoto 是表名,#『100』@ProductPhotoID是查找 ID 值為 100 的產品照片的謂詞。 @LargePhoto是從中檢索值的列。  
  
  
