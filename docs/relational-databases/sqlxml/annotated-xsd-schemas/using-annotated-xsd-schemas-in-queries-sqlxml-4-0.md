---
title: 使用註解式 XSD 結構描述中的查詢 (SQLXML 4.0) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cc4d6f7c2d77f2c375765bd745bee8e35e70f622
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>在查詢中使用註解式 XSD 結構描述 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  您可以針對 XSD 結構描述指定範本中的 XPath 查詢，藉以針對註解式結構描述指定查詢來擷取資料庫中的資料。  
  
 **\<Sql:xpath-查詢 >** 元素可讓您指定 XPath 查詢針對註解式結構描述所定義的 XML 檢視。 依據所要執行的 XPath 查詢的註解式結構描述由使用**對應結構描述**屬性 **\<sql:xpath-查詢 >** 項目。  
  
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
  
 然後，您可以建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs)，將查詢當做範本檔的一部分執行。 如需詳細資訊，請參閱[Annotated XDR Schemas &#40;SQLXML 4.0 中已被取代&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="using-inline-mapping-schemas"></a>使用內嵌的對應結構描述  
 註解式結構描述可以直接包含在範本中，接著就可以針對內嵌的結構描述指定範本中的 XPath 查詢。 範本也可以是一個 Updategram。  
  
 一個範本可以包含多個內嵌結構描述。 若要使用內嵌結構描述包含在範本中，指定**識別碼**屬性包含唯一值 **\<schema >** 項目，然後再使用 **#idvalue**來參考內嵌結構描述。 **識別碼**屬性中都有相同的行為**sql: id-prefix** ({描述 urn:-microsoft-schemas-microsoft-com:-sql} id) XDR 結構描述中使用。  
  
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
  
 範本也會指定兩個 XPath 查詢。 每個 **\<xpath 查詢 >** 項目的唯一識別對應結構描述，藉由指定**對應結構描述**屬性。  
  
 當您在範本中，指定將內嵌結構描述**sql： 為對應結構描述**註釋也必須指定在 **\<schema >** 項目。 **Sql： 為對應結構描述**接受布林值 (0 = false，1 = true)。 內嵌結構描述與**sql： 為對應結構描述 ="1"** 會做為內嵌的註解式結構描述並不會傳回 XML 文件中。  
  
 **Sql： 為對應結構描述**註解屬於範本命名空間**描述 urn:-microsoft-schemas-microsoft-com:-sql**。  
  
 若要測試此範例，將範本 (InlineSchemaTemplate.xml) 儲存在本機目錄中，然後建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 來執行範本。 如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 除了指定**對應結構描述**屬性 **\<sql:xpath-查詢 >** 元素，在範本中 （當 XPath 查詢），或在 **\<updg:sync >** 項目在 updategram 中，您可以執行下列：  
  
-   指定**對應結構描述**屬性**\<根目錄 >** 範本中的項目 （全域宣告）。 此對應結構描述就會變成沒有明確的所有 XPath 和 updategram 節點將都使用的預設結構描述**對應結構描述**註解。  
  
-   指定**對應結構描述**屬性使用 ADO**命令**物件。  
  
 **對應結構描述**屬性上指定 **\<xpath 查詢 >** 或 **\<updg:sync >** 項目具有最高優先順序;ADO**命令**物件具有最低的優先順序。  
  
 請注意，是否您在範本中指定 XPath 查詢，且未指定對應結構描述執行 XPath 查詢是針對，XPath 查詢會被視為**dbobject**類型查詢。 例如，假設有以下的範本：  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 此範本會指定一個 XPath 查詢，但不會指定對應結構描述。 因此，此查詢會視為**dbobject**類型查詢，其中 Production.ProductPhoto 是資料表名稱和@ProductPhotoID= '100' 是尋找 ID 值為 100 之產品相片的述詞。 @LargePhoto 是要從中擷取值之資料行。  
  
  
