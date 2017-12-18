---
title: "產生內嵌 XSD 結構描述 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XSD schemas [SQL Server]
- XMLSCHEMA option
- schemas [SQL Server], XML
- XDR schemas
- FOR XML clause, inline XSD schema generation
- inline XSD schema generation [SQL Server]
- XMLDATA option
ms.assetid: 04b35145-1cca-45f4-9eb7-990abf2e647d
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e0b7f3b2064b37cecffb2ae84532731ee742e5ea
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="generate-an-inline-xsd-schema"></a>產生內嵌 XSD 結構描述
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] 在 FOR XML 子句中，您可以要求您的查詢將內嵌結構描述連同查詢結果一起傳回。 如果您要的是 XDR 結構描述，請在 FOR XML 子句中使用 XMLDATA 關鍵字。 而如果您要的是 XSD 結構描述，則請使用 XMLSCHEMA 關鍵字。  
  
 此主題描述 XMLSCHEMA 關鍵字，並說明所產生之內嵌 XSD 結構描述的結構。 以下是要求內嵌結構描述時的一些限制：  
  
-   您只能在 RAW 和 AUTO 模式中指定 XMLSCHEMA，但不能在 EXPLICIT 模式中指定。  
  
-   如果巢狀 FOR XML 查詢指定了 TYPE 指示詞，則查詢結果會是 **xml** 類型，但此結果會當做不具類型之 XML 資料的執行個體來處理。 如需詳細資訊，請參閱 [XML 資料 &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)。  
  
 當您在 FOR XML 查詢中指定 XMLSCHEMA 時，會同時收到結構描述和 XML 資料做為查詢結果。 此資料的每一個最上層元素使用預設命名空間宣告來參考上一個結構描述，此宣告再參考內嵌結構描述的目標命名空間。  
  
 例如：  
  
```  
<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">  
  <xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="Production.ProductModel">  
    <xsd:complexType>  
      <xsd:attribute name="ProductModelID" type="sqltypes:int" use="required" />  
      <xsd:attribute name="Name" use="required">  
        <xsd:simpleType sqltypes:sqlTypeAlias="[AdventureWorks2012].[dbo].[Name]">  
          <xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033" sqltypes:sqlCompareOptions="IgnoreCase IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">  
            <xsd:maxLength value="50" />  
          </xsd:restriction>  
        </xsd:simpleType>  
      </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
<Production.ProductModel xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" ProductModelID="1" Name="Classic Vest" />  
```  
  
 此結果包含 XML 結構描述和 XML 結果。 結果中的 <`ProductModel`> 最上層元素使用預設命名空間宣告 xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1"，來參考結構描述。  
  
 結果的結構描述部份可能包含了描述多個命名空間的多個結構描述文件。 至少會傳回下列兩份結構描述文件：  
  
-   一份結構描述文件用於 **Sqltypes** 命名空間，並對其傳回基底 SQL 類型。  
  
-   另一份結構描述文件描述 FOR XML 查詢結果的外觀。  
  
 另外，如果查詢結果中包含任何具類型的 **xml** 資料類型，則與這些具類型的 **xml** 資料類型相關聯的結構描述也會包含在內。  
  
 在描述 FOR XML 結果外觀的結構描述文件中，目標命名空間包含固定部分，以及會自動遞增的數值部分。 此命名空間的格式如下所示，其中 *n* 是正整數。 例如，在上一個查詢中，urn:schemas-microsoft-com:sql:SqlRowSet1 就是目標命名空間。  
  
```  
urn:schemas-microsoft-com:sql:SqlRowSetn  
```  
  
 每次執行都會導致結果中的目標命名空間發生改變，但這可能不是您想要的。 例如，如果您查詢產生的 XML，目標命名空間中的變更會要求您更新查詢。 您可在 XMLSCHEMA 選項加入 FOR XML 子句時，選擇性地指定目標命名空間。 產生的 XML 將會包含您所提供的命名空間，並且維持不變，不論您執行查詢多少次都一樣。  
  
```  
SELECT ProductModelID, Name  
FROM   Production.ProductModel  
WHERE ProductModelID=1  
FOR XML AUTO, XMLSCHEMA ('MyURI')  
```  
  
## <a name="entity-elements"></a>實體元素  
 若要討論針對查詢結果而產生之 XSD 結構描述結構的詳細資料，必須先說明實體元素  
  
 由 FOR XML 查詢所傳回之 XML 資料中的實體元素，是從資料表產生的元素，而非從資料行產生。 例如，下列 FOR XML 查詢會從 `Person` 資料庫中的 `AdventureWorks2012` 資料表傳回連絡資訊。  
  
