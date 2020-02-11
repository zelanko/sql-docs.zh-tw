---
title: SequenceType 運算式（XQuery） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- SequenceType expressions
- instance of operator [XQuery]
- expressions [XQuery], SequenceType
- cast as operator
ms.assetid: ad3573da-d820-4d1c-81c4-a83c4640ce22
author: rothja
ms.author: jroth
ms.openlocfilehash: e7c3cdf33b0765ba50e5553f3bc31fd5c69312e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67946287"
---
# <a name="sequencetype-expressions-xquery"></a>時序類型運算式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 XQuery 中，值永遠是一種時序。 值的類型又稱為時序類型。 序列類型可用於 XQuery 運算式**的實例**中。 當您需要參考 XQuery 運算式中的類型時，就會使用 XQuery 規格中所描述的 SequenceType 語法。  
  
 不可部分完成的類型名稱也可以在**轉換**中當做 XQuery 運算式使用。 在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中，部分支援 SequenceTypes 的**實例**和**cast 做為**XQuery 運算式。  
  
## <a name="instance-of-operator"></a>運算子的執行個體  
 運算子的**實例**可以用來判斷指定之運算式值的動態或執行時間類型。 例如：  
  
```  
  
Expression instance of SequenceType[Occurrence indicator]  
```  
  
 請注意， `instance of`運算子`Occurrence indicator`會指定產生的序列中的基數、專案數目。 若未指定，會將基數假設為 1。 在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中，只支援問號（**？）** 出現次數指標。 **？** 出現指示器指出`Expression`可以傳回零個或一個專案。 如果 **？** 指定出現指示器時， `instance of`會在`Expression`類型符合指定`SequenceType`的時傳回 True，不論是否`Expression`傳回單一或空的序列。  
  
 如果 **？** 未指定發生次數指標， `sequence of`只有當`Expression`類型符合指定的`Type`並`Expression`傳回 singleton 時，才會傳回 True。  
  
 **注意**中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]不支援加號**+**（）和星號（**&#42;**）出現指示器。  
  
 下列範例說明如何使用 XQuery 運算子的**實例**。  
  
### <a name="example-a"></a>範例 A  
 下列範例會建立**xml**類型變數，並針對它指定查詢。 查詢運算式指定 `instance of` 運算子，以判斷第一個運算元所傳回的動態類型值是否符合第二個運算元所指定的類型。  
  
 下列查詢會傳回 True，因為125值是指定之類型的實例**xs： integer**：  
  
```  
declare @x xml  
set @x=''  
select @x.query('125 instance of xs:integer')  
go  
```  
  
 下列查詢會傳回 True，因為在第一個運算元中由運算式 /a[1] 所傳回的值是元素。  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('/a[1] instance of element()')  
