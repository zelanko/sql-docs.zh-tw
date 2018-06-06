---
title: 序列類型比對 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- sequence type matching [XQuery]
- XQuery, sequence type matching
ms.assetid: 8c56fb69-ca04-4aba-b55a-64ae216c492d
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2ce01e8b2f587527b264a3ea11021257375fb842
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="type-system---sequence-type-matching"></a>類型系統的序列類型比對
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 運算式值一律為 0 個以上項目的序列。 項目可以是不可部份完成的值，或是節點。 序列類型是指將查詢運算式傳回的序列類型與特定類型比對的能力。 例如：  
  
-   如果運算式值為不可部份完成值，您可能想知道它是整數、十進位或字串類型。  
  
-   如果運算式值為 XML 節點，您可能想知道它是註解節點、處理指示節點或文字節點。  
  
-   您可能想知道運算式是傳回 XML 元素或是特定名稱和類型的屬性節點。  
  
 您可以在序列類型比對中使用 `instance of` 布林運算子。 如需有關`instance of`運算式，請參閱[SequenceType 運算式&#40;XQuery&#41;](../xquery/sequencetype-expressions-xquery.md)。  
  
## <a name="comparing-the-atomic-value-type-returned-by-an-expression"></a>比較運算式傳回的不可部份完成值類型  
 如果運算式傳回含有不可部份完成值的序列，則您必須尋找序列中值的類型。 下列範例說明如何使用序列類型語法，來評估運算式傳回的不可部份完成值類型。  
  
### <a name="example-determining-whether-a-sequence-is-empty"></a>範例：判斷序列是否為空  
 **Empty （)** 順序類型可以在序列類型運算式中用來判斷指定的運算式所傳回的序列是否是空的序列。  
  
 在下列範例中，XML 結構描述允許 <`root`> 元素為 Nilled：  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 現在，如果具類型的 XML 執行個體指定 <`root`> 元素的值，`instance of empty()` 會傳回 False。  
  
```  
DECLARE @var XML(SC1)  
SET @var = '<root>1</root>'  
-- The following returns False  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
 如果執行個體中的 <`root`> 元素是 Nilled，其值為空的序列，且 `instance of empty()` 會傳回 True。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" />'  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
### <a name="example-determining-the-type-of-an-attribute-value"></a>範例：判斷屬性值的類型  
 有時候，您或許想在處理之前評估運算式傳回的序列類型。 例如，有一個 XML 結構描述，其中有個節點定義為聯集類型。 在下列範例中，集合中的 XML 結構描述將 `a` 屬性定義為聯集類型，其值可以是十進位或字串類型。  
  
```  
-- Drop schema collection if it exists.  
-- DROP XML SCHEMA COLLECTION SC.  
-- GO  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
  <element name="root">  
    <complexType>  
       <sequence/>  
         <attribute name="a">  
            <simpleType>  
               <union memberTypes="decimal string"/>  
            </simpleType>  
         </attribute>  
     </complexType>  
  </element>  
</schema>'  
GO  
```  
  
 在處理具類型的 XML 執行個體之前，您或許想知道 `a` 屬性值的類型。 在下列範例中，`a` 屬性值是十進位類型。 因此，`, instance of xs:decimal` 傳回 True。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="2.5"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:decimal')  
GO  
```  
  
 現在，請將 `a` 屬性值變更為字串類型。 `instance of xs:string` 將傳回 True。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="Hello"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:string')  
GO  
```  
  
### <a name="example-cardinality-in-sequence-expressions"></a>範例：序列運算式中的基數  
 此範例說明基數在序列運算式中的作用。 下列 XML 結構描述定義的 <`root`> 元素是位元組類型且為 Nillable。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 在下列查詢中，因為運算式會傳回單一位元組類型，所以 `instance of` 傳回 True。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root>111</root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
```  
  
 如果您使 <`root`> 元素成為 Nil，則它的值是空的序列。 也就是說，運算式 `/root[1]` 會傳回空的序列。 因此，`instance of xs:byte` 傳回 False。 請注意，此案例中的預設基數是 1。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
-- result = false  
```  
  
 如果您加入發生指標 (`?`) 來指定基數，則序列運算式會傳回 True。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte? ')   
GO  
-- result = true  
```  
  
 請注意，序列類型運算式中的測試是以兩階段完成：  
  
1.  首先，測試會判斷運算式類型是否符合指定的類型。  
  
2.  如果符合，測試接著會判斷運算式傳回的項目數是否符合指定的發生指標。  
  
 如果都符合，`instance of` 運算式會傳回 True。  
  
### <a name="example-querying-against-an-xml-type-column"></a>範例：針對 xml 類型資料行查詢  
 在下列範例中，查詢針對 Instructions 資料行指定**xml**輸入[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]資料庫。 它是具類型的 XML 資料行，因為它有相關聯的結構描述。 XML 結構描述定義了整數類型的 `LocationID` 屬性。 因此，在序列運算式中， `instance of xs:integer?` ，則傳回 True。  
  
