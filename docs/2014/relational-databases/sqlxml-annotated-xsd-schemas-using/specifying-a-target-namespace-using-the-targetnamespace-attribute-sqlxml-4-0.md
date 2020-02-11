---
title: 使用 targetNamespace 屬性來指定目標命名空間（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd97b67974f248d002255c1977feebe4551e691f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013674"
---
# <a name="specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-40"></a>使用 targetNamespace 屬性來指定目標命名空間 (SQLXML 4.0)
  在撰寫 XSD 架構時，您可以使用 XSD **targetNamespace**屬性來指定目標命名空間。 本主題描述 XSD **targetNamespace**、 **elementFormDefault**和**attributeFormDefault**屬性如何作用、它們如何影響所產生的 XML 實例，以及如何使用命名空間來指定 XPath 查詢。  
  
 您可以使用**xsd： targetNamespace**屬性，將預設命名空間中的元素和屬性放入不同的命名空間。 您也可以指定本機宣告的元素及結構描述的屬性是否應該以命名空間限定的形式出現 (使用前置詞明確限定或是依照預設的隱含方式限定)。 您可以使用** \<xsd： schema>** 專案上的**elementFormDefault**和**attributeFormDefault**屬性，全域指定本機專案和屬性的限定性，或者您也可以使用**form**屬性分別指定個別的專案和屬性。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱[執行 SQLXML 範例的需求](../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-a-target-namespace"></a>A. 指定目標命名空間  
 下列 XSD 架構會使用**xsd： targetNamespace**屬性來指定目標命名空間。 此架構也會將**elementFormDefault**和**attributeFormDefault**屬性值設定為 **"不合格"** （這些屬性的預設值）。 這是全域宣告，會影響所有本機專案****（ **** ** ** ** \<** 在架構中的順序>）和屬性（在架構中的 CustomerID、連絡人和訂單）。  
  
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
  
-   **CustomerType**和**OrderType**類型宣告是全域的，因此會包含在架構的目標命名空間中。 如此一來，在** \<Customer>** 元素的宣告和其** \<Order>** 子項目中參考這些型別時，就會指定與目標命名空間相關聯的前置詞。  
  
-   客戶>元素也會包含在架構的目標命名空間中，因為它是架構中的全域元素。 ** \< **  
  
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
  
 這個實例檔會定義 urn： MyNamespace 命名空間，並將前置詞（y0）與它產生關聯。 前置詞僅適用于** \<Customer>** 全域專案。 （元素是全域的，因為它宣告為架構中的** \<xsd： schema>** 元素的子系。）  
  
 前置詞不會套用至本機專案和屬性，因為在架構中， **elementFormDefault**和**attributeFormDefault**屬性的值設定為「不**合格**」。 請注意， ** \<Order>** 專案是本機的，因為它的宣告會顯示為** \<complexType>** 元素的子系，以定義** \<CustomerType 的>** 元素。 同樣地，屬性（**CustomerID**、「**訂單**」和「**連絡人**」）是區域，而非「全域」。  
  
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
  
     範本中的 XPath 查詢會傳回 CustomerID 為1的客戶** \<>** 元素。 請注意，XPath 查詢會針對此查詢中的元素 (而不是屬性) 來指定命名空間前置詞  (如同結構描述中所指定，本機屬性並未限定)。  
  
     針對對應結構描述 (targetNamespace.xml) 所指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\targetNamepsace.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 查詢](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 如果架構指定具有 **"合格"** 值的**elementFormDefault**和**attributeFormDefault**屬性，實例檔將會具有所有本機專案和限定的屬性。 您可以變更先前的架構，以將這些屬性包含在** \<xsd： schema>** 元素中，然後再次執行範本。 因為這些屬性現在也會在此執行個體中限定，所以 XPath 查詢將會變更為可包含命名空間前置詞。  
  
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
  
  
