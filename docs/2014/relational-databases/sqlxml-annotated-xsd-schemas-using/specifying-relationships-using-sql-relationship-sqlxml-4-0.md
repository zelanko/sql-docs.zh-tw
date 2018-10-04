---
title: '指定關聯性使用 sql: relationship (SQLXML 4.0) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- IDREFS relationships [SQLXML]
- parent attribute [SQLXML]
- element relationships [SQLXML]
- multiple element relationships
- attribute relationships [SQLXML]
- sql:relationship
- relationship chains [SQLXML]
- IDREF relationships [SQLXML]
- parent-child relationships [SQLXML]
- relationship annotation
- XSD schemas [SQLXML], relationships
- annotated XSD schemas, relationships
- relationships [SQLXML], specifying
- unnamed relationships
- ID relationships [SQLXML]
- hierarchical relationships [SQLXML]
- named relationships [SQLXML]
ms.assetid: 98820afa-74e1-4e62-b336-6111a3dede4c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e5ca0676d280a266561c45388beac938366d17ca
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48144908"
---
# <a name="specifying-relationships-using-sqlrelationship-sqlxml-40"></a>使用 sql:relationship 指定關聯性 (SQLXML 4.0)
  XML 文件中的元素可以是相關聯的。 元素可以是巢狀階層，而且在元素之間可以指定 ID、IDREF 或 IDREFS 關聯性。  
  
 例如，在 XSD 結構描述**\<客戶 >** 項目包含**\<順序 >** 子項目。 當結構描述對應到 AdventureWorks 資料庫中， **\<客戶 >** 元素會對應到 Sales.Customer 資料表和**\<順序 >** 元素會對應到Sales.SalesOrderHeader 資料表。 Sales.Customer 和 Sales.SalesOrderHeader 這些基礎資料表是相關聯的，因為客戶下了訂單。 Sales.SalesOrderHeader 資料表中的 CustomerID 是外部索引鍵，參考 Sales.Customer 資料表中的 CustomerID 主索引鍵。 您可以使用 `sql:relationship` 註解，建立對應結構描述元素之間的關聯性。  
  
 在註解式 XSD 結構描述中，會根據主索引鍵和基礎資料表之間元素所對應的外部索引鍵關聯性，使用 `sql:relationship` 註解以階層方式建立巢狀結構描述元素。 指定 `sql:relationship` 註解時，您必須識別下列項目：  
  
-   父資料表 (Sales.Customer) 和子資料表 (Sales.SalesOrderHeader)。  
  
