---
title: 使用 sql： datatype 轉換資料類型（SQLXML）
description: 瞭解如何使用 SQLXML 4.0 中的 xsd： type 和 sql： datatype 屬性來控制 XSD 資料類型與 SQL Server 資料類型之間的對應。
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- type attribute
- sql:datatype
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- xsd:type
- datatype annotation
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XSD schemas [SQLXML], mapping data types
ms.assetid: db192105-e8aa-4392-b812-9d727918c005
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 926f9588ad5bf9a29490a84017f3317f8ec5c424
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750786"
---
# <a name="data-type-conversions-and-the-sqldatatype-annotation-sqlxml-40"></a>資料類型轉換和 sql： datatype 注釋（SQLXML 4.0）
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  在 XSD 架構中， **xsd： type**屬性會指定元素或屬性的 xsd 資料類型。 當 XSD 結構描述用於從資料庫擷取資料時，指定的資料類型則會用於將資料格式化。  
  
 除了在架構中指定 XSD 型別之外，您也可以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用**sql： datatype**注釋來指定 Microsoft 資料型別。 **Xsd： type**和**sql： datatype**屬性會控制 xsd 資料類型與資料類型之間的對應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="xsdtype-attribute"></a>xsd:type 屬性  
 您可以使用**xsd： type**屬性來指定對應至資料行之屬性或元素的 XML 資料類型。 **Xsd： type**會影響從伺服器傳回的檔，以及執行的 XPath 查詢。 針對包含**xsd： type**的對應架構執行 xpath 查詢時，xpath 會在處理查詢時使用指定的資料類型。 如需有關 XPath 如何使用**xsd： type**的詳細資訊，請參閱[將 Xsd 資料類型對應到 xpath 資料類型 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)。  
  
 在傳回的文件中，所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型會轉換為字串表示。 某些資料類型需要額外的轉換。 下表列出用於各種**xsd： type**值的轉換。  
  
|XSD 資料類型|SQL Server 轉換|  
|-------------------|---------------------------|  
|Boolean|CONVERT(bit, COLUMN)|  
|Date|LEFT(CONVERT(nvarchar(4000), COLUMN, 126), 10)|  
|decimal|CONVERT(money, COLUMN)|  
|id/idref/idrefs|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|nmtoken/nmtokens|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|時間|SUBSTRING(CONVERT(nvarchar(4000), COLUMN, 126), 1+CHARINDEX(N'T', CONVERT(nvarchar(4000), COLUMN, 126)), 24)|  
|All others|No additional conversion|  
  
> [!NOTE]  
>  所傳回的某些值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能與使用**xsd： type**所指定的 XML 資料類型不相容，這是因為不可能轉換（例如，將 "XYZ" 轉換成**decimal**資料類型），或是因為值超過該資料類型的範圍（例如，轉換成**UnsignedShort** xsd 類型的-100000）。 不相容的類型轉換可能產生無效的 XML 文件或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤。  
  
## <a name="mapping-from-sql-server-data-types-to-xsd-data-types"></a>從 SQL Server 資料類型對應到 XSD 資料類型  
 下表列出從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型對應到 XSD 資料類型的明顯對應。 如果您知道 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型，這個表格會提供您在 XSD 結構描述中可以指定的對應 XSD 類型。  
  
|SQL Server 資料類型|XSD 資料類型|  
|--------------------------|-------------------|  
|**bigint**|**long**|  
|**binary**|**base64Binary**|  
|**bit**|**boolean**|  
|**char**|**string**|  
|**datetime**|**dateTime**|  
|**decimal**|**decimal**|  
|**float**|**double**|  
|**image**|**base64Binary**|  
|**int**|**int**|  
|**money**|**decimal**|  
|**nchar**|**string**|  
|**ntext**|**string**|  
|**nvarchar**|**string**|  
|**numeric**|**decimal**|  
|**real**|**float**|  
|**smalldatetime**|**dateTime**|  
|**smallint**|**short**|  
|**smallmoney**|**decimal**|  
|**sql_variant**|**string**|  
|**sysname**|**string**|  
|**text**|**string**|  
|**timestamp**|**dateTime**|  
|**tinyint**|**unsignedByte**|  
|**varbinary**|**base64Binary**|  
|**varchar**|**string**|  
|**uniqueidentifier**|**string**|  
  
