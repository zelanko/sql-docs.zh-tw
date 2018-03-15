---
title: OPENXML (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENXML_TSQL
- OPENXML
dev_langs:
- TSQL
helpviewer_keywords:
- OPENXML statement
- rowsets [SQL Server], XML documents
- XML [SQL Server], rowset views
ms.assetid: 8088b114-7d01-435a-8e0d-b81abacc86d6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f5b32c99393bb5b7f31423df840f7f0069dd3518
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="openxml-transact-sql"></a>OPENXML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OPENXML 提供 XML 文件上的資料列集檢視。 因為 OPENXML 是資料列集提供者，所以 OPENXML 可以用在像是資料表、檢視或 OPENROWSET 函數等資料列集提供者能出現的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
OPENXML( idoc int [ in] , rowpattern nvarchar [ in ] , [ flags byte [ in ] ] )   
[ WITH ( SchemaDeclaration | TableName ) ]  
```  
  
## <a name="arguments"></a>引數  
 *idoc*  
 這是 XML 文件內部表示的文件控制代碼。 XML 文件的內部表示是透過呼叫 **sp_xml_preparedocument** 所建立。  
  
 *rowpattern*  
 這是用來識別要當作資料列處理的節點 (在其控制代碼由 *idoc* 參數傳入的 XML 文件中) 的 XPath 模式。  
  
 *flags*  
 表示應該使用在 XML 資料和關聯式資料列集之間的對應，以及應如何填入溢出的資料行。 *flags* 是選擇性的輸入參數，而且可以是下列其中一個值。  
  
|位元組值|描述|  
|----------------|-----------------|  
|**0**|預設為**以屬性為主**的對應。|  
|**1**|使用**以屬性為主**的對應。 可以和 XML_ELEMENTS 合併使用。 在這個情況下，會先套用**以屬性為主**的對應，然後對所有尚未處理的資料行套用**以元素為主**的對應。|  
|**2**|使用**以元素為主**的對應。 可以和 XML_ATTRIBUTES 合併使用。 在這個情況下，會先套用**以屬性為主**的對應，然後對所有尚未處理的資料行套用**以元素為主**的對應。|  
|**8**|可以和 XML_ATTRIBUTES 或 XML_ELEMENTS 合併使用 (邏輯 OR)。 在擷取的內容中，這個旗標表示耗用的資料不應複製到溢位屬性 **@mp:xmltext**。|  
  
 *SchemaDeclaration*  
 這是表單的結構描述定義：*ColName**ColType* [*ColPattern* | *MetaProperty*] [**,***ColNameColType* [*ColPattern* | *MetaProperty*]...]  
  
 *ColName*  
 這是資料列集中的資料行名稱。  
  
 *ColType*  
 這是資料列集中資料行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 如果資料行類型與屬性的基礎 **xml** 資料類型不同，則會發生強制型轉。  
  
 *ColPattern*  
 這是描述 XML 節點應該如何對應到資料行的選擇性、一般 XPath 模式。 如果未指定 *ColPattern*，則會發生預設的對應 (由 *flags* 所指定之**以屬性為主**或**以元素為主**的對應)。  
  
 會使用指定為 *ColPattern* 的 XPath 模式來指定對應的特殊性質 (在為**以屬性為主**和**以元素為主**之對應的情況下)，此性質可覆寫或增強由 *flags* 所指定的預設對應。  
  
 指定為 *ColPattern* 的一般 XPath 模式也支援中繼屬性。  
  
 *MetaProperty*  
 這是 OPENXML 提供的中繼屬性之一。 如果指定 *MetaProperty*，資料行會包含由中繼屬性所提供的資訊。 中繼屬性可讓您擷取 XML 節點的相關資訊 (如相對位置和命名空間資訊)。 這提供比文字表示更詳細的資訊。  
  
 *TableName*  
 這是在具有所要結構描述的資料表已經存在且不需要資料行模式的情況下，可以提供的資料表名稱 (而非 *SchemaDeclaration*)。  
  
## <a name="remarks"></a>Remarks  
 WITH 子句會使用 *SchemaDeclaration* 或指定現有的 *TableName*，來提供資料列集格式 (以及其他需要的對應資訊)。 如果未指定選擇性的 WITH 子句，則會以**邊緣**資料表格式傳回結果。 邊緣資料表代表單一資料表中的細粒 XML 文件結構 (如元素/屬性名稱、文件階層、命名空間、PI 等等)。  
  
 下表說明**邊緣**資料表的結構。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**bigint**|這是文件節點的唯一識別碼。<br /><br /> 根元素的識別碼值為 0。 負的識別碼值會保留。|  
|**parentid**|**bigint**|識別節點的父系。 這個識別碼所識別的父系不一定是父元素，這要視其父系由這個識別碼所識別之節點的 NodeType 而定。 例如，如果節點是文字節點，則其父系可能是屬性節點。<br /><br />  如果節點位於 XML 文件的最上層，其 ParentID 為 NULL。|  
|**nodetype**|**int**|識別節點類型。 這是對應到 XML DOM 節點類型編號的整數。<br /><br /> 節點類型有：<br /><br /> 1 = 元素節點<br /><br /> 2 = 屬性節點<br /><br /> 3 = 文字節點|  
|**localname**|**nvarchar**|提供元素或屬性的本機名稱。 如果 DOM 物件不具有名稱，則為 NULL。|  
|**prefix**|**nvarchar**|這是節點名稱的命名空間前置詞。|  
|**namespaceuri**|**nvarchar**|這是節點的命名空間 URI。 如果值是 NULL，表示沒有命名空間。|  
|**datatype**|**nvarchar**|這是元素或屬性資料列的實際資料類型，否則為 NULL。 資料類型是從內嵌 DTD 或內嵌結構描述推斷。|  
|**prev**|**bigint**|這是前一個同層級元素的 XML 識別碼。 如果沒有直接的前一個同層級，則為 NULL。|  
|**text**|**ntext**|包含文字格式的屬性值或元素內容 (如果**邊緣**資料表項目不需要值，則為 NULL)。|  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-a-simple-select-statement-with-openxml"></a>A. 以 OPENXML 使用簡單的 SELECT 陳述式  
 下列範例會使用 `sp_xml_preparedocument` 來建立 XML 影像的內部表示法。 然後對 XML 文件的內部表示法執行使用 `SELECT` 資料列集提供者的 `OPENXML` 陳述式。  
  
 *flag* 值是設為 `1`。 這表示**以屬性為主**的對應。 因此 XML 屬性是對應到資料列集中的資料行。 指定為 `/ROOT/Customer` 的 *rowpattern* 會識別要處理的 `<Customers>` 節點。  
  
 因為資料行名稱符合 XML 屬性名稱，所以沒有指定選擇性的 *ColPattern* (資料行模式) 參數。  
  
 `OPENXML` 資料列集提供者建立了有 2 個資料行的資料列集 (`CustomerID` 和 `ContactName`)，`SELECT` 陳述式可由這個資料列集擷取必要的資料行 (本範例中為所有資料行)。  
  
```  
DECLARE @idoc int, @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;  
-- Execute a SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customer',1)  
            WITH (CustomerID  varchar(10),  
                  ContactName varchar(20));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 如果相同的 `SELECT` 陳述式是以 *flags* 設為 `2` 的方式 (表示**以元素為主**的對應) 來執行，則 XML 文件中兩個客戶的 `CustomerID` 及 `ContactName` 值都會以 NULL 傳回，因為 XML 文件中沒有任何名為 `CustomerID` 或 `ContactName` 的元素。  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName  
---------- -----------  
NULL       NULL  
NULL       NULL  
```  
  
### <a name="b-specifying-colpattern-for-mapping-between-columns-and-the-xml-attributes"></a>B. 指定資料行與 XML 屬性間對應的 ColPattern  
 下列查詢從 XML 文件傳回客戶識別碼、訂單日期、產品識別碼與數量屬性。 *rowpattern* 會識別 `<OrderDetails>` 元素。 `ProductID` 和 `Quantity` 是 `<OrderDetails>` 元素的屬性。 然而，`OrderID`、`CustomerID` 和 `OrderDate` 是父元素 (`<Orders>`) 的屬性。  
  
 已指定選擇性的 *ColPattern*。 這表示下列項目：  
  
-   資料列集中的 `OrderID`、`CustomerID` 和 `OrderDate` 會對應到由 XML 文件中 *rowpattern* 所識別節點之父系的屬性。  
  
-   資料列集中的 `ProdID` 資料行會對應到 `ProductID` 屬性，而資料列集中的 `Qty` 資料行則會對應到 *rowpattern* 中所識別之節點的 `Quantity` 屬性。  
  
 雖然**以元素為主**的對應是由 *flags* 參數所指定，但是在 *ColPattern* 中指定的對應會覆寫這個對應。  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">v  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';   
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT stmt using OPENXML rowset provider  
SELECT *  
FROM   OPENXML (@idoc, '/ROOT/Customer/Order/OrderDetail',2)   
         WITH (OrderID       int         '../@OrderID',   
               CustomerID  varchar(10) '../@CustomerID',   
               OrderDate   datetime    '../@OrderDate',   
               ProdID      int         '@ProductID',   
               Qty         int         '@Quantity');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
OrderID CustomerID           OrderDate                 ProdID    Qty  
------------------------------------------------------------------------  
10248      VINET       1996-07-04 00:00:00.000   11      12  
10248      VINET       1996-07-04 00:00:00.000   42      10  
10283      LILAS       1996-08-16 00:00:00.000   72      3  
```  
  
### <a name="c-obtaining-results-in-an-edge-table-format"></a>C. 取得邊緣資料表格式的結果  
 下列範例中的取樣 XML 文件是由 `<Customers>`、`<Orders>` 和 `<Order_0020_Details>` 元素組成。 首先，會呼叫 **sp_xml_preparedocument** 以取得文件控制代碼。 接著將這個文件控制代碼傳送到 `OPENXML`。  
  
 在 `OPENXML` 陳述式中，*rowpattern* (`/ROOT/Customers`) 會識別要處理的 `<Customers>` 節點。 由於並未提供 WITH 子句，因此 `OPENXML` 會以**邊緣**資料表格式傳回資料列集。  
  
 最後，`SELECT` 陳述式會擷取**邊緣**資料表中的所有資料行。  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customers CustomerID="VINET" ContactName="Paul Henriot">  
   <Orders CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <Order_x0020_Details OrderID="10248" ProductID="11" Quantity="12"/>  
      <Order_x0020_Details OrderID="10248" ProductID="42" Quantity="10"/>  
   </Orders>  
</Customers>  
<Customers CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Orders CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <Order_x0020_Details OrderID="10283" ProductID="72" Quantity="3"/>  
   </Orders>  
</Customers>  
</ROOT>';  
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customers')   
EXEC sp_xml_removedocument @idoc;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [範例：使用 OPENXML](../../relational-databases/xml/examples-using-openxml.md)  
  
  
