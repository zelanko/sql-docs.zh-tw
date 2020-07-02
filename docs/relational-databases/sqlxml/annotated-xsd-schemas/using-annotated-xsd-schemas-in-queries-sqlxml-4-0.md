---
title: 在查詢中使用批註式 XSD 架構（SQLXML）
description: 瞭解如何針對 SQLXML 4.0 中批註式 XSD 架構指定 XPath 查詢，以從資料庫中取出資料。
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
ms.openlocfilehash: 857710f894ddc8ef2c874bdc3fed127f0625c8f4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725849"
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>在查詢中使用註解式 XSD 結構描述 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  您可以針對 XSD 結構描述指定範本中的 XPath 查詢，藉以針對註解式結構描述指定查詢來擷取資料庫中的資料。  
  
 **\<sql:xpath-query>** 元素可讓您針對批註式架構所定義的 XML view，指定 XPath 查詢。 要對其執行 XPath 查詢的批註式架構，會使用專案的**對應架構**屬性來識別 **\<sql:xpath-query>** 。  
  
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
  
 然後，您可以建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs)，將查詢當做範本檔的一部分執行。 如需詳細資訊，請參閱[SQLXML 4.0&#41;中 &#40;已被取代的批註式 XDR 架構](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="using-inline-mapping-schemas"></a>使用內嵌的對應結構描述  
 註解式結構描述可以直接包含在範本中，接著就可以針對內嵌的結構描述指定範本中的 XPath 查詢。 範本也可以是一個 Updategram。  
  
 一個範本可以包含多個內嵌結構描述。 若要使用範本中包含的內嵌架構，請在元素上指定具有唯一值的**id**屬性 **\<xsd:schema>** ，然後使用 **#idvalue**來參考內嵌架構。 在 XDR 架構中使用的**sql： id** （{urn：架構-microsoft-com： xml-sql} id）的行為與**id**屬性相同。  
  
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
  
 範本也會指定兩個 XPath 查詢。 每個專案都會藉 **\<xpath-query>** 由指定**對應架構**屬性來唯一識別對應架構。  
  
 當您在範本中指定內嵌架構時，也必須在元素上指定**sql： is-對應架構**注釋 **\<xsd:schema>** 。 **Sql： is-mapping-架構**會採用布林值（0 = false，1 = true）。 具有**sql： is-對應架構 = "1"** 的內嵌架構會被視為內嵌批註的架構，而且不會在 XML 檔中傳回。  
  
 **Sql： is-mapping-架構**注釋屬於範本命名空間**urn：架構-microsoft-com： xml-sql**。  
  
 若要測試此範例，將範本 (InlineSchemaTemplate.xml) 儲存在本機目錄中，然後建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 來執行範本。 如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 除了在範本中的專案上指定**對應架構**屬性 **\<sql:xpath-query>** （當有 XPath 查詢時），或在 updategram 中的元素上， **\<updg:sync>** 您可以執行下列動作：  
  
-   在範本的元素（全域宣告）上指定**對應架構**屬性 **\<ROOT>** 。 這個對應架構接著會變成預設的架構，而所有沒有明確**對應架構**注釋的 XPath 和 updategram-節點將會使用它。  
  
-   使用 ADO **Command**物件指定**對應架構**屬性。  
  
 在或元素上指定的**對應-架構**屬性 **\<xpath-query>** **\<updg:sync>** 具有最高的優先順序; ADO **Command**物件的優先順序最低。  
  
 請注意，如果您在範本中指定 XPath 查詢，且未指定執行 XPath 查詢所依據的對應架構，則會將 XPath 查詢視為**dbobject**類型查詢。 例如，假設有以下的範本：  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 此範本會指定一個 XPath 查詢，但不會指定對應結構描述。 因此，此查詢會被視為**dbobject**類型查詢，其中 ProductPhoto 是資料表名稱，而 @ProductPhotoID = ' 100 ' 則是找到識別碼值為100之產品相片的述詞。 @LargePhoto這是要從中取得值的資料行。  
  
  