```  
SELECT BusinessEntityID, FirstName  
FROM Person.Person  
WHERE BusinessEntityID = 1  
FOR XML AUTO, ELEMENTS  
```  
  
 以下是結果：  
  
 `<Person>`  
  
 `<BusinessEntityID>1</BusinessEntityID>`  
  
 `<FirstName>Ken</FirstName>`  
  
 `</Person>`  
  
 在此結果中，<`Person`> 是實體元素。 在 XML 結果中可能有多個實體元素，每一個元素在內嵌 XSD 結構描述中都有全域宣告。 例如，下列查詢擷取特定訂單的銷售訂單標頭和詳細資訊。  
  
```  
SELECT  SalesOrderHeader.SalesOrderID, ProductID, OrderQty  
FROM    Sales.SalesOrderHeader, Sales.SalesOrderDetail  
WHERE   SalesOrderHeader.SalesOrderID = SalesOrderDetail.SalesOrderID  
AND     SalesOrderHeader.SalesOrderID=5001  
FOR XML AUTO, ELEMENTS, XMLSCHEMA  
```  
  
 因為此查詢指定 ELEMENTS 指示詞，所以產生的 XML 是元素中心的。 此查詢也指定 XMLSCHEMA 指示詞。 因此，會傳回內嵌 XSD 結構描述。 以下是結果：  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="Sales.SalesOrderHeader">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="SalesOrderID" type="sqltypes:int" />`  
  
 `<xsd:element ref="schema:Sales.SalesOrderDetail" minOccurs="0" maxOccurs="unbounded" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `<xsd:element name="Sales.SalesOrderDetail">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="OrderQty" type="sqltypes:smallint" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 請注意下列項目是從上一個查詢而來：  
  
-   在結果中，<`SalesOrderHeader`> 和 <`SalesOrderDetail`> 是實體元素。 因為它們都是實體元素，所以在結構描述中已有全域宣告。 也就是說，此宣告會出現在 <`Schema`> 元素內的最上層。  
  
-   <`SalesOrderID`>、<`ProductID`> 和 <`OrderQty`> 不是實體元素，因為它們對應到資料行。 因為 ELEMENTS 指示詞的緣故，資料行的資料是以 XML 中的元素傳回。 這些元素對應至實體元素之複雜類型的本機元素。 請注意，如果未指定 ELEMENTS 指示詞，則 `SalesOrderID`、 `ProductID` 和 `OrderQty` 值會對應至相對應實體元素之複雜類型的本機屬性。  
  
## <a name="attribute-name-clashes"></a>屬性名稱衝突  
 以下討論是以 `CustOrder` 和 `CustOrderDetail` 資料表為基礎。 若要測試下列範例，請建立這些資料表並加入您自己的範例資料：  
  
```  
CREATE TABLE CustOrder (OrderID int primary key, CustomerID int)  
GO  
CREATE TABLE CustOrderDetail (OrderID int, ProductID int, Qty int)  
GO  
```  
  
 在 FOR XML 中，有時候相同的名稱會表示不同的屬性 (Property) 或屬性 (Attribute)。 例如，下列屬性中心的 RAW 模式查詢會產生兩個屬性，其名稱都是 OrderID。 這樣會產生錯誤。  
  
```  
SELECT CustOrder.OrderID,   
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
FROM   dbo.CustOrder, dbo.CustOrderDetail  
WHERE  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA  
```  
  
 不過，因為兩個元素具有相同名稱是可接受的，所以，您可以加入 ELEMENTS 指示詞來解決此問題：  
  
```  
SELECT CustOrder.OrderID,  
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
from   dbo.CustOrder, dbo.CustOrderDetail  
where  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA, ELEMENTS  
```  
  
 以下是結果。 請注意內嵌 XSD 結構描述中，OrderID 元素定義了兩次。 其中一個宣告將 minOccurs 設為 0，對應於 CustOrderDetail 資料表的 OrderID；第二個宣告對應於 `CustOrder` 資料表的 OrderID 主索引鍵資料行，其中的 minOccurs 預設為 1。  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" />`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" minOccurs="0" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
## <a name="element-name-clashes"></a>元素名稱衝突  
 在 FOR XML 中，可以使用相同的名稱來表示兩個子元素。 例如，下列查詢會擷取產品的 ListPrice 和 DealerPrice 值，但此查詢對這兩個資料行指定相同的別名：Price。 因此，產生的資料列集將具有兩個相同名稱的資料行。  
  
### <a name="case-1-both-subelements-are-nonkey-columns-of-the-same-type-and-can-be-null"></a>案例 1：兩個子元素都是相同類型的非索引鍵之索引資料行，而且可以是 NULL  
 在下列查詢中，兩個子元素都是相同類型的非索引鍵之索引資料行，而且可以是 NULL。  
  