```  
SELECT Instructions.query('   
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
data(/AWMI:root[1]/AWMI:Location[1]/@LocationID) instance of xs:integer?') as Result   
FROM Production.ProductModel   
WHERE ProductModelID = 7  
```  
  
## <a name="comparing-the-node-type-returned-by-an-expression"></a>比較運算式傳回的節點類型  
 如果運算式傳回含有節點的序列，則您必須尋找序列中節點的類型。 下列範例說明如何使用序列類型語法，來評估運算式傳回的節點類型。 您可以使用下列序列類型：  
  
-   **m （)** – 比對序列中的任何項目。  
  
-   **node （)** – 判斷序列是否為節點。  
  
-   **p** – 判斷運算式是否會傳回處理指示。  
  
-   **comment** – 判斷運算式是否會傳回註解。  
  
-   **d** – 判斷運算式是否會傳回文件節點。  
  
 下列範例說明這些序列類型。  
  
### <a name="example-using-sequence-types"></a>範例：使用序列類型  
 在此範例中，會對不具類型的 XML 變數執行數個查詢。 這些查詢會說明序列類型的使用方式。  
  
```  
DECLARE @var XML  
SET @var = '<?xml-stylesheet href="someValue" type="text/xsl" ?>  
<root>text node  
  <!-- comment 1 -->   
  <a>Data a</a>  
  <!-- comment  2 -->  
</root>'  
```  
  
 在第一個查詢中，運算式會傳回 <`a`> 元素的具類型值。 在第二個查詢中，運算式會傳回 <`a`> 元素。 兩者都是項目。 因此，兩個查詢都傳回 True。  
  
```  
SELECT @var.query('data(/root[1]/a[1]) instance of item()')  
SELECT @var.query('/root[1]/a[1] instance of item()')  
```  
  
 下列三個查詢中的所有 XQuery 運算式都會傳回 <`root`> 元素的元素節點子系。 因此，序列類型運算式 `instance of node()` 會傳回 True，其他兩個運算式 (`instance of text()` 和 `instance of document-node()`) 則傳回 False。  
  
```  
SELECT @var.query('(/root/*)[1] instance of node()')  
SELECT @var.query('(/root/*)[1] instance of text()')  
SELECT @var.query('(/root/*)[1] instance of document-node()')   
```  
  
 在下列查詢中，`instance of document-node()` 運算式會傳回 True，因為 <`root`> 元素的父系是文件節點。  
  
```  
SELECT @var.query('(/root/..)[1] instance of document-node()') -- true  
```  
  
 在下列查詢中，運算式會從 XML 執行個體中擷取第一個節點。 因為它是處理指示節點，所以 `instance of processing-instruction()` 運算式會傳回 True。  
  
```  
SELECT @var.query('(/node())[1] instance of processing-instruction()')  
```  
  
### <a name="implementation-limitations"></a>實作限制  
 特定限制如下：  
  
-   **d**語法不支援內容類型。  
  
-   **processing-instruction （name)** 語法不受支援。  
  
## <a name="element-tests"></a>元素測試  
 元素測試是用來比對運算式傳回的元素節點與具有特定名稱和類型的元素節點。 您可以使用這些元素測試：  
  
```  
element ()  
element(ElementName)  
element(ElementName, ElementType?)   
element(*, ElementType?)  
```  
  
## <a name="attribute-tests"></a>屬性測試  
 屬性測試會判斷運算式傳回的屬性是否為屬性節點。 您可以使用這些屬性測試：  
  
 `attribute()`  
  
 `attribute(AttributeName)`  
  
 `attribute(AttributeName, AttributeType)`  
  
## <a name="test-examples"></a>測試範例  
 下列範例說明元素測試和屬性測試都很有用的案例。  
  
### <a name="example-a"></a>範例 A  
 下列 XML 結構描述定義了 `CustomerType` 複雜類型，其中 <`firstName`> 和 <`lastName`> 元素是選擇性的。 對於指定的 XML 執行個體，您必須決定是否保留特定客戶的名字。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="myNS" xmlns:ns="myNS">  
  <complexType name="CustomerType">  
     <sequence>  
        <element name="firstName" type="string" minOccurs="0"   
                  nillable="true" />  
        <element name="lastName" type="string" minOccurs="0"/>  
     </sequence>  
  </complexType>  
  <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS">  
<firstName>SomeFirstName</firstName>  
<lastName>SomeLastName</lastName>  
</x:customer>'  
```  
  
 下列查詢使用 `instance of element (firstName)` 運算式，來判斷 <`customer`> 的第一個子元素是否是名稱為 <`firstName`> 的元素。 在此案例中，它傳回 True。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
     (/x:customer/*)[1] instance of element (firstName)')  
GO  
```  
  
 如果您從執行個體中移除 <`firstName`> 元素，則查詢將傳回 False。  
  
 您也可以使用下列各項：  
  
-   `element(ElementName, ElementType?)` 序列類型語法，如下列查詢所示。 它會比對名稱為 `firstName` 且類型為 `xs:string` 的元素節點 (Nilled 或 Non-nilled)。  
  
    ```  
    SELECT @var.query('declare namespace x="myNS";   
    (/x:customer/*)[1] instance of element (firstName, xs:string?)')  
    ```  
  
