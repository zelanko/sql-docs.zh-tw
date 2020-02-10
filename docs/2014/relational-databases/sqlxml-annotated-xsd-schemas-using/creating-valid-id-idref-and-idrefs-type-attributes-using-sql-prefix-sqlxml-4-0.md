---
title: 使用 sql： prefix 建立有效的 ID、IDREF 和 IDREFS 類型屬性（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREFS relationships [SQLXML]
- annotated XSD schemas, ID type attribute
- IDREF type attribute [SQLXML]
- annotated XSD schemas, IDREFS type attribute
- ID type attribute [SQLXML]
- sql:prefix
- prefix annotation
- IDREF relationships [SQLXML]
- IDREFS type attribute [SQLXML]
- annotated XSD schemas, IDREF type attribute
- ID relationships [SQLXML]
ms.assetid: 1c7f77d3-81f3-4820-bb63-c4aaa4ea9aa1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48ae7034ec0c133c1140e4c581794302ca8bad77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013914"
---
# <a name="creating-valid-id-idref-and-idrefs-type-attributes-using-sqlprefix-sqlxml-40"></a>使用 sql:prefix 建立 Valid ID、IDREF 和 IDREFS 類型屬性 (SQLXML 4.0)
  屬性可以指定為識別碼類型屬性。 然後可以使用指定為 IDREF 或 IDREFS 的屬性來參考 ID 類型屬性，啟用文件之間的連結。  
  
 ID、IDREF 和 IDREFS 會對應至 PK/FK (主索引鍵/外部索引鍵) 在資料庫中的關聯性，但是有一些差異。 在 XML 文件中，ID 類型屬性的值必須是相異的。 如果在 XML 檔中將**CustomerID**和「**訂單**」屬性指定為 ID 類型，則這些值必須是相異的。 然而在資料庫中，CustomerID 和 OrderID 資料行的值可以相同  (例如，CustomerID = 1 且 OrderID = 1 在資料庫中是有效的)。  
  
 若要讓識別碼、IDREF 和 IDREFS 屬性是有效的：  
  
-   識別碼的值在 XML 文件中必須是唯一的。  
  
-   針對每一個 IDREF 和 IDREFS，參考的識別碼值都必須在 XML 文件中。  
  
-   ID、IDREF 和 IDREFS 的值必須是具名 Token  (例如，整數值 101 不能是 ID 值)。  
  
-   ID、IDREF 和 IDREFS 類型的屬性不能對應至類型 `text`、`ntext`、`image` 或任何其他二進位資料類型 (例如 `timestamp`) 的資料行。  
  
 如果 XML 文件含有多個識別碼，請使用 `sql:prefix` 註解來確保值是唯一的。  
  
 請注意，`sql:prefix` 註解不能搭配 XSD 固定屬性一起使用。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱[執行 SQLXML 範例的需求](../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-id-and-idrefs-types"></a>A. 指定 ID 和 IDREFS 類型  
 在下列架構中， ** \<Customer>** 元素是由** \<Order>** 子項目所組成。 Order>元素也具有子項目，也就是** \<OrderDetail>** 元素。 ** \< **  
  
 Customer>的**OrderIDList**屬性是一個 IDREFS 類型屬性，它會參考** \<Order>** **元素的「訂單」屬性。** ** \< **  
  
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
             <xsd:attribute name="SalesOrderID"   
                            type="xsd:ID" sql:prefix="ord-" />  
             <xsd:attribute name="OrderDate" type="xsd:date" />  
             <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
      </xsd:element>  
    </xsd:sequence>  
    <xsd:attribute name="CustomerID" type="xsd:string" />  
    <xsd:attribute name="OrderIDList" type="xsd:IDREFS"   
                   sql:relation="Sales.SalesOrderHeader" sql:field="SalesOrderID"  
                   sql:relationship="CustOrders" sql:prefix="ord-">  
    </xsd:attribute>  
  </xsd:complexType>  
</xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 sqlPrefix.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存在與 sqlPrefix.xml 相同的目錄中，並儲存為 sqlPrefixT.xml。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="sqlPrefix.xml">  
        /Customer[@CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (sqlPrefix.xml) 指定的目錄路徑，相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\sqlPrefix.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 查詢](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下是部份結果：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="1" OrderIDList="ord-43860 ord-44501 ord-45283 ord-46042">  
    <Order SalesOrderID="ord-43860" OrderDate="2001-08-01" CustomerID="1">  
      <OrderDetail SalesOrderID="43860" ProductID="729" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="732" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="738" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="753" OrderQty="2" />   
      ...  
    </Order>  
    ...  
 </Customer>  
</ROOT>  
```  
  
  
