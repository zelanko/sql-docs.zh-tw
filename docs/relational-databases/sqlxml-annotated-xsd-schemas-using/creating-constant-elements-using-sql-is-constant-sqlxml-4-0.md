---
title: 使用 sql： is-常數（SQLXML）來建立常數元素
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- element does not map [SQLXML]
- sql:is-constant
- XSD schemas [SQLXML], constant elements
- element mapping [SQLXML], constant elements
- is-constant annotation
- constant elements [SQLXML]
- annotated XSD schemas, constant elements
ms.assetid: 940eea1b-54f5-445f-b844-c894d9f3941b
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 45ab0c13ad2c631a438e2a8637e36d192165094b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "75257483"
---
# <a name="creating-constant-elements-using-sqlis-constant-sqlxml-40"></a>使用 sql:is-constant 建立常數元素 (SQLXML 4.0)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  若要指定常數元素（也就是 XSD 架構中未對應到任何資料庫資料表或資料行的元素），您可以使用**sql： is-常數**注釋。 此註解接受布林值 (0 = false，1 = true)。 可接受的值為 0、1、true 和 false。 您可以在沒有任何屬性的元素上指定**sql： is-常數**注釋。 如果該註解是在值為 True (或 1) 的元素上指定，該元素不會對應到資料庫，但是仍會出現在 XML 文件中。  
  
 **Sql： is-常數**注釋可用於：  
  
-   將最上層元素加入到 XML 文件中。 XML 需要單一的最上層元素 (根元素) 供文件使用。  
  
-   建立容器元素，例如包裝所有訂單的** \<訂單>** 元素。  
  
 **Sql： is-常數**注釋可以加入** \<complexType>** 元素中。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱[執行 SQLXML 範例的需求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-sqlis-constant-to-add-a-container-element"></a>A. 指定 sql:is-constant 來加入容器元素  
 在這個批註式 XSD 架構中， ** \<CustomerOrders>** 會藉由指定**sql： is-常數**屬性（其值為1）定義為常數元素。 因此， ** \<CustomerOrders>** 不會對應到任何資料庫資料表或資料行。 這個常數元素是由>子項目的** \<順序**所組成。  
  
 雖然** \<CustomerOrders>** 不會對應到任何資料庫資料表或資料行，但它仍會顯示在產生的 XML 中，當做包含** \<Order>** 子項目的容器元素。  
  
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
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="CustomerOrders" sql:is-constant="1" >  
          <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"  
                           sql:relationship="CustOrders"   
                           maxOccurs="unbounded" >  
                <xsd:complexType>  
                   <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                   <xsd:attribute name="OrderDate" type="xsd:date" />  
                   <xsd:attribute name="CustomerID" type="xsd:string" />  
                </xsd:complexType>  
              </xsd:element>  
            </xsd:sequence>  
           </xsd:complexType>  
          </xsd:element>  
         </xsd:sequence>  
          <xsd:attribute name="CustomerID" type="xsd:string" />  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 isConstant.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 isConstantT.xml，並儲存在與儲存 isConstant.xml 相同的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="isConstant.xml">  
            Customer[@CustomerID=1]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     為對應結構描述 (isConstant.xml) 指定的目錄路徑，是儲存範本之目錄的相對路徑。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\isConstant.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  

     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 查詢](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 這是部分結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
<Customer CustomerID="1">   
  <CustomerOrders>   
    <Order SalesOrderID="43860" OrderDate="2001-08-01" CustomerID="1" />   
    <Order SalesOrderID="44501" OrderDate="2001-11-01" CustomerID="1" />   
    <Order SalesOrderID="45283" OrderDate="2002-02-01" CustomerID="1" />   
    <Order SalesOrderID="46042" OrderDate="2002-05-01" CustomerID="1" />   
    ...  
  </CustomerOrders>   
</Customer>   
</ROOT>  
```  
  
  
