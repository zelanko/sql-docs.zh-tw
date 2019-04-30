---
title: XML 結構描述集合 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XSD schemas [SQL Server]
- xml_schema_namespace function
- XML schema collections [SQL Server], about XML schema collections
- metadata [SQL Server], XML schema collections
- queries [XML in SQL Server], XML schema collections
- schema collections [SQL Server]
- schemas [SQL Server], XML
- XML [SQL Server], schema collections
- XML schema collections [SQL Server]
- schema collections [SQL Server], about XML schema collections
ms.assetid: 659d41aa-ccec-4554-804a-722a96ef25c2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45f3dfbf7a4caa2744ef57a352b0434e7eb1bf37
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63193035"
---
# <a name="xml-schema-collections-sql-server"></a>XML 結構描述集合 (SQL Server)
  主題中所述[xml &#40;TRANSACT-SQL&#41;](/sql/t-sql/xml/xml-transact-sql)，SQL Server 提供原生的 XML 資料，透過儲存`xml`資料類型。 您可以選擇性地關聯的 XSD 結構描述的變數或資料行`xml`透過 XML 結構描述集合的型別。 XML 結構描述集合會儲存匯入的 XML 結構描述，然後用來執行下列作業：  
  
-   驗證 XML 執行個體  
  
-   當 XML 資料儲存在資料庫中時，設定其類型  
  
 請注意，XML 結構描述集合是一個中繼資料實體，就像資料庫中的資料表。 您可以加以建立、修改及卸除。 系統會將 [CREATE XML SCHEMA COLLECTION (Transact-SQL)](/sql/t-sql/statements/create-xml-schema-collection-transact-sql) 陳述式中所指定的結構描述，自動匯入新建的 XML 結構描述集合物件中。 您可以使用 [ALTER XML SCHEMA COLLECTION (Transact-SQL)](/sql/t-sql/statements/alter-xml-schema-collection-transact-sql) 陳述式，將其他的結構描述或結構描述元件匯入資料庫的現有集合物件中。  
  
 如[比較具類型的 XML 與不具類型的 XML](../xml/compare-typed-xml-to-untyped-xml.md) 主題所述，如果 XML 是儲存在有關聯之結構描述的資料行或變數中，即為**具類型的** XML，因為結構描述會提供執行個體資料所需的資料類型資訊。 SQL Server 會使用此類型資訊來將資料儲存最佳化。  
  
 查詢處理引擎也會使用結構描述來檢查類型，以及將查詢和資料修改最佳化。  
  
 此外，SQL Server 會使用相關聯的 XML 結構描述集合的情況下，輸入`xml`，來驗證 XML 執行個體。 如果 XML 執行個體符合結構描述，資料庫就會允許執行個體以其類型資訊儲存在系統中。 否則，資料庫會拒絕該執行個體。  
  
 您可以使用內建函數 XML_SCHEMA_NAMESPACE 來擷取儲存在資料庫中的結構描述集合。 如需詳細資訊，請參閱 [檢視儲存的 XML 結構描述集合](../xml/view-a-stored-xml-schema-collection.md)。  
  
 您也可以使用 XML 結構描述集合來輸入 XML 變數、參數及資料行。  
  
##  <a name="ddl"></a> 管理結構描述集合的 DDL  
 您可以在資料庫中建立 XML 結構描述集合，然後將它們與 `xml` 類型的變數和資料行產生關聯。 為了管理資料庫中的結構描述集合， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了下列 DDL 陳述式：  
  
-   [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-xml-schema-collection-transact-sql) 將結構描述元件匯入資料庫中。  
  
-   [ALTER XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-xml-schema-collection-transact-sql) 修改現有 XML 結構描述集合中的結構描述元件。  
  
-   [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-xml-schema-collection-transact-sql) 刪除整個 XML 結構描述集合及其所有的元件。  
  
 若要使用 XML 結構描述集合及其包含的結構描述，您必須先使用 CREATE XML SCHEMA COLLECTION 陳述式來建立集合和結構描述。 在建立結構描述集合之後，您就可以建立 `xml` 類型的變數和資料行，並將結構描述集合與它們產生關聯。 請注意，建立結構描述集合之後，各種結構描述元件會儲存在中繼資料內。 您也可以使用 ALTER XML SCHEMA COLLECTION 將更多元件加入現有的結構描述，或將新的結構描述加入現有的集合。  
  
 若要卸除結構描述集合，請使用 DROP XML SCHEMA COLLECTION 陳述式。 這會卸除集合中包含的所有結構描述，並移除集合物件。 請注意，必須符合 [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-xml-schema-collection-transact-sql) 中描述的條件，才能卸除結構描述集合。  
  
##  <a name="components"></a> 了解結構描述元件  
 當您使用 CREATE XML SCHEMA COLLECTION 陳述式時，會將各種結構描述元件匯入資料庫中。 結構描述元件包括結構描述元素、屬性和類型定義。 當您使用 DROP XML SCHEMA COLLECTION 陳述式時，整個集合都會移除。  
  
 CREATE XML SCHEMA COLLECTION 會將結構描述元件儲存到各種系統資料表中。  
  
 例如，請考慮下列結構描述：  
  
```  
<?xml version="1.0"?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            targetNamespace="uri:Cust_Orders2"  
            xmlns="uri:Cust_Orders2" >  
  <xsd:attribute name="SomeAttribute" type="xsd:int" />  
  <xsd:complexType name="SomeType" />  
  <xsd:complexType name="OrderType" >  
    <xsd:sequence>  
      <xsd:element name="OrderDate" type="xsd:date" />  
      <xsd:element name="RequiredDate" type="xsd:date" />  
      <xsd:element name="ShippedDate" type="xsd:date" />  
    </xsd:sequence>  
    <xsd:attribute name="OrderID" type="xsd:ID" />  
    <xsd:attribute name="CustomerID"  />  
    <xsd:attribute name="EmployeeID"  />  
  </xsd:complexType>  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order" type="OrderType"  
                     maxOccurs="unbounded" />  
       </xsd:sequence>  
      <xsd:attribute name="CustomerID" type="xsd:string" />  
      <xsd:attribute name="OrderIDList" type="xsd:IDREFS" />  
  </xsd:complexType>  
  <xsd:element name="Customer" type="CustomerType" />  
</xsd:schema>  
```  
  
 以上的結構描述顯示可儲存於資料庫的不同類型元件， 這些元件包括 `SomeAttribute`、 `SomeType`、 `OrderType`、 `CustomerType`、 `Customer`、 `Order`、 `CustomerID`、 `OrderID`、 `OrderDate`、 `RequiredDate`及 `ShippedDate`。  
  
### <a name="component-categories"></a>元件類別  
 儲存在資料庫中的「結構描述」元件可分成下列類別：  
  
-   ELEMENT  
  
-   ATTRIBUTE  
  
-   TYPE (適用於簡單或複雜類型)  
  
-   ATTRIBUTEGROUP  
  
-   MODELGROUP  
  
 例如：  
  
-   **SomeAttribute** 是 ATTRIBUTE 元件。  
  
-   **SomeType**、 **OrderType**和 **CustomerType** 是 TYPE 元件。  
  
-   **Customer** 是 ELEMENT 元件。  
  
 當您將結構描述匯入資料庫後， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並不會儲存結構描述本身。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會儲存各種個別的元件。 也就是說，並未儲存 \<Schema> 標記，只是保留定義於其中的元件。 所有的結構描述元素都沒有保留。 如果 \<Schema> 標記包含指定其元件預設行為的屬性，則這些屬性會在匯入程序期間移到標記內的結構描述元件，如下表所示。  
  
|屬性名稱|行為|  
|--------------------|--------------|  
|**attributeFormDefault**|**form** 屬性會套用到結構描述中尚未出現此屬性的所有屬性宣告上，而且其值會設定為 **attributeFormDefault** 屬性的值。|  
|**elementFormDefault**|**form** 屬性會套用到結構描述中尚未出現此屬性的所有元素宣告上，而且其值會設定為 **elementFormDefault** 屬性的值。|  
|**blockDefault**|**block** 屬性會套用到尚未出現此屬性的所有元素宣告和類型定義上，而且其值會設定為 **blockDefault** 屬性的值。|  
|**finalDefault**|**final** 屬性會套用到尚未出現此屬性的所有元素宣告和類型定義上，而且其值會設定為 **finalDefault** 屬性的值。|  
|**targetNamespace**|隸屬於目標命名空間之元件的詳細資訊會儲存在中繼資料內。|  
  
##  <a name="perms"></a> XML 結構描述集合上的權限  
 您必須有必要權限，才能執行下列作業：  
  
-   建立/載入 XML 結構描述集合  
  
-   修改 XML 結構描述集合  
  
-   卸除 XML 結構描述集合  
  
-   使用 XML 結構描述集合來輸入`xml`輸入資料行、 變數和參數，或在資料表或資料行條件約束中使用它  
  
 SQL Server 安全性模型允許在每個物件上都可以有 CONTROL 權限。 此權限的被授與者可取得物件上的所有其他權限。 物件的擁有者也擁有該物件的所有權限。  
  
 某物件上 CONTROL 權限的擁有者和被授與者，可以授與該物件上的任何權限。 如果指定了 WITH GRANT OPTION，不是擁有者的使用者或沒有 CONTROL 權限的使用者仍可以授與物件上的權限。 例如，假設「使用者 A」透過 WITH GRANT OPTION，對於 XML 結構描述集合 S 擁有 REFERENCES 權限，但沒有其他權限。「使用者 A」可以授與「使用者 B」對於結構描述集合 S 的 REFERENCES 權限。  
  
 安全性模型也允許建立和使用 XML 結構描述集合的權限，或將所有權從某個使用者轉給另一個使用者的權限。 下列主題描述 XML 結構描述集合權限。  
  
-   [授與 XML 結構描述集合的權限](../xml/grant-permissions-on-an-xml-schema-collection.md)  
  
     此主題討論如何授與權限以建立 XML 結構描述集合，以及如何授與 XML 結構描述集合物件上的權限。  
  
-   [撤銷 XML 結構描述集合上的權限](../xml/revoke-permissions-on-an-xml-schema-collection.md)  
  
     此主題討論如何使用撤銷權限以防止建立 XML 結構描述集合，以及如何撤銷 XML 結構描述集合物件上的權限。  
  
-   [拒絕 XML 結構描述集合的權限](../xml/deny-permissions-on-an-xml-schema-collection.md)  
  
     此主題討論如何拒絕建立 XML 結構描述集合的權限，以及拒絕 XML 結構描述集合物件的權限。  
  
##  <a name="info"></a> 取得有關 XML 結構描述和結構描述集合的資訊  
 XML 結構描述集合會列舉在目錄檢視 sys.xml_schema_collections 中。 XML 結構描述集合 "sys" 是由系統定義的。 其包含預先定義的命名空間，您不需要明確地將其載入，即可用在所有使用者自訂的 XML 結構描述集合中。 此清單包含 xml、xs、xsi、fn 及 xdt 的命名空間。 另外二個目錄檢視為 sys.xml_schema_namespaces：列舉出每個 XML 結構描述集合中的所有命名空間；以及 sys.xml_components：列舉出每個 XML 結構描述中的所有 XML 結構描述元件。  
  
 內建函式**XML_SCHEMA_NAMESPACE**， *schemaName、 XmlSchemacollectionName、 namespace-uri*，會產生`xml`資料類型執行個體... 此執行個體包含 XML 結構描述集合中所包含之結構描述的 XML 結構描述片段 (預先定義的 XML 結構描述除外)。  
  
 您可以用下列方法來列舉 XML 結構描述集合的內容：  
  
-   在 XML 結構描述集合的適當目錄檢視上撰寫 Transact-SQL 查詢。  
  
-   使用內建函數 **XML_SCHEMA_NAMESPACE()**。 您可以套用`xml`資料類型方法，此函式的輸出。 但是您不能修改基礎 XML 結構描述。  
  
 如下列範例所示。  
  
### <a name="example-enumerate-the-xml-namespaces-in-an-xml-schema-collection"></a>範例列舉 XML 結構描述集合中的 XML 命名空間  
 針對 XML 結構描述集合 "myCollection" 來使用下列查詢：  
  
```  
SELECT XSN.name  
FROM    sys.xml_schema_collections XSC JOIN sys.xml_schema_namespaces XSN  
    ON (XSC.xml_collection_id = XSN.xml_collection_id)  
WHERE    XSC.name = 'myCollection'     
```  
  
### <a name="example-enumerate-the-contents-of-an-xml-schema-collection"></a>範例列舉 XML 結構描述集合的內容  
 下列陳述式會列舉關聯式結構描述 dbo 中之 XML 結構描述集合 "myCollection" 的內容。  
  
```  
SELECT XML_SCHEMA_NAMESPACE (N'dbo', N'myCollection')  
```  
  
 在集合內的個別 XML 結構描述可以做為取得`xml`資料類型執行個體所做的第三個引數中指定的目標命名空間**xml_schema_namespace （)**。 下列範例會顯示這一點。  
  
