---
title: 範例:使用 OPENXML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ColPattern [XML in SQL Server]
- XML [SQL Server], mapping data
- OPENXML statement, about OPENXML statement
- overflow in XML document [SQL Server]
- mapping XML data [SQL Server]
- combining attribute-centric and element centric mapping
- unconsumed data
- attribute-centric mapping
- column patterns [XML in SQL Server]
- XML [SQL Server], overflow handling
- row patterns [XML in SQL Server]
- rowpattern [XML in SQL Server]
- flags parameter
- element-centric mapping [SQL Server]
- edge tables
ms.assetid: 689297f3-adb0-4d8d-bf62-cfda26210164
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9887a9af6735b54a78dd72ed3a90aeff70c7990f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63205112"
---
# <a name="examples-using-openxml"></a>範例:使用 OPENXML
  在此主題下的範例將說明如何使用 OPENXML 來建立 XML 文件的資料列集檢視。 如需 OPENXML 語法的相關資訊，請參閱 [OPENXML &#40;Transact-SQL&#41;](/sql/t-sql/functions/openxml-transact-sql)。 範例中將說明 OPENXML 的各個方面，但是不指定 OPENXML 的中繼屬性。 如需如何指定 OPENXML 的中繼屬性的詳細資訊，請參閱 [在 OPENXML 中指定中繼屬性](specify-metaproperties-in-openxml.md)。  
  
## <a name="examples"></a>範例  
 在擷取資料時， *rowpattern* 是用來識別 XML 文件中決定資料列的節點。 另外， *rowpattern* 是以 XPath 模式語言表示，該語言使用於 MSXML XPath 實作中。 例如，如果模式結尾是元素或屬性，則會為 *rowpattern*所選取的每一個元素或屬性節點建立一個資料列。  
  
 *flags* 值提供預設對應。 若在 *SchemaDeclaration* 中未指定 *ColPattern*，則假設為 *flags* 中所指定的對應。 若在 *SchemaDeclaration* 中指定 *ColPattern* ，則略過 *flags*值。 指定的 *ColPattern* 將決定處理溢位和未使用資料的對應 (屬性中心或元素中心) 以及行為。  
  
### <a name="a-executing-a-simple-select-statement-with-openxml"></a>A. 以 OPENXML 執行簡單的 SELECT 陳述式  
 此範例中的 XML 文件是由 <`Customer`>、<`Order`> 和 <`OrderDetail`> 元素組成。 OPENXML 陳述式所擷取的客戶資訊是來自於 XML 文件中的兩個資料行資料列集：**CustomerID** 和 **ContactName**。  
  
 首先，呼叫 **sp_xml_preparedocument** 預存程序以取得文件控制代碼。 接著將此文件控制代碼傳遞至 OPENXML。  
  
 OPENXML 陳述式說明下列各項：  
  
-   *rowpattern* (/ROOT/Customer) 識別要處理的 <`Customer`> 節點。  
  
-   *flags* 參數值設為 **1** ，表示屬性中心的對應。 因此，XML 屬性對應至 *SchemaDeclaration*中定義之資料列集的資料行。  
  
-   在 WITH 子句內的 *SchemaDeclaration*中，指定的 *ColName* 值與對應的 XML 屬性名稱相符。 因此不會在 *SchemaDeclaration* 中指定 *ColPattern*參數。  
  
 然後，SELECT 陳述式擷取由 OPENXML 所提供之資料列集內的所有資料行。  
  
```  
DECLARE @DocHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
          OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
          OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @DocHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@DocHandle, '/ROOT/Customer',1)  
      WITH (CustomerID  varchar(10),  
            ContactName varchar(20))  
EXEC sp_xml_removedocument @DocHandle  
```  
  
 以下是結果：  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 由於 <`Customer`> 元素不具有任何子元素，若相同的 SELECT 陳述式以 *flags* 設為 **2** 來執行 (表示元素中心的對應)，則兩個客戶的 **CustomerID** 及 **ContactName** 值將以 NULL 傳回。  
  
 @xmlDocument 也可以是 **ML** 類型或 **(n)varchar(max)** 類型。  
  
 如果 XML 文件中的 <`CustomerID`> 和 <`ContactName`> 是子元素，元素中心的對應會擷取這些值。  
  
```  
DECLARE @XmlDocumentHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer>  
   <CustomerID>VINET</CustomerID>  
   <ContactName>Paul Henriot</ContactName>  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer>     
   <CustomerID>LILAS</CustomerID>  
   <ContactName>Carlos Gonzlez</ContactName>  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @XmlDocumentHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT    *  
FROM      OPENXML (@XmlDocumentHandle, '/ROOT/Customer',2)  
           WITH (CustomerID  varchar(10),  
                 ContactName varchar(20))  
EXEC sp_xml_removedocument @XmlDocumentHandle  
```  
  
 以下是結果：  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 請注意， **sp_xml_preparedocument** 傳回的文件控制代碼是對批次的期間有效，而不是對工作階段有效。  
  
### <a name="b-specifying-colpattern-for-mapping-between-rowset-columns-and-the-xml-attributes-and-elements"></a>B. 指定 ColPattern 來進行資料列集資料行與 XML 屬性和元素之間的對應  
 此範例將說明如何在選用的 *ColPattern* 參數中指定 XPath 模式，以提供資料列集資料行與 XML 屬性和元素之間的對應。  
  
 此範例中的 XML 文件是由 <`Customer`>、<`Order`> 和 <`OrderDetail`> 元素組成。 OPENXML 陳述式所擷取的客戶及訂單資訊是來自於 XML 文件中的資料列集 (**CustomerID**、**OrderDate**、**ProdID** 及 **Qty**)。  
  
 首先，呼叫 **sp_xml_preparedocument** 預存程序以取得文件控制代碼。 接著將此文件控制代碼傳遞至 OPENXML。  
  
 OPENXML 陳述式說明下列各項：  
  
-   *rowpattern* (/ROOT/Customer/Order/OrderDetail) 識別要處理的 <`OrderDetail`> 節點。  
  
 舉例來說，*flags* 參數值設為 **2**，表示元素中心的對應。 不過， *ColPattern* 中指定的對應會覆寫此對應。 也就是說， *ColPattern* 中所指定的 XPath 模式會將資料列集的資料行對應到屬性。 這會導致屬性中心的對應。  
  
 在 WITH 子句內的 *SchemaDeclaration*中，亦使用 *ColName* 與 *ColType* 參數來指定 *ColPattern* 。 選用的 *ColPattern* 是指定的 XPath 模式，它表示下列各項：  
  
-   資料列集的 **OrderID**、**CustomerID** 和 **OrderDate** 資料行對應到 *rowpattern* 所識別節點的父系之屬性，且 *rowpattern* 識別 <`OrderDetail`> 節點。 因此，**CustomerID** 和 **OrderDate** 資料行對應到 <`Order`> 元素的 **CustomerID** 和 **OrderDate** 屬性。  
  
-   資料列集的 **ProdID** 及 **Qty** 資料行對應至 *rowpattern* 中所識別節點的 **ProductID** 及 **Quantity** 屬性。  
  
 然後，SELECT 陳述式擷取由 OPENXML 所提供之資料列集內的所有資料行。  
  
```  
DECLARE @XmlDocumentHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @XmlDocumentHandle OUTPUT, @XmlDocument  
-- Execute a SELECT stmt using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@XmlDocumentHandle, '/ROOT/Customer/Order/OrderDetail',2)  
WITH (OrderID     int         '../@OrderID',  
      CustomerID  varchar(10) '../@CustomerID',  
      OrderDate   datetime    '../@OrderDate',  
      ProdID      int         '@ProductID',  
      Qty         int         '@Quantity')  
EXEC sp_xml_removedocument @XmlDocumentHandle  
```  
  
 以下是結果：  
  
```  
OrderID CustomerID        OrderDate          ProdID    Qty  
-------------------------------------------------------------  
10248    VINET     1996-07-04 00:00:00.000     11       12  
10248    VINET     1996-07-04 00:00:00.000     42       10  
10283    LILAS     1996-08-16 00:00:00.000     72        3  
```  
  
 指定為 *ColPattern* 的 XPath 模式也可以指定為將 XML 元素對應到資料列集資料行。 這會導致元素中心的對應。 在下列範例中，XML 文件 <`CustomerID`> 和 <`OrderDate`> 是 <`Orders`> 元素的子元素。 由於 *ColPattern* 覆寫了 *flags* 參數中所指定的對應，因此在 OPENXML 中並未指定 *flags* 參數。  
  
```  
DECLARE @docHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order EmployeeID="5" >  
      <OrderID>10248</OrderID>  
      <CustomerID>VINET</CustomerID>  
      <OrderDate>1996-07-04T00:00:00</OrderDate>  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order  EmployeeID="3" >  
      <OrderID>10283</OrderID>  
      <CustomerID>LILAS</CustomerID>  
      <OrderDate>1996-08-16T00:00:00</OrderDate>  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer/Order/OrderDetail')  
WITH (CustomerID  varchar(10)   '../CustomerID',  
      OrderDate   datetime      '../OrderDate',  
      ProdID      int           '@ProductID',  
      Qty         int           '@Quantity')  
EXEC sp_xml_removedocument @docHandle  
```  
  
### <a name="c-combining-attribute-centric-and-element-centric-mapping"></a>C. 結合以屬性為主及以元素為主的對應  
 在此範例中， *flags* 參數設為 **3** ，表示將套用屬性中心和元素中心的兩種對應。 在此情況下，會先套用屬性中心的對應，然後所有尚未處理的資料行則套用元素中心的對應。  
  
```  
DECLARE @docHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument =N'<ROOT>  
<Customer CustomerID="VINET"  >  
     <ContactName>Paul Henriot</ContactName>  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
          OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" >   
     <ContactName>Carlos Gonzlez</ContactName>  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
          OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @XmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer',3)  
      WITH (CustomerID  varchar(10),  
            ContactName varchar(20))  
EXEC sp_xml_removedocument @docHandle  
```  
  
 以下是結果：  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 屬性中心的對應套用於 **CustomerID**。 <`Customer`> 元素中沒有 **ContactName** 屬性。 因此，套用元素中心的對應。  
  
### <a name="d-specifying-the-text-xpath-function-as-colpattern"></a>D. 指定 text() XPath 函數為 ColPattern  
 此範例中的 XML 文件是由 <`Customer`> 和 <`Order`> 元素組成。 OPENXML 陳述式擷取的資料列集是由 <`Order`> 元素的 **oid** 屬性、*rowpattern* 所識別的節點父系的識別碼以及元素內容的分葉值字串所組成。  
  
 首先，呼叫 **sp_xml_preparedocument** 預存程序以取得文件控制代碼。 接著將此文件控制代碼傳遞至 OPENXML。  
  
 OPENXML 陳述式說明下列各項：  
  
-   *rowpattern* (/root/Customer/Order) 識別要處理的 <`Order`> 節點。  
  
-   *flags* 參數值設為 **1**，表示屬性中心的對應。 因此，XML 屬性對應至 *SchemaDeclaration*中所定義的資料列集資料行。  
  
-   在 WITH 子句內的 *SchemaDeclaration* 中，資料列集資料行名稱 **oid** 和 **amount** 符合相對應的 XML 屬性名稱。 因此未指定 *ColPattern* 參數。 針對資料列集中的 **comment** 資料行， XPath 函數 **text()** 指定為 *ColPattern*。 這將會覆寫 *flags*中所指定之屬性中心的對應，而資料行將包含元素內容的分葉值字串。  
  
 然後，SELECT 陳述式擷取由 OPENXML 所提供之資料列集內的所有資料行。  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
--sample XML document  
SET @xmlDocument =N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied  
      </Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
            <Urgency>Important</Urgency>  
            Happy Customer.  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/root/Customer/Order', 1)  
     WITH (oid     char(5),   
           amount  float,   
           comment ntext 'text()')  
EXEC sp_xml_removedocument @docHandle  
```  
  
 以下是結果：  
  
```  
oid   amount        comment  
----- -----------   -----------------------------  
O1    3.5           NULL  
O2    13.4          Customer was very satisfied  
O3    100.0         Happy Customer.  
O4    10000.0       NULL  
```  
  
### <a name="e-specifying-tablename-in-the-with-clause"></a>E. 在 WITH 子句中指定 TableName  
 此範例在 WITH 子句中指定 *TableName* ，而不是在 *SchemaDeclaration*中。 若您具有所需結構的資料表，且不需要資料行模式 (*ColPattern* 參數)，這會是相當有用的方式。  
  
 此範例中的 XML 文件是由 <`Customer`> 和 <`Order`> 元素組成。 OPENXML 陳述式所擷取的訂單資訊是來自於 XML 文件中的三個資料行資料列集 (**oid**、**date** 及 **amount**)。  
  
 首先，呼叫 **sp_xml_preparedocument** 預存程序以取得文件控制代碼。 接著將此文件控制代碼傳遞至 OPENXML。  
  
 OPENXML 陳述式說明下列各項：  
  
-   *rowpattern* (/root/Customer/Order) 識別要處理的 <`Order`> 節點。  
  
-   WITH 子句中沒有 *SchemaDeclaration*。 相反地，有指定資料表名稱。 因此，資料表結構描述是做為資料列集結構描述使用。  
  
-   *flags* 參數值設為 **1** ，表示屬性中心的對應。 因此，由 *rowpattern*識別的元素屬性是對應到相同名稱的資料列集資料行。  
  
 然後，SELECT 陳述式擷取由 OPENXML 所提供之資料列集內的所有資料行。  
  
```  
-- Create a test table. This table schema is used by OPENXML as the  
-- rowset schema.  
CREATE TABLE T1(oid char(5), date datetime, amount float)  
GO  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
-- Sample XML document  
SET @xmlDocument =N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very   
             satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/root/Customer/Order', 1)  
     WITH T1  
EXEC sp_xml_removedocument @docHandle  
```  
  
 以下是結果：  
  
```  
oid   date                        amount  
----- --------------------------- ----------  
O1    1996-01-20 00:00:00.000     3.5  
O2    1997-04-30 00:00:00.000     13.4  
O3    1999-07-14 00:00:00.000     100.0  
O4    1996-01-20 00:00:00.000     10000.0  
```  
  
### <a name="f-obtaining-the-result-in-an-edge-table-format"></a>F. 取得邊緣資料表格式的結果  
 在此範例中，OPENXML 陳述式未指定 WITH 子句。 因此，OPENXML 所產生的資料列集具有邊緣資料表格式。 SELECT 陳述式以邊緣資料表傳回所有資料行。  
  
 此範例中的範例 XML 文件是由 <`Customer`>、<`Order`> 和 <`OrderDetail`> 元素組成。  
  
 首先，呼叫 **sp_xml_preparedocument** 預存程序以取得文件控制代碼。 接著將此文件控制代碼傳遞至 OPENXML。  
  
 OPENXML 陳述式說明下列各項：  
  
-   *rowpattern* (/ROOT/Customer) 識別要處理的 <`Customer`> 節點。  
  
-   未提供 WITH 子句。 因此，OPENXML 以邊緣資料表格式傳回資料列集。  
  
 然後，SELECT 陳述式擷取邊緣資料表中的所有資料行。  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
SET @xmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer')  
  
EXEC sp_xml_removedocument @docHandle  
```  
  
 結果是以邊緣資料表傳回。 您可以針對邊緣資料表寫入查詢以取得資訊。 例如：  
  
-   以下查詢傳回文件中 **Customer** 節點的數目。 由於未指定 WITH 子句，因此 OPENXML 傳回邊緣資料表。 SELECT 陳述式查詢邊緣資料表。  
  
    ```  
    SELECT count(*)  
    FROM OPENXML(@docHandle, '/')  
    WHERE localname = 'Customer'  
    ```  
  
-   下列查詢傳回元素類型之 XML 節點的本機名稱。  
  
    ```  
    SELECT distinct localname   
    FROM OPENXML(@docHandle, '/')   
    WHERE nodetype = 1   
    ORDER BY localname  
    ```  
  
### <a name="g-specifying-rowpattern-ending-with-an-attribute"></a>G. 指定 rowpattern 結束於屬性  
 此範例中的 XML 文件是由 <`Customer`>、<`Order`> 和 <`OrderDetail`> 元素組成。 OPENXML 陳述式所擷取的訂單詳細資訊是來自於 XML 文件中的三的資料行資料列集 (**ProductID**、**Quantity** 和 **OrderID**)。  
  
 首先，呼叫 **sp_xml_preparedocument** 預存程序以取得文件控制代碼。 接著將此文件控制代碼傳遞至 OPENXML。  
  
 OPENXML 陳述式說明下列各項：  
  
-   *rowpattern* (/ROOT/Customer/Order/OrderDetail/\@ProductID) 結束於 XML 屬性 ( **ProductID**)。 在結果資料列集中，為每個在 XML 文件中選取的屬性節點建立資料列。  
  
-   在此範例中，未指定 *flags* 參數。 相反地，由 *ColPattern* 參數指定對應。  
  
 在 WITH 子句內的 *SchemaDeclaration* 中，亦使用 *ColName* 與 *ColType* 參數來指定 *ColPattern* 。 選用的 *ColPattern* 是指定的 XPath 模式，它表示下列各項：  
  
-   針對資料列集內的 **ProdID** 資料行指定為 *ColPattern* 的 XPath 模式 (**.**) 識別內容節點，即目前節點。 根據所指定的 *rowpattern*，這是 <`OrderDetail`> 元素的 **ProductID** 屬性。  
  
-   針對資料列集內的 **Qty** 資料行所指定的 *ColPattern*、**../\@Quantity**，識別內容節點 \<ProductID> 之父節點 <`OrderDetail`> 的 **Quantity** 屬性。  
  
-   同樣地，針對資料列集內的 **OID** 資料行所指定的 *ColPattern*、**../../\@OrderID**，識別內容節點的父節點之父系 <`Order`> 的 **OrderID** 屬性。 父節點是 <`OrderDetail`>，內容節點是 <`ProductID`>。  
  
 然後，SELECT 陳述式擷取由 OPENXML 所提供之資料列集內的所有資料行。  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
--Sample XML document  
SET @xmlDocument =N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer/Order/OrderDetail/@ProductID')  
       WITH ( ProdID  int '.',  
              Qty     int '../@Quantity',  
              OID     int '../../@OrderID')  
EXEC sp_xml_removedocument @docHandle  
```  
  
 以下是結果：  
  
```  
ProdID      Qty         OID  
----------- ----------- -------   
11          12          10248  
42          10          10248  
72          3           10283  
```  
  
### <a name="h-specifying-an-xml-document-that-has-multiple-text-nodes"></a>H. 指定含有多個文字節點的 XML 文件  
 若在 XML 文件中具有多個文字節點，含有 *ColPattern* **text()** 的 SELECT 陳述式將只傳回第一個文字節點，而不是所有節點。 例如：  
  
```  
DECLARE @h int  
EXEC sp_xml_preparedocument @h OUTPUT,  
         N'<root xmlns:a="urn:1">  
           <a:Elem abar="asdf">  
             T<a>a</a>U  
           </a:Elem>  
         </root>',  
         '<ns xmlns:b="urn:1" />'  
  
SELECT * FROM openxml(@h, '/root/b:Elem')  
      WITH (Col1 varchar(20) 'text()')  
EXEC sp_xml_removedocument @h  
```  
  
 SELECT 陳述式傳回的結果為 **T** ，而非 **TaU**。  
  
### <a name="i-specifying-the-xml-data-type-in-the-with-clause"></a>I. 在 WITH 子句中指定 xml 資料類型  
 在 WITH 子句中，對應到 **xml** 資料類型資料行的資料行模式，不論具類型或不具類型，都必須傳回空序列或元素的序列、處理指示、文字節點和註解。 此資料轉換成 **xml** 資料類型。  
  
 在下列範例中，WITH 子句中的資料表結構描述宣告包含 **xml** 類型資料行。  
  
```  
DECLARE @h int  
DECLARE @x xml  
set @x = '<Root>  
  <row id="1"><lname>Duffy</lname>  
   <Address>  
            <Street>111 Maple</Street>  
            <City>Seattle</City>  
   </Address>  
  </row>  
  <row id="2"><lname>Wang</lname>  
   <Address>  
            <Street>222 Pine</Street>  
            <City>Bothell</City>  
   </Address>  
  </row>  
</Root>'  
  
EXEC sp_xml_preparedocument @h output, @x  
SELECT *  
FROM   OPENXML (@h, '/Root/row', 10)  
      WITH (id int '@id',  
  
            lname    varchar(30),  
            xmlname  xml 'lname',  
            OverFlow xml '@mp:xmltext')  
EXEC sp_xml_removedocument @h  
```  
  
 特別是，您要將 **xml** 類型變數 (\@x) 傳遞至 **sp_xml_preparedocument()** 函式。  
  
 以下是結果：  
  
```  
id  lname   xmlname                   OverFlow  
--- ------- ------------------------------ -------------------------------  
1   Duffy   <lname>Duffy</lname>  <row><Address>  
                                   <Street>111 Maple</Street>  
                                   <City>Seattle</City>  
                                  </Address></row>  
2   Wang    <lname>Wang</lname>   <row><Address>  
                                    <Street>222 Pine</Street>  
                                    <City>Bothell</City>  
                                   </Address></row>  
```  
  
 請注意結果的下列各項：  
  
-   若為 **varchar(30)** 類型的 **lname** 資料行，會從對應的 <`lname`> 元素擷取其值。  
  
-   若為 **xml** 類型的 **xmlname** 資料行，會傳回相同名稱元素作為它的值。  
  
-   此旗標設為 10。 10 表示 2 + 8，其中 2 指示元素中心的對應，8 表示只有未耗用的 XML 資料才加入至 WITH 子句中定義的 OverFlow 資料行。 如果您將旗標設為 2，則整個 XML 文件會複製到在 WITH 子句中指定的 OverFlow 資料行。  
  
-   假如 WITH 子句中的資料行是具類型的 XML 資料行，但 XML 執行個體不符合此結構描述，則會傳回錯誤。  
  
### <a name="j-retrieving-individual-values-from-multivalued-attributes"></a>J. 從多值屬性中擷取個別的值  
 XML 文件可以擁有多重值的屬性。 例如， **IDREFS** 屬性可為多重值。 在 XML 文件中，多重值的屬性值是指定為字串，並以空格區隔其值。 在下列 XML 文件中，\<學生> 項目的 **attends** 屬性與 \<班級> 的 **attendedBy** 屬性為多重值。 從多重值 XML 屬性中擷取個別的值，並將每個值儲存於資料庫中的個別資料列需要額外的工作。 此範例顯示其處理過程。  
  
 此範例 XML 文件由下列元素構成：  
  
-   \<學生>  
  
     **id** (學生識別碼)、 **name**與 **attends** 屬性。 **attends** 屬性為多重值屬性。  
  
-   \<班級>  
  
     **id** (班級識別碼)、 **name**與 **attendedBy** 屬性。 **attendedBy** 屬性為多重值屬性。  
  
 \<學生> 中的 **attends** 屬性與 \<班級> 中的 **attendedBy** 屬性代表學生與類別資料表之間的 **m:n** 關聯性。 一位學生可以選擇多種學科而一種學科可以收授多位學生。  
  
 假設您要切割此文件並將文件儲存於資料庫，如下所示：  
  
-   將 \<學生> 資料儲存於 Students 資料表中。  
  
-   將 \<班級> 資料儲存於 Courses 資料表中。  
  
-   將 Student 與 Class 之間的 **m:n** 關聯性資料儲存於 CourseAttendence 資料表中。 取出這些值需要額外的工作。 若要擷取此資訊並將之儲存於資料表，請使用下列預存程序：  
  
    -   **Insert_Idrefs_Values**  
  
         將學科識別碼與學生識別碼的值插入 CourseAttendence 資料表。  
  
    -   **Extract_idrefs_values**  
  
         從每個 \<課程> 項目中擷取個別的學生識別碼。 使用邊緣資料表來擷取這些值。  
  
 以下為其步驟：  
  
```  
-- Create these tables:  
DROP TABLE CourseAttendance  
DROP TABLE Students  
DROP TABLE Courses  
GO  
CREATE TABLE Students(  
                id   varchar(5) primary key,  
                name varchar(30)  
                )  
GO  
CREATE TABLE Courses(  
               id       varchar(5) primary key,  
               name     varchar(30),  
               taughtBy varchar(5)  
)  
GO  
CREATE TABLE CourseAttendance(  
             id         varchar(5) references Courses(id),  
             attendedBy varchar(5) references Students(id),  
             constraint CourseAttendance_PK primary key (id, attendedBy)  
)  
go  
-- Create these stored procedures:  
DROP PROCEDURE f_idrefs  
GO  
CREATE PROCEDURE f_idrefs  
    @t      varchar(500),  
    @idtab  varchar(50),  
    @id     varchar(5)  
AS  
DECLARE @sp int  
DECLARE @att varchar(5)  
SET @sp = 0  
WHILE (LEN(@t) > 0)  
BEGIN   
    SET @sp = CHARINDEX(' ', @t+ ' ')  
    SET @att = LEFT(@t, @sp-1)  
    EXEC('INSERT INTO '+@idtab+' VALUES ('''+@id+''', '''+@att+''')')  
    SET @t = SUBSTRING(@t+ ' ', @sp+1, LEN(@t)+1-@sp)  
END  
Go  
  
DROP PROCEDURE fill_idrefs  
GO  
CREATE PROCEDURE fill_idrefs   
    @xmldoc     int,  
    @xpath      varchar(100),  
    @from       varchar(50),  
    @to         varchar(50),  
    @idtable    varchar(100)  
AS  
DECLARE @t varchar(500)  
DECLARE @id varchar(5)  
  
/* Temporary Edge table */  
SELECT *   
INTO #TempEdge   
FROM OPENXML(@xmldoc, @xpath)  
  
DECLARE fillidrefs_cursor CURSOR FOR  
    SELECT CAST(iv.text AS nvarchar(200)) AS id,  
           CAST(av.text AS nvarchar(4000)) AS refs  
    FROM   #TempEdge c, #TempEdge i,  
           #TempEdge iv, #TempEdge a, #TempEdge av  
    WHERE  c.id = i.parentid  
    AND    UPPER(i.localname) = UPPER(@from)  
    AND    i.id = iv.parentid  
    AND    c.id = a.parentid  
    AND    UPPER(a.localname) = UPPER(@to)  
    AND    a.id = av.parentid  
  
OPEN fillidrefs_cursor  
FETCH NEXT FROM fillidrefs_cursor INTO @id, @t  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
    IF (@@FETCH_STATUS <> -2)  
    BEGIN  
        execute f_idrefs @t, @idtable, @id  
    END  
    FETCH NEXT FROM fillidrefs_cursor INTO @id, @t  
END  
CLOSE fillidrefs_cursor  
DEALLOCATE fillidrefs_cursor  
Go  
-- This is the sample document that is shredded and the data is stored in the preceding tables.  
DECLARE @h int  
EXECUTE sp_xml_preparedocument @h OUTPUT, N'<Data>  
  <Student id = "s1" name = "Student1"  attends = "c1 c3 c6"  />  
  <Student id = "s2" name = "Student2"  attends = "c2 c4" />  
  <Student id = "s3" name = "Student3"  attends = "c2 c4 c6" />  
  <Student id = "s4" name = "Student4"  attends = "c1 c3 c5" />  
  <Student id = "s5" name = "Student5"  attends = "c1 c3 c5 c6" />  
  <Student id = "s6" name = "Student6" />  
  
  <Class id = "c1" name = "Intro to Programming"   
         attendedBy = "s1 s4 s5" />  
  <Class id = "c2" name = "Databases"   
         attendedBy = "s2 s3" />  
  <Class id = "c3" name = "Operating Systems"   
         attendedBy = "s1 s4 s5" />  
  <Class id = "c4" name = "Networks" attendedBy = "s2 s3" />  
  <Class id = "c5" name = "Algorithms and Graphs"   
         attendedBy =  "s4 s5"/>  
  <Class id = "c6" name = "Power and Pragmatism"   
         attendedBy = "s1 s3 s5" />  
</Data>'  
  
INSERT INTO Students SELECT * FROM OPENXML(@h, '//Student') WITH Students  
  
INSERT INTO Courses SELECT * FROM OPENXML(@h, '//Class') WITH Courses  
/* Using the edge table */  
EXECUTE fill_idrefs @h, '//Class', 'id', 'attendedby', 'CourseAttendance'  
  
SELECT * FROM Students  
SELECT * FROM Courses  
SELECT * FROM CourseAttendance  
  
EXECUTE sp_xml_removedocument @h  
```  
  
### <a name="k-retrieving-binary-from-base64-encoded-data-in-xml"></a>K. 從 XML 的 Base64 編碼資料中擷取二進位資料  
 二進位資料常常使用 Base64 編碼而包含在 XML 中。 當您使用 OPENXML 來切割此 XML 時，會接收到 Base64 編碼資料。 此範例示範如何將 Base64 編碼資料轉換回二進位。  
  
-   以範例二進位資料建立資料表。  
  
-   使用 FOR XML 查詢和 BINARY BASE64 選項來建構將二進位資料編碼成 base64 的 XML。  
  
-   使用 OPENXML 來切割 XML。 OPENXML 傳回的資料將為 Base64 編碼資料。 接下來，呼叫 .value 函數將此資料轉換回二進位。  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 varbinary(100))  
go  
-- Insert sample binary data  
INSERT T VALUES(1, 0x1234567890)   
go  
 -- Create test XML document that has base64 encoded binary data (use FOR XML query and specify BINARY BASE64 option)  
SELECT * FROM T  
FOR XML AUTO, BINARY BASE64  
go  
-- result  
-- <T Col1="1" Col2="EjRWeJA="/>  
  
-- Now shredd the sample XML using OPENXML.   
-- Call the .value function to convert   
-- the base64 encoded data returned by OPENXML to binary.  
DECLARE @h int ;  
EXEC sp_xml_preparedocument @h OUTPUT, '<T Col1="1" Col2="EjRWeJA="/>' ;  
SELECT Col1,   
CAST('<binary>' + Col2 + '</binary>' AS XML).value('.', 'varbinary(max)') AS BinaryCol   
FROM openxml(@h, '/T')   
WITH (Col1 integer, Col2 varchar(max)) ;  
EXEC sp_xml_removedocument @h ;  
GO  
```  
  
 以下是結果。 傳回的二進位資料是資料表 T 的原始二進位資料。  
  
```  
Col1        BinaryCol  
----------- ---------------------  
1           0x1234567890  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_xml_preparedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql)   
 [sp_xml_removedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql)   
 [OPENXML &#40;Transact-SQL&#41;](/sql/t-sql/functions/openxml-transact-sql)   
 [OPENXML &#40;SQL Server&#41;](openxml-sql-server.md)  
  
  