-   `element(*, type?)` 序列類型語法，如下列查詢所示。 如果類型是 `xs:string`，不論名稱是什麼，即會符合元素節點。  
  
    ```  
    SELECT @var.query('declare namespace x="myNS"; (/x:customer/*)[1] instance of element (*, xs:string?)')  
    GO  
    ```  
  
### <a name="example-b"></a>範例 B  
 下列範例說明如何判斷運算式傳回的節點是否為具有特定名稱的元素節點。 它會使用**element()** 測試。  
  
 在下列範例中，XML 執行個體中所要查詢的兩個 <`Customer`> 元素分別為兩種不同類型：`CustomerType` 和 `SpecialCustomerType`。 假設您想要知道運算式傳回的 <`Customer`> 元素的類型。 下列 XML 結構描述集合定義了 `CustomerType` 與 `SpecialCustomerType` 類型。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
          targetNamespace="myNS"  xmlns:ns="myNS">  
  <complexType name="CustomerType">  
    <sequence>  
      <element name="firstName" type="string"/>  
      <element name="lastName" type="string"/>  
    </sequence>  
  </complexType>  
  <complexType name="SpecialCustomerType">  
     <complexContent>  
       <extension base="ns:CustomerType">  
        <sequence>  
            <element name="Age" type="int"/>  
        </sequence>  
       </extension>  
     </complexContent>  
    </complexType>  
   <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 此 XML 結構描述集合用來建立具類型**xml**變數。 指派給此變數的 XML 執行個體有兩個 <`customer`> 元素，分別為不同類型。 第一個元素是 `CustomerType` 類型，而第二個元素是 `SpecialCustomerType` 類型。  
  
```  
DECLARE @var XML(SC)  
SET @var = '  
<x:customer xmlns:x="myNS">  
   <firstName>FirstName1</firstName>  
   <lastName>LastName1</lastName>  
</x:customer>  
<x:customer xsi:type="x:SpecialCustomerType" xmlns:x="myNS" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
   <firstName> FirstName2</firstName>  
   <lastName> LastName2</lastName>  
   <Age>21</Age>  
</x:customer>'  
```  
  
 在下列查詢中，`instance of element (*, x:SpecialCustomerType ?)` 運算式會傳回 False，因為運算式傳回的第一個 customer 元素不是 `SpecialCustomerType` 類型。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
    (/x:customer)[1] instance of element (*, x:SpecialCustomerType ?)')  
```  
  
 如果您變更上一個查詢的運算式，並擷取第二個 <`customer`> 元素 (`/x:customer)[2]`)，則 `instance of` 會傳回 True。  
  
### <a name="example-c"></a>範例 C  
 此範例會使用屬性測試。 下列 XML 結構描述定義了 CustomerType 複雜類型，它包含 CustomerID 和 Age 屬性。 Age 屬性是選擇性的。 對於特定的 XML 執行個體，您或許想判斷 Age 屬性是否有出現在 <`customer`> 元素中。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
       targetNamespace="myNS" xmlns:ns="myNS">  
<complexType name="CustomerType">  
  <sequence>  
     <element name="firstName" type="string" minOccurs="0"   
               nillable="true" />  
     <element name="lastName" type="string" minOccurs="0"/>  
  </sequence>  
  <attribute name="CustomerID" type="integer" use="required" />  
  <attribute name="Age" type="integer" use="optional" />  
 </complexType>  
 <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 下列查詢會傳回 True，因為要查詢的 XML 執行個體中，有一個屬性節點的名稱是 `Age`。 在此運算式中，使用了 `attribute(Age)` 屬性測試。 因為屬性沒有順序，所以查詢會使用 FLWOR 運算式來擷取所有屬性，然後使用 `instance of` 運算式來測試每一個屬性。 此範例會先建立 XML 結構描述集合來建立具類型**xml**變數。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS" CustomerID="1" Age="22" >  
<firstName>SomeFName</firstName>  
<lastName>SomeLName</lastName>  
</x:customer>'  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age)) THEN  
        "true"  
        ELSE  
        ()')     
GO  
  
```  
  
 如果您從執行個體中移除選擇性的 `Age` 屬性，則上一個查詢將傳回 False。  
  
 您可以在屬性測試內指定屬性名稱和類型 (`attribute(name,type)`)。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age, xs:integer)) THEN  
        "true"  
        ELSE  
        ()')  
```  
  
 或者，您可以指定`attribute(*, type)`序列類型語法。 如果屬性類型符合指定的類型，不論名稱是什麼，即會符合屬性節點。  
  
### <a name="implementation-limitations"></a>實作限制  
 特定限制如下：  
  
-   在元素測試中，類型名稱後面必須發生指標 (**？**)。  
  
-   **element （ElementName，TypeName）**不支援。  
  
-   **項目 (\*，TypeName)** 不支援。  
  
-   **schema-element()** 不支援。  
  
-   **schema-attribute(AttributeName)** 不支援。  
  
-   明確查詢**xsi: type**或**xsi: nil**不支援。  
  
## <a name="see-also"></a>另請參閱  
 [類型系統&#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
