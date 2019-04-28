---
title: 使用註解的查詢 (SQLXML 4.0) 中的 XSD 結構描述 |Microsoft Docs
ms.custom: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9af0e0c5a843ecf475b28dd873ecfedc5d2f6472
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62677948"
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>在查詢中使用註解式 XSD 結構描述 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  您可以針對 XSD 結構描述指定範本中的 XPath 查詢，藉以針對註解式結構描述指定查詢來擷取資料庫中的資料。  
  
  **\<Sql:xpath-查詢 >** 元素可讓您指定 XPath 查詢針對註解式結構描述所定義的 XML 檢視。 針對所要執行的 XPath 查詢的註解式結構描述由使用**對應結構描述**屬性 **\<sql:xpath-查詢 >** 項目。  
  
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
  
 然後，您可以建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs)，將查詢當做範本檔的一部分執行。 如需詳細資訊，請參閱 < [Annotated XDR Schemas&#40;在 SQLXML 4.0 中已被取代&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="using-inline-mapping-schemas"></a>使用內嵌的對應結構描述  
 註解式結構描述可以直接包含在範本中，接著就可以針對內嵌的結構描述指定範本中的 XPath 查詢。 範本也可以是一個 Updategram。  
  
 一個範本可以包含多個內嵌結構描述。 若要使用內嵌結構描述包含在範本中，指定**識別碼**屬性具有唯一值 **\<2&gt;xsd:schema&lt;2} >** 項目，然後再使用 **#idvalue**來參考內嵌結構描述。 **識別碼**屬性是相同的行為**sql: id-prefix** ({urn: schemas-microsoft-microsoft-schemas-microsoft-com:-sql} id) 用於 XDR 結構描述。  
  
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
  
 範本也會指定兩個 XPath 查詢。 每個 **\<xpath 查詢 >** 藉由指定項目的唯一識別的對應結構描述**對應結構描述**屬性。  
  
 當您在範本中，指定將內嵌結構描述**sql： 為對應結構描述**也必須在上指定註釋 **\<2&gt;xsd:schema&lt;2} >** 項目。 **Sql： 為對應結構描述**接受布林值 (0 = false,1 = true)。 使用內嵌結構描述**sql： 為對應結構描述 ="1"** 視為內嵌註解式結構描述，而且不會傳回 XML 文件中。  
  
 **Sql： 為對應結構描述**註解屬於範本命名空間**urn: schemas-microsoft-microsoft-schemas-microsoft-com:-sql**。  
  
 若要測試此範例，將範本 (InlineSchemaTemplate.xml) 儲存在本機目錄中，然後建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 來執行範本。 如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 除了指定**對應結構描述**屬性上 **\<sql:xpath-查詢 >** 項目在範本中 （當 XPath 查詢），或在 **\<updg:sync >** 項目在 updategram 中，您可以執行下列動作：  
  
-   指定**對應結構描述**屬性上**\<根 >** 範本中的項目 （全域宣告）。 此對應結構描述就會變成沒有明確的所有 XPath 和 updategram 節點將都使用的預設結構描述**對應結構描述**註釋。  
  
-   指定**對應結構描述**屬性使用 ADO**命令**物件。  
  
 **對應結構描述**屬性上指定 **\<xpath 查詢 >** 或是 **\<updg:sync >** 項目具有最高優先順序;ADO**命令**物件具有最低的優先順序。  
  
 請注意，是否您在範本中指定 XPath 查詢，且未指定的 XPath 查詢會根據執行的對應結構描述，XPath 查詢會被視為**dbobject**類型查詢。 例如，假設有以下的範本：  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 此範本會指定一個 XPath 查詢，但不會指定對應結構描述。 因此，此查詢會視為**dbobject**類型的查詢，其中 Production.ProductPhoto 是資料表名稱和@ProductPhotoID= '100' 是尋找 ID 值為 100 之產品相片的述詞。 @LargePhoto 是要從中擷取值的資料行。  
  
  
