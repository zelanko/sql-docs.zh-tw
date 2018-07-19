---
title: 指定目標命名空間使用 targetNamespace 屬性 (SQLXML 4.0) |Microsoft 文件
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
- namespaces [SQLXML], annotated XSD schemas
- targetNamespace attribute
- XSD schemas [SQLXML], target namespaces
- annotated XSD schemas, target namespaces
- xsd:targetNamespace
- attributeFormDefault attribute
- elementFormDefault attribute
- target namespaces [SQLXML]
ms.assetid: f3df9877-6672-4444-8245-2670063c9310
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0c755e668f5d7360d9d37f352d1cc32295b3cf5c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32971903"
---
# <a name="specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-40"></a>使用 targetNamespace 屬性來指定目標命名空間 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  在撰寫 XSD 結構描述，您可以使用 XSD **targetNamespace**屬性來指定目標命名空間。 本主題描述如何在 XSD **targetNamespace**， **elementFormDefault**，和**attributeFormDefault**屬性工作，它們會是 XML 執行個體的影響產生，以及與命名空間指定 XPath 查詢的方式。  
  
 您可以使用**xsd: targetnamespace**屬性，以將項目和預設命名空間的屬性放入不同的命名空間。 您也可以指定本機宣告的元素及結構描述的屬性是否應該以命名空間限定的形式出現 (使用前置詞明確限定或是依照預設的隱含方式限定)。 您可以使用**elementFormDefault**和**attributeFormDefault**上的屬性 **\<schema >** 以全域方式指定的項目限定本機元素和屬性，或者您可以使用**表單**屬性，以分別指定個別的項目和屬性。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱[執行 SQLXML 範例的需求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-a-target-namespace"></a>A. 指定目標命名空間  
 下列 XSD 結構描述指定目標命名空間使用**xsd: targetnamespace**屬性。 結構描述也會設定**elementFormDefault**和**attributeFormDefault**屬性的值即可 **"unqualified"** （這些屬性的預設值）。 這是全域宣告，而且會影響所有本機元素 (**\<順序 >** 結構描述中) 和屬性 (**CustomerID**， **ContactName**，和**OrderID**結構描述中)。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:CO="urn:MyNamespace"   
            targetNamespace="urn:MyNamespace" >  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer"   
               sql:relation="Sales.Customer"   
               type="CO:CustomerType" />  
  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustOrders"  
                     type="CO:OrderType" />  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesPersonID"  type="xsd:string" />  
  </xsd:complexType>  
  <xsd:complexType name="OrderType" >  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name="CustomerID" type="xsd:string" />  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 在此結構描述中：  
  
-   **CustomerType**和**OrderType**類型宣告是全域的因此會包含在結構描述的目標命名空間。 如此一來，當參考這些類型的宣告中**\<客戶 >** 項目和其**\<順序 >** 子元素，指定相關聯的前置字元目標命名空間中。  
  
-   **\<客戶 >** 因為它是結構描述中的全域項目，在結構描述的目標命名空間也包含項目。  
  
 針對此結構描述執行下列 XPath 查詢：  
  
```  
(/CO:Customer[@CustomerID=1)   
```  
  
 XPath 查詢會產生這個執行個體文件 (只顯示一些訂單)：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <y0:Customer xmlns:y0="urn:MyNamespace"   
      CustomerID="ALFKI" ContactName="Maria Anders">  
        <Order CustomerID="ALFKI" OrderID="10643" />   
        <Order CustomerID="ALFKI" OrderID="10692" />   
        ...  
  </y0:Customer>  
  </ROOT>  
```  
  
 這個執行個體文件定義 urn: MyNamespace 的命名空間，並將它的前置詞 (y0) 產生關聯。 前置詞只會套用至**\<客戶 >** 全域項目。 (此元素為全域的因為它宣告為的子系 **\<schema >** 結構描述中的項目。)  
  
 前置詞不會套用到本機元素和屬性因為值**elementFormDefault**和**attributeFormDefault**屬性設為 **"unqualified"** 結構描述中。 請注意， **\<順序 >** 本機項目是因為它的宣告會顯示為的子系 **\<complexType >** 項目，定義 **\<CustomerType >** 項目。 同樣地，屬性 (**CustomerID**， **OrderID**，和**ContactName**) 是本機、 不是全域。  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>若要建立這個結構描述的工作範例  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將此檔案儲存為 targetNameSpace.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 targetNameSpaceT.xml，並放在與 targetNamespace.xml 相同的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="targetNamespace.xml"  
                       xmlns:CO="urn:MyNamespace" >  
        /CO:Customer[@CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     範本中的 XPath 查詢會傳回**\<客戶 >** 針對 customerid 為 1 的客戶的項目。 請注意，XPath 查詢會針對此查詢中的元素 (而不是屬性) 來指定命名空間前置詞  (如同結構描述中所指定，本機屬性並未限定)。  
  
     針對對應結構描述 (targetNamespace.xml) 所指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\targetNamepsace.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 如果結構描述指定**elementFormDefault**和**attributeFormDefault**屬性而且值 **"qualified"**，執行個體文件將會擁有所有的本機限定的項目和屬性。 您可以變更要包含這些屬性在上述的結構描述 **\<schema >** 項目，再重新執行範本。 因為這些屬性現在也會在此執行個體中限定，所以 XPath 查詢將會變更為可包含命名空間前置詞。  
  
 這是修改過的 XPath 查詢：  
  
```  
/CO:Customer[@CO:CustomerID=1]  
```  
  
 這是傳回的 XML 文件：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <y0:Customer xmlns:y0="urn:MyNamespace" CustomerID="1" SalesPersonID="280">  
      <Order SalesOrderID="43860" CustomerID="1" />   
      <Order SalesOrderID="44501" CustomerID="1" />   
      <Order SalesOrderID="45283" CustomerID="1" />   
      <Order SalesOrderID="46042" CustomerID="1" />   
   </y0:Customer>  
</ROOT>  
```  
  
  