## <a name="sqldatatype-annotation"></a>sql:datatype 註解  
 **Sql： datatype**注釋是用來指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型; 當下列情況時，必須指定此注釋：  
  
-   您**dateTime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 從 XSD **datetime**、 **date**或**time**類型大量載入到 datetime 資料行。 在此情況下，您必須 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用**sql： datatype = "dateTime"** 來識別資料行資料類型。 這項規則也套用於 Updategram。  
  
-   您會大量載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **uniqueidentifier**類型的資料行，而且 XSD 值是包含大括弧（{和}）的 GUID。 當您指定**sql： datatype = "uniqueidentifier"** 時，會先從值中移除大括弧，再將它插入資料行中。 如果未指定**sql： datatype** ，此值會以大括弧傳送，而插入或更新會失敗。  
  
-   XML 資料類型**base64Binary**會對應至各種 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型（**binary**、 **image**或**Varbinary**）。 若要將 XML 資料類型**base64Binary**對應至特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，請使用**sql： datatype**注釋。 該註解會指定資料行明確的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，而該資料行是屬性對應之資料行。 當資料儲存在資料庫中時，這樣的作法就很有用。 藉由指定**sql： datatype**注釋，您可以識別明確的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。  
  
 通常建議您在架構中指定**sql： datatype** 。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱[執行 SQLXML 範例的需求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-xsdtype"></a>A. 指定 xsd:type  
 這個範例示範如何在架構中使用**xsd： type**屬性所指定的 xsd**日期**類型，如何影響所產生的 XML 檔。 該結構描述在 AdventureWorks 資料庫中會提供 Sales.SalesOrderHeader 資料表的 XML 檢視。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader">  
     <xsd:complexType>  
       <xsd:attribute name="SalesOrderID" type="xsd:string" />   
       <xsd:attribute name="CustomerID"   type="xsd:string" />   
       <xsd:attribute name="OrderDate"    type="xsd:date" />   
       <xsd:attribute name="DueDate"  />   
       <xsd:attribute name="ShipDate"  type="xsd:time" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 在這個 XSD 結構描述中，有三種屬性會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回日期值。 當結構描述：  
  
-   在**日期時間屬性上**指定**xsd： type = date** ， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會顯示針對 [**訂購**] 屬性所傳回之值的日期部分。  
  
-   在**ShipDate**屬性上指定**xsd： type = time** ，會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 顯示針對**ShipDate**屬性所傳回之值的時間部分。  
  
-   不會在**DueDate**屬性上指定**xsd： type** ，會顯示所傳回的相同值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 xsdType.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 xsdTypeT.xml 並放在與 xsdType.xml 一樣的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="xsdType.xml">  
        /Order  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     指定給對應結構描述 (xsdType.xml) 的目錄路徑，與儲存範本之目錄相關。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\xsdType.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  

     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 部分結果集如下：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43659"   
         CustomerID="676"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
  <Order SalesOrderID="43660"   
         CustomerID="117"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
 ...  
</ROOT>  
```  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader">  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="CustomerID"  />  
    <AttributeType name="OrderDate" dt:type="date" />  
    <AttributeType name="DueDate" />  
    <AttributeType name="ShipDate" dt:type="time" />  
  
    <attribute type="SalesOrderID" sql:field="OrderID" />  
    <attribute type="CustomerID" sql:field="CustomerID" />  
    <attribute type="OrderDate" sql:field="OrderDate" />  
    <attribute type="DueDate" sql:field="DueDate" />  
    <attribute type="ShipDate" sql:field="ShipDate" />  
</ElementType>  
</Schema>  
```  
  
### <a name="b-specifying-sql-data-type-using-sqldatatype"></a>B. 藉由使用 sql:datatype 指定 SQL 資料類型  
 如需實用範例，請參閱[XML 大量載入範例中的範例 G &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)。 在這個範例中，包含 "{" 和 "}" 的 GUID 值是大量載入的。 此範例中的架構會指定**sql： datatype** ，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型識別為**uniqueidentifier**。 這個範例說明何時必須在架構中指定**sql： datatype** 。  
  
  