### <a name="example-output-a-specified-schema-from-an-xml-schema-collection"></a>範例從 XML 結構描述集合輸出指定的結構描述  
 下列陳述式會從關聯式結構描述 dbo 中的 XML 結構描述集合 "myCollection"，輸出含有目標命名空間 "<https://www.microsoft.com/books>" 的 XML 結構描述。  
  
```  
SELECT XML_SCHEMA_NAMESPACE (N'dbo', N'myCollection',   
N'https://www.microsoft.com/books')  
```  
  
### <a name="querying-xml-schemas"></a>查詢 XML 結構描述  
 您可以用下列方法來查詢您已載入至 XML 結構描述集合的 XML 結構描述：  
  
-   在 XML 結構描述命名空間的目錄檢視上撰寫 Transact-SQL 查詢。  
  
-   建立一個包含 `xml` 資料類型資料行的資料表來儲存您的 XML 結構描述，並將其載入至 XML 類型系統。 您可以使用 `xml` 資料類型方法來查詢 XML 資料行。 您也可以在此資料行上建立 XML 索引。 然而，使用這個方法時，應用程式必須維護儲存在 XML 資料行中之 XML 結構描述與 XML 類型系統之間的一致性。 例如，若您從 XML 類型系統中卸除 XML 結構描述命名空間，就必須也將它從資料表中卸除，以維持一致性。  
  
## <a name="see-also"></a>另請參閱  
 [檢視儲存的 XML 結構描述集合](../xml/view-a-stored-xml-schema-collection.md)   
 [前置處理結構描述以合併包含的結構描述](../xml/preprocess-a-schema-to-merge-included-schemas.md)   
 [伺服器上 XML 結構描述集合的需求與限制](../xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