-   在父資料表和子資料表之間組成關聯性的一或多個資料行。 例如，同時出現在父資料表和子資料表中的 CustomerID 資料行。  
  
 這項資訊用於產生適當的階層。  
  
 若要提供資料表名稱和需要的聯結資訊，則要在 `sql:relationship` 註解上指定下列屬性。 這些屬性只能搭配有效期 **\<sql: relationship >** 項目：  
  
 **名稱**  
 指定關聯性的唯一名稱。  
  
 **父系**  
 指定父關聯 (資料表)。 這是選用的屬性；如果未指定此屬性，會從文件之子階層中的資訊取得父資料表名稱。 如果結構描述指定使用相同的兩個父子式階層 **\<sql: relationship >** 但不同的父項目，您不要指定父屬性 **\<sql:關聯性 >**。 這項資訊是從結構描述的階層中取得。  
  
 **parent-key**  
 指定父系的父索引鍵。 如果父索引鍵由多個資料行所組成，值就會用資料行之間的空格指定。 在指定給多重資料行索引鍵和其對應之子索引鍵的值之間有位置性對應。  
  
 **子系**  
 指定子關聯 (資料表)。  
  
 **child-key**  
 在參考父系中之 parent-key 的子系中指定子索引鍵。 如果子索引鍵由多個屬性 (資料行) 所組成，則 child-key 的值就會用屬性或資料行之間的空格指定。 在指定給多重資料行索引鍵和其對應之父索引鍵的值之間有位置性對應。  
  
 **反向**  
 這個屬性上指定 **\<sql: relationship >** 由 updategrams 所使用。 如需詳細資訊，請參閱 < [sql: relationship 指定 sql: inverse 屬性](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)。  
  
 `sql:key-fields`註解必須指定項目中包含子元素，具有 **\<sql: relationship >** 定義項目和子系之間並不提供的主索引鍵父元素中指定的資料表。 即使未指定結構描述 **\<sql: relationship >**，您必須指定`sql:key-fields`來產生適當的階層。 如需詳細資訊，請參閱 <<c0> [ 使用 sql: key-fields 來識別索引鍵資料行-欄位](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)。  
  
 若要在結果中產生正確的巢狀結構，建議在所有的結構描述中指定 `sql:key-fields`。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱 <<c0> [ 如需執行 SQLXML 範例的需求](../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-the-sqlrelationship-annotation-on-an-element"></a>A. 在元素上指定 sql:relationship 註解  
 下列的註解式的 XSD 結構描述包括**\<客戶 >** 並**\<順序 >** 項目。 **\<順序 >** 項目是子元素**\<客戶 >** 項目。  
  
 在結構描述中，`sql:relationship`上指定註釋**\<順序 >** 子項目。 在 定義關聯性本身 **\<xsd: appinfo >** 項目。  
  
 **\<關聯性 >** 元素 Sales.SalesOrderHeader 資料表中 CustomerID 識別為參考 Sales.Customer 資料表中的 CustomerID 主要索引鍵的外部索引鍵。 因此，客戶的訂單顯示為子項目， **\<客戶 >** 項目。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                    sql:relationship="CustOrders" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 上述結構描述使用具名關聯性。 您也可以指定一個未命名的關聯性。 結果是相同的。  
  
 這是修訂過的結構描述 (其中會指定未命名的關聯性)：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer"  type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader">  
           <xsd:annotation>  
            <xsd:appinfo>  
              <sql:relationship   
                parent="Sales.Customer"  
                parent-key="CustomerID"  
                child="Sales.SalesOrderHeader"  
                child-key="CustomerID" />  
            </xsd:appinfo>  
           </xsd:annotation>  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 sql-relationship.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 sql-relationshipT.xml 並放在與儲存 sql-relationship.xml 相同的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sql-relationship.xml">  
            /Customer[@CustomerID=1]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     為對應結構描述 (sql-relationship.xml) 指定的目錄路徑，是儲存範本之目錄的相對路徑。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\sql-relationship.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 < [Ba6e326154d2"&gt;using ADO to Execute SQLXML Queries&lt](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下為結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer CustomerID="1">   
    <Order OrderID="43860" CustomerID="1" />   
    <Order OrderID="44501" CustomerID="1" />   
    <Order OrderID="45283" CustomerID="1" />   
    <Order OrderID="46042" CustomerID="1" />   
  </Customer>   
</ROOT>  
```  
  
### <a name="b-specifying-a-relationship-chain"></a>B. 指定關聯性鏈結  
 針對這個範例，假設您想要讓下列 XML 文件使用從 AdventureWorks 資料庫取得的資料：  
  
```  
<Order SalesOrderID="43659">  
  <Product Name="Mountain Bike Socks, M"/>   
  <Product Name="Sport-100 Helmet, Blue"/>  
  ...  
</Order>  
...  
```  
  
 針對 Sales.SalesOrderHeader 資料表中每筆訂單，XML 文件有一個**\<順序 >** 項目。 而且每個**\<順序 >** 項目有一份**\<產品 >** 子項目，一個用於每個要求在順序中的產品。  
  
 若要指定產生此階層的 XSD 結構描述，您必須指定兩個關聯性：OrderOD 和 ODProduct。 OrderOD 關聯性會在 Sales.SalesOrderHeader 和 Sales.SalesOrderDetail 資料表之間指定父子式關聯性。 ODProduct 關聯性會在 Sales.SalesOrderDetail 和 Production.Product 資料表之間指定關聯性。  
  
 在下列結構描述中，`msdata:relationship`上的註釋**\<產品 >** 項目會指定兩個值： OrderOD 和 ODProduct。 指定這些值的順序很重要。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <msdata:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  
    <msdata:relationship name="ODProduct"  
          parent="Sales.SalesOrderDetail"  
          parent-key="ProductID"  
          child="Production.Product"  
          child-key="ProductID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID"  
                     msdata:relationship="OrderOD ODProduct">  
          <xsd:complexType>  
             <xsd:attribute name="Name" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
    </xsd:complexType>  
</xsd:schema>  
```  
  
 您可以指定匿名關聯性，而非指定具名關聯性。 在此案例中的整個內容**\<註釋 >**... **\</annotation >**，其中描述兩個關聯性時，顯示為的子元素**\<產品 >**。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID" >  
         <xsd:annotation>  
          <xsd:appinfo>  
           <msdata:relationship   
               parent="Sales.SalesOrderHeader"  
               parent-key="SalesOrderID"  
               child="Sales.SalesOrderDetail"  
               child-key="SalesOrderID" />  
  
           <msdata:relationship   
               parent="Sales.SalesOrderDetail"  
               parent-key="ProductID"  
               child="Production.Product"  
               child-key="ProductID" />  
         </xsd:appinfo>  
       </xsd:annotation>  
       <xsd:complexType>  
          <xsd:attribute name="Name" type="xsd:string" />  
       </xsd:complexType>  
     </xsd:element>  
   </xsd:sequence>  
   <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
  </xsd:complexType>  
 </xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 relationshipChain.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 然後將檔案儲存為 relationshipChainT.xml，並放在與儲存 relationshipChain.xml 的相同目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationshipChain.xml">  
            /Order  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     為對應結構描述 (relationshipChain.xml) 指定的目錄路徑，是儲存範本之目錄的相對路徑。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\relationshipChain.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 < [Ba6e326154d2"&gt;using ADO to Execute SQLXML Queries&lt](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下為結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Order SalesOrderID="43659">  
    <Product Name="Mountain Bike Socks, M" />   
    <Product Name="Sport-100 Helmet, Blue" />   
    <Product Name="AWC Logo Cap" />   
    <Product Name="Long-Sleeve Logo Jersey, M" />   
    <Product Name="Long-Sleeve Logo Jersey, XL" />   
    ...  
  </Order>  
  ...  
</ROOT>  
```  
  
### <a name="c-specifying-the-relationship-annotation-on-an-attribute"></a>C. 在屬性上指定關聯性註解  
 在此範例中的結構描述包括\<客戶 > 項目\<CustomerID > 子元素和 IDREFS 類型的 OrderIDList 屬性。 \<客戶 > 元素會對應到 AdventureWorks 資料庫中的 Sales.Customer 資料表。 根據預設，此對應的範圍套用至所有子元素或屬性，除非`sql:relation`上指定的子元素或屬性，在此情況下，必須定義適當的主索引鍵/外部索引鍵關聯性，使用\<關聯性 > 項目。 同時，使用 `relation` 註解指定不同資料表的子元素或屬性也必須指定 `relationship` 註解。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
     </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="CustomerID"   type="xsd:string" />   
     </xsd:sequence>  
     <xsd:attribute name="OrderIDList"   
                     type="xsd:IDREFS"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:field="SalesOrderID"  
                     sql:relationship="CustOrders" >  
        </xsd:attribute>  
    </xsd:complexType>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 relationship-on-attribute.xml。  
  
2.  複製下列範本，並將其貼到檔案中。 將檔案儲存為 relationship-on-attributeT.xml，並放在與儲存 relationship-on-attribute.xml 相同的目錄中。 範本中的查詢會選取 CustomerID 為 1 的客戶。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-on-attribute.xml">  
        /Customer[CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     為對應結構描述 (relationship-on-attribute.xml) 指定的目錄路徑，是儲存範本之目錄的相對路徑。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\relationship-on-attribute.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 < [Ba6e326154d2"&gt;using ADO to Execute SQLXML Queries&lt](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下為結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer OrderIDList="43860 44501 45283 46042">  
    <CustomerID>1</CustomerID>   
  </Customer>  
</ROOT>  
```  
  
### <a name="d-specifying-sqlrelationship-on-multiple-elements"></a>D. 在多重元素中指定 sql:relationship  
 在此範例中，包含註解式的 XSD 結構描述**\<客戶 >**， **\<順序 >**，以及 **\<OrderDetail >** 項目。  
  
 **\<順序 >** 項目是子元素**\<客戶 >** 項目。 **\<sql: relationship >** 上指定**\<順序 >** 子項目; 因此，客戶的訂單顯示為子項目的**\<客戶 >**.  
  
 **\<順序 >** 項目包含 **\<OrderDetail >** 子項目。 **\<sql: relationship >** 上指定 **\<OrderDetail >** 子項目，因此，訂單的訂單詳細資料會顯示為該子項目**\<順序 >** 項目。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
        parent="Sales.Customer"  
        parent-key="CustomerID"  
        child="Sales.SalesOrderHeader"  
        child-key="CustomerID" />  
  
    <sql:relationship name="OrderOrderDetail"  
        parent="Sales.SalesOrderHeader"  
        parent-key="SalesOrderID"  
        child="Sales.SalesOrderDetail"  
        child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"    
              sql:relationship="CustOrders" maxOccurs="unbounded" >  
          <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OrderDetail"   
                             sql:relation="Sales.SalesOrderDetail"   
                             sql:relationship="OrderOrderDetail"   
                             maxOccurs="unbounded" >  
                  <xsd:complexType>  
                    <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                    <xsd:attribute name="ProductID" type="xsd:string" />  
                    <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID" type="xsd:string" />  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 relationship-multiple-elements.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 relationship-multiple-elementsT.xml，並放在與儲存 relationship-multiple-elements.xml 相同的目錄中。 範本中的查詢會傳回 CustomerID 為 1 和 SalesOrderID 為 43860 之客戶的訂單資訊。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-multiple-elements.xml">  
        /Customer[@CustomerID=1]/Order[@SalesOrderID=43860]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     為對應結構描述 (relationship-multiple-elements.xml) 指定的目錄路徑，是儲存範本之目錄的相對路徑。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\relationship-multiple-elements.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 < [Ba6e326154d2"&gt;using ADO to Execute SQLXML Queries&lt](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下為結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43860" OrderDate="2001-08-01" CustomerID="1">  
     <OrderDetail SalesOrderID="43860" ProductID="761" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="770" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="758" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="765" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="732" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="762" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="738" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="768" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="753" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="729" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="763" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="756" OrderQty="1" />   
  </Order>  
</ROOT>  
```  
  
### <a name="e-specifying-the-sqlrelationship-without-the-parent-attribute"></a>E. 指定\<sql: relationship > 沒有 parent 屬性  
 此範例說明如何指定 **\<sql: relationship >** 而不需要**父**屬性。 例如，假設您有下列員工資料表：  
  
```  
Emp1(SalesPersonID, FirstName, LastName, ReportsTo)  
Emp2(SalesPersonID, FirstName, LastName, ReportsTo)  
```  
  
 下列的 XML 檢視 **\<Emp1 >** 並 **\<Emp2 >** 對應到 Sales.Emp1 和 Sales.Emp2 資料表的項目：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="EmpOrders"  
          parent-key="SalesPersonID"  
          child="Sales.SalesOrderHeader"  
          child-key="SalesPersonID" />  
     </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Emp1" sql:relation="Sales.Emp1" type="EmpType" />  
  <xsd:element name="Emp2" sql:relation="Sales.Emp2" type="EmpType" />  
   <xsd:complexType name="EmpType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:relationship="EmpOrders" >  
          <xsd:complexType>  
             <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
             <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesPersonID"   type="xsd:integer" />   
        <xsd:attribute name="LastName"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 在結構描述中，同時 **\<Emp1 >** 項目並 **\<Emp2 >** 項目都屬於型別`EmpType`。 型別`EmpType`描述**\<順序 >** 子項目和對應 **\<sql: relationship >**。 在此情況下，沒有可以識別在單一父系 **\<sql: relationship >** 利用**父**屬性。 在此情況下，您未指定**父代**屬性中 **\<sql: relationship >**;**父**屬性資訊取自結構描述中的階層。  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  在 AdventureWorks 資料庫中建立這些資料表：  
  
    ```  
    USE AdventureWorks  
    CREATE TABLE Sales.Emp1 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    CREATE TABLE Sales.Emp2 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    ```  
  
2.  在資料表中加入此範例資料：  
  
    ```  
    INSERT INTO Sales.Emp1 values (279, 'Nancy', 'Devolio',NULL)  
    INSERT INTO Sales.Emp1 values (282, 'Andrew', 'Fuller',1)  
    INSERT INTO Sales.Emp1 values (276, 'Janet', 'Leverling',1)  
    INSERT INTO Sales.Emp2 values (277, 'Margaret', 'Peacock',3)  
    INSERT INTO Sales.Emp2 values (283, 'Steven', 'Devolio',4)  
    INSERT INTO Sales.Emp2 values (275, 'Nancy', 'Buchanan',5)  
    INSERT INTO Sales.Emp2 values (281, 'Michael', 'Suyama',6)  
    ```  
  
3.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 relationship-noparent.xml。  
  
4.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 relationship-noparentT.xml，並放在與儲存 relationship-noparent.xml 相同的目錄中。 在範本中的查詢會選取所有\<Emp1 > 項目 （因此，父系為 Emp1）。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationship-noparent.xml">  
            /Emp1  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     為對應結構描述 (relationship-noparent.xml) 指定的目錄路徑，是儲存範本之目錄的相對路徑。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\relationship-noparent.xml"  
    ```  
  
5.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 < [Ba6e326154d2"&gt;using ADO to Execute SQLXML Queries&lt](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下是部分結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<Emp1 SalesPersonID="276" LastName="Leverling">  
  <Order SalesOrderID="43663" CustomerID="510" />   
  <Order SalesOrderID="43666" CustomerID="511" />   
  <Order SalesOrderID="43859" CustomerID="259" />  
  ...  
</Emp1>  
```  
  
  