```  
DROP TABLE T  
go  
CREATE TABLE T (ProductID int primary key, ListPrice money, DealerPrice money)  
go  
INSERT INTO T values (1, 1.25, null)  
go  
  
SELECT ProductID, ListPrice Price, DealerPrice Price  
FROM   T  
for    XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 這是所產生的對應 XML。 以下只顯示內嵌 XSD 的一部分：  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" minOccurs="0" maxOccurs="2" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `</row>`  
  
 請注意內嵌 XSD 結構描述中的下列各項：  
  
-   ListPrice 和 DealerPrice 都屬於相同類型 `money`，而且在資料表中都可以是 NULL。 因此，由於它們可能不會在產生的 XML 中傳回，所以在 <`row`> 元素 (其 minOccurs=0 且 maxOccurs=2) 的複雜類型宣告中，只有一個 <`Price`> 子元素。  
  
-   結果，因為 `DealerPrice` 值在資料表中是 NULL，所以只有 `ListPrice` 會做為 <`Price`> 元素傳回。 如果將 `XSINIL` 參數加入 ELEMENTS 指示詞，您會收到兩個元素，它們將對應至 DealerPrice 的 <`Price`> 元素的 `xsi:nil` 值設定為 TRUE。 您也會在內嵌 XSD 結構描述的 <`row`> 複雜類型定義中，接收到兩個 <`Price`> 子元素，這兩個子元素的 `nillable` 屬性都設為 TRUE。 以下片段是部分結果：  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `<Price xsi:nil="true" />`  
  
 `</row>`  
  
### <a name="case-2-one-key-and-one-nonkey-column-of-the-same-type"></a>案例 2：類型相同的索引鍵資料行和非索引鍵之索引資料行  
 下列查詢說明類型相同的索引鍵資料行和非索引鍵之索引資料行。  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 int, Col3 nvarchar(20))  
go  
INSERT INTO T VALUES (1, 1, 'test')  
go   
```  
  
 下列針對資料表 **T** 的查詢，為 Col1 和 Col2 指定了相同別名，其中 Col1 是不能為 Null 的主索引鍵，而 Col2 則可以是 Null。 這會產生兩個同層級元素，兩者都是 <`row`> 元素的子系。  
  
```  
SELECT Col1 as Col, Col2 as Col, Col3  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 以下是結果。 以下只顯示內嵌 XSD 結構描述的一部份：  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="Col3" minOccurs="0">`  
  
 `<xsd:simpleType>`  
  
 `<xsd:restriction base="sqltypes:nvarchar"`  
  
 `sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth"`  
  
 `sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `</xsd:element>`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col>1</Col>`  
  
 `<Col>1</Col>`  
  
 `<Col3>test</Col3>`  
  
 `</row>`  
  
 請注意，在內嵌 XSD 結構描述中，對應於 Col2 的 <`Col`> 元素，其 minOccurs 是設為 0。  
  
### <a name="case-3-both-elements-of-different-types-and-corresponding-columns-can-be-null"></a>案例 3：不同類型的兩個元素，及其對應資料行都可以是 NULL  
 下列查詢是針對案例 2 所顯示的範例資料表而指定：  
  
```  
SELECT Col1, Col2 as Col, Col3 as Col  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 下列查詢中，Col2 和 Col3 使用相同別名。 這會產生兩個具有相同名稱的同層級元素，且在結果中這兩者都是 <`raw`> 元素的子系。 這兩個資料行屬於不同類型，而且兩者都可以是 NULL。 以下是結果。 只顯示一部份的內嵌 XSD 結構描述。  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:simpleType name="Col1">`  
  
 `<xsd:restriction base="sqltypes:int" />`  
  
 `</xsd:simpleType>`  
  
 `<xsd:simpleType name="Col2">`  
  
 `<xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col1" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" minOccurs="0" maxOccurs="2" type="xsd:anySimpleType" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col1>1</Col1>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col1">1</Col>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col2">test</Col>`  
  
 `</row>`  
  
 請注意內嵌 XSD 結構描述中的下列各項：  
  
-   因為 Col2 和 Col3 可以是 NULL，所以 <`Col`> 元素宣告將 minOccurs 指定為 0，將 maxOccurs 指定為 2。  
  
-   因為這兩個 <`Col`> 元素是同層級，所以在結構描述中有一個元素宣告。 同時，因為兩元素也都是不同類型 (雖然都是簡單類型)，所以結構描述中的元素類型是 `xsd:anySimpleType`。 在結果中，每一個執行個體類型是由 `xsi:type` 屬性加以識別。  
  
-   在結果中，<`Col`> 元素的每一個執行個體是使用 `xsi:type` 屬性來參考其執行個體類型。  
  
  
