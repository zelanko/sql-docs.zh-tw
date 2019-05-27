---
title: '建立常數項目使用 sql: is-constant&lt (SQLXML 4.0) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
manager: craigg
ms.openlocfilehash: bc100446eb6dff17125b0df7a60b8c2c82e46277
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66013940"
---
# <a name="creating-constant-elements-using-sqlis-constant-sqlxml-40"></a>使用 sql:is-constant 建立常數元素 (SQLXML 4.0)
  若要指定常數元素-也就是 XSD 結構描述沒有對應到任何資料庫資料表或資料行中的項目-您可以使用`sql:is-constant`註釋。 此註解接受布林值 (0 = false，1 = true)。 可接受的值為 0、1、true 和 false。 `sql:is-constant` 註解可以在沒有任何屬性的元素上指定。 如果該註解是在值為 True (或 1) 的元素上指定，該元素不會對應到資料庫，但是仍會出現在 XML 文件中。  
  
 `sql:is-constant` 註解可以用於：  
  
-   將最上層元素加入到 XML 文件中。 XML 需要單一的最上層元素 (根元素) 供文件使用。  
  
-   建立容器元素，例如**\<訂單 >** 包裝所有訂單的項目。  
  
 `sql:is-constant`註解可以加入至 **\<complexType >** 項目。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱 <<c0> [ 如需執行 SQLXML 範例的需求](../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-sqlis-constant-to-add-a-container-element"></a>A. 指定 sql:is-constant 來加入容器元素  
 在此註解式 XSD 結構描述 **\<CustomerOrders >** 定義為常數元素，藉由指定`sql:is-constant`屬性的值為 1。 因此，  **\<CustomerOrders >** 未對應到任何資料庫資料表或資料行。 此常數元素組成**\<順序 >** 子項目。  
  
 雖然 **\<CustomerOrders >** 不會對應到任何資料庫資料表或資料行，它仍然會出現在產生的 XML，做為容器項目包含**\<順序 >** 子項目。  
  
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
  
     如需詳細資訊，請參閱 [使用ADO執行SQLXML查詢](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
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
  
  