go  
```  
  
 同樣地，`instance of` 會在下列查詢中傳回 True，因為在第一個運算式中的運算式值類型是屬性。  
  
```  
declare @x xml  
set @x='<a attr1="x">1</a>'  
select @x.query('/a[1]/@attr1 instance of attribute()')  
go  
```  
  
 在下列範例中，`data(/a[1]` 運算式會傳回不可部份完成值，其類型為 xdt:untypedAtomic。 因此，`instance of` 會傳回 True。  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('data(/a[1]) instance of xdt:untypedAtomic')  
go  
```  
  
 在下列查詢中，`data(/a[1]/@attrA` 運算式會傳回不具類型的不可部份完成值。 因此，`instance of` 會傳回 True。  
  
```  
declare @x xml  
set @x='<a attrA="X">1</a>'  
select @x.query('data(/a[1]/@attrA) instance of xdt:untypedAtomic')  
go  
```  
  
### <a name="example-b"></a>範例 B  
 在此範例中，您正在查詢 AdventureWorks 範例資料庫中具 XML 類型的資料行。 與正在查詢的資料行關聯的 XML 結構描述集合，將會提供類型資訊。  
  
 在運算式中， **data （）** 會根據與資料行相關聯的架構，傳回類型為 xs： String 之 ProductModelID 屬性的具類型值。 因此，`instance of` 會傳回 True。  
  
```  
SELECT CatalogDescription.query('  
   declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   data(/PD:ProductDescription[1]/@ProductModelID) instance of xs:string  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 如需詳細資訊，請參閱[比較具類型的 xml 與](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)不具類型的 xml。  
  
 下列查詢會 usetheBoolean `instance of`運算式，以判斷 LocationID 屬性是否為 xs： integer 類型：  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   /AWMI:root[1]/AWMI:Location[1]/@LocationID instance of attribute(LocationID,xs:integer)  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 下列查詢是針對 CatalogDescription 類型的 XML 資料行所指定。 與此資料行關聯的 XML 結構描述集合，將會提供類型資訊。  
  
 此查詢使用 `element(ElementName, ElementType?)` 運算式中的 `instance of` 測試來驗證 `/PD:ProductDescription[1]` 是否會傳回特定名稱與類型的元素節點。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /PD:ProductDescription[1] instance of element(PD:ProductDescription, PD:ProductDescription?)  
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 此查詢會傳回 True。  
  
### <a name="example-c"></a>範例 C  
 在使用聯集類型時，`instance of` 中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 運算式有一個限制：具體而言，當元素或屬性的類型是聯集類型時，`instance of` 可能無法判斷正確的類型。 因此，除非 SequenceType 中所使用的不可部份完成類型是 simpleType 階層中運算式之實際類型的最高父系，否則查詢會傳回 False。 也就是，在 SequenceType 中所指定的不可部份完成類型必須是 anySimpleType 的直接子系。 如需類型階層的詳細資訊，請參閱[XQuery 中的類型轉換規則](../xquery/type-casting-rules-in-xquery.md)。  
  
 下個查詢範例將執行下列動作：  
  
-   以聯集類型建立 XML 結構描述集合，例如，定義在類型中的整數或字串類型。  
  
-   使用 XML 架構集合宣告具類型的**xml**變數。  
  
-   指派範例 XML 執行個體給變數。  
  
-   在處理聯集類型時，查詢變數以說明 `instance of` 行為。  
  
 此查詢如下：  
  
```  
CREATE XML SCHEMA COLLECTION MyTestSchema AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns">  
<simpleType name="MyUnionType">  
<union memberTypes="integer string"/>  
</simpleType>  
<element name="TestElement" type="ns:MyUnionType"/>  
</schema>'  
Go  
```  
  
 下列查詢會傳回 False，因為在 `instance of` 運算式中指定的 SequenceType 不是指定運算式中實際類型的最高父系。 也就是說，<`TestElement`> 的值是整數類型。 最高父系是 xs:decimal。 不過，並未將它指定為 `instance of` 運算子的第二個運算元。  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
  
SELECT @var.query('declare namespace ns="http://ns"   
   data(/ns:TestElement[1]) instance of xs:integer')  
go  
```  
  
 因為 xs:integer 的最高父系是 xs:decimal，如果您修改查詢並將 xs:decimal 指定為查詢中的 SequenceType，查詢將會傳回 True。  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
SELECT @var.query('declare namespace ns="http://ns"     
   data(/ns:TestElement[1]) instance of xs:decimal')  
go  
```  
  
### <a name="example-d"></a>範例 D  
 在此範例中，您會先建立 XML 架構集合，並使用它來輸入**xml**變數。 然後會查詢具類型的**xml**變數以說明`instance of`功能。  
  
 下列 XML 架構集合會定義簡單類型 myType，以及類型為 myType 的元素 <`root`>：  
  
```  
drop xml schema collection SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="myNS" xmlns:ns="myNS"  
xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
      <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
           <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
Go  
```  
  
 現在，建立具類型的**xml**變數並加以查詢：  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
   data(/ns:root[1]) instance of ns:myType')  
go  
```  
  
 因為 myType 類型是由 varchar 類型的限制所衍生出來，而 varchar 類型是定義在 sqltypes 結構描述中，所以 `instance of` 也會傳回 True。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
go  
```  
  
### <a name="example-e"></a>範例 E  
 在下列範例中，運算式會擷取 IDREFS 屬性的其中一個值，並使用 `instance of` 來判斷值是否為 IDREF 類型。 本範例將執行下列動作：  
  
-   建立 XML `Customer`架構集合，其中 <> 元素具有**OrderList** IDREFS 類型屬性，而且 <`Order`> 專案具有「**訂單**識別碼」類型屬性。  
  
-   建立具類型的**xml**變數，並將範例 xml 實例指派給它。  
  
-   針對變數指定查詢。 查詢運算式會從第一個 <`Customer`> 的 OrderList IDRERS type 屬性中，抓取第一個訂單識別碼的值。 所擷取的值是 IDREF 類型。 因此，`instance of` 會傳回 True。  
  
```  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
  
select @x.query(' declare namespace CustOrders="Customers";   
 data(CustOrders:Customers/Customer[1]/@OrderList)[1] instance of xs:IDREF ? ') as XML_result  
```  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   與`instance of`運算子比較時，不支援**架構元素（）** 和**架構屬性（）** 序列類型。  
  
-   例如，完整時序不支援 `(1,2) instance of xs:integer*`。  
  
-   當您使用**element （）** 序列類型的形式指定型別名稱（例如`element(ElementName, TypeName)`）時，型別必須以問號（？）限定。 例如，`element(Title, xs:string?)` 指出元素可能為 Null。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]不支援使用`instance of`來偵測**xsi： nil**屬性的執行時間。  
  
-   如果在 `Expression` 中的值是源自於聯集類型的元素或屬性，則 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 只能識別基本類型，而無法識別衍生值類型的衍生類型。 例如，如果 <`e1`> 定義為具有靜態類型（xs： integer | xs： string），下列將會傳回 False。  
  
    ```  
    data(<e1>123</e1>) instance of xs:integer  
    ```  
  
     然而，`data(<e1>123</e1>) instance of xs:decimal` 將會傳回 True。  
  
-   針對**處理指示（）** 和**檔節點（）** 序列類型，只允許不含引數的表單。 例如，允許 `processing-instruction()` 但不允許 `processing-instruction('abc')`。  
  
## <a name="cast-as-operator"></a>cast as 運算子  
 **Cast as**運算式可以用來將值轉換成特定的資料類型。 例如：  
  
```  
  
Expression cast as  AtomicType?  
```  
  
 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，在 `AtomicType` 後面需要問號 (?)。 例如，如下列查詢所示， `"2" cast as xs:integer?`會將字串值轉換為整數：  
  
```  
declare @x xml  
set @x=''  
select @x.query('"2" cast as xs:integer?')  
```  
  
 在下列查詢中， **data （）** 會傳回 ProductModelID 屬性的具類型值，也就是字串類型。 `cast as`運算子會將值轉換為 xs： integer。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('  
   data(/PD:ProductDescription[1]/@ProductModelID) cast as xs:integer?  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 在此查詢中，不需要明確使用**資料（）** 。 
  `cast as` 運算式可在輸入運算式上執行隱含的不可部份完成。  
  
### <a name="constructor-functions"></a>建構函式  
 您可以使用不可部份完成類型的建構函式。 例如，您可以使用`cast as` **xs： integer （）** 函數（如下列範例所示），而不是使用運算子`"2" cast as xs:integer?`：  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:integer("2")')  
```  
  
 下列範例會傳回等於 2000-01-01Z 的 xs:date 值。  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:date("2000-01-01Z")')  
```  
  
 您也可以使用使用者自訂不可部份完成類型的建構函式。 例如，如果與 XML 資料類型相關聯的 XML 架構集合定義了簡單的類型，則可以使用**myType （）** 函數來傳回該類型的值。  
  
#### <a name="implementation-limitations"></a>實作限制  
  
-   不支援 XQuery 運算式**typeswitch**、**可轉換**和**treat** 。  
  
-   **轉換成**需要問號（？）在不可部分完成的類型之後。  
  
-   **xs： QName**不支援做為轉換的類型。 請改用**展開的-QName** 。  
  
-   **xs： date**、 **xs： time**和**xs： datetime**需要一個以 Z 表示的時區。  
  
     下列查詢會失敗，因為未指定時區。  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25")}</a>')  
    go  
    ```  
  
     只要在值中加入 Z 時區指標，查詢就可成功執行。  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25Z")}</a>')  
    go  
    ```  
  
     以下是結果：  
  
    ```  
    <a>2002-05-25Z</a>  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 運算式](../xquery/xquery-expressions.md)   
 [輸入 System &#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
