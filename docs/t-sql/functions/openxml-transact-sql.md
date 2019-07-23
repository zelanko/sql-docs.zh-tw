---
title: OPENXML (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9dacd09604661f9880533fcdcafd2fb7ab9ab12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914588"
---
# <a name="openxml-transact-sql"></a>OPENXML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  OPENXML 提供 XML 文件上的資料列集檢視。 因為 OPENXML 是資料列集提供者，所以 OPENXML 可以用在像是資料表、檢視或 OPENROWSET 函數等資料列集提供者能出現的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中。  
  
 ![文章連結圖示](../../database-engine/configure-windows/media/topic-link.gif "文章連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
OPENXML( idoc int [ in] , rowpattern nvarchar [ in ] , [ flags byte [ in ] ] )   
[ WITH ( SchemaDeclaration | TableName ) ]  
```  
  
## <a name="arguments"></a>引數  
 *idoc*  
 這是 XML 文件內部表示的文件控制代碼。 XML 文件的內部表示是透過呼叫 **sp_xml_preparedocument** 所建立。  
  
 *rowpattern*  
 為用於識別應作為資料列處理節點的 XPath 模式。 節點來自在 *idoc* 參數中傳遞其控點的 XML 文件。
  
 *flags*  
 指出 XML 資料和關聯式資料列集之間所使用的對應，以及填入溢出資料行的方式。 *flags* 是選擇性的輸入參數，而且可以是下列其中一個值。  
  
|位元組值|Description|  
|----------------|-----------------|  
|**0**|預設為**以屬性為主**的對應。|  
|**1**|使用**以屬性為主**的對應。 可以和 XML_ELEMENTS 合併使用。 在此情況下，會先套用**屬性中心**對應。 接下來，會針對任何剩餘的資料行套用**項目中心**對應。|  
|**2**|使用**以元素為主**的對應。 可以和 XML_ATTRIBUTES 合併使用。 在此情況下，會先套用**屬性中心**對應。 接下來，會針對任何剩餘的資料行套用**項目中心**對應。|  
|**8**|可以和 XML_ATTRIBUTES 或 XML_ELEMENTS 合併使用 (邏輯 OR)。 在擷取的內容中，此標幟會指出所取用的資料不應複製到溢位屬性 **\@mp:xmltext**。|  
  
 _SchemaDeclaration_  
 這是表單的結構描述定義：_ColName_*ColType* [_ColPattern_ | _MetaProperty_] [ **,** _ColNameColType_ [_ColPattern_ | _MetaProperty_]...]  
  
 _ColName_  
 這是資料列集中的資料行名稱。  
  
 *ColType*  
 這是資料列集中資料行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 如果資料行類型與屬性的基礎 **xml** 資料類型不同，則會發生強制型轉。  
  
 *ColPattern*  
 這是描述 XML 節點應該如何對應到資料行的選擇性、一般 XPath 模式。 若未指定 *ColPattern*，則會發生預設對應 (*flags* 指定的**屬性中心**或**項目中心**對應)。  
  
 作為指定為 *ColPattern* 之 XPath 模式會用於指定對應的特殊性質 (針對**屬性中心**和**項目中心**對應)，覆寫或增強 *flags* 指出的預設對應。  
  
 指定為 *ColPattern* 的一般 XPath 模式也支援中繼屬性。  
  
 *MetaProperty*  
 這是 OPENXML 提供的中繼屬性之一。 如果指定 *MetaProperty*，資料行會包含由中繼屬性所提供的資訊。 中繼屬性可讓您擷取 XML 節點的相關資訊 (如相對位置和命名空間資訊)。 這些中繼屬性可提供比文字表示中可見內容更多的資訊。  
  
 *TableName*  
 這是在具有所要結構描述的資料表已經存在且不需要資料行模式的情況下，可以提供的資料表名稱 (而非 *SchemaDeclaration*)。  
  
## <a name="remarks"></a>Remarks  
 WITH 子句會使用 *SchemaDeclaration* 或指定現有的 *TableName*，來提供資料列集格式 (以及其他需要的對應資訊)。 若沒有指定選擇性的 WITH 子句，則會以**邊緣**資料表格式傳回結果。 邊緣資料表代表單一資料表中的細粒 XML 文件結構 (如元素/屬性名稱、文件階層、命名空間、PI 等等)。  
  
 下表說明**邊緣**資料表的結構。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**bigint**|這是文件節點的唯一識別碼。<br /><br /> 根元素的識別碼值為 0。 負的識別碼值會保留。|  
|**parentid**|**bigint**|識別節點的父系。 這個識別碼所識別的父系不一定是父項目，這要視其父系由這個識別碼所識別節點的 NodeType 而定。 例如，如果節點是文字節點，則其父系可能是屬性節點。<br /><br />  如果節點位於 XML 文件的最上層，其 ParentID 為 NULL。|  
|**nodetype**|**int**|識別節點類型。 這是對應到 XML DOM 節點類型編號的整數。<br /><br /> 節點類型有：<br /><br /> 1 = 元素節點<br /><br /> 2 = 屬性節點<br /><br /> 3 = 文字節點|  
|**localname**|**nvarchar**|提供元素或屬性的本機名稱。 如果 DOM 物件不具有名稱，則為 NULL。|  
|**prefix**|**nvarchar**|這是節點名稱的命名空間前置詞。|  
|**namespaceuri**|**nvarchar**|這是節點的命名空間 URI。 如果值是 NULL，表示沒有命名空間。|  
|**datatype**|**nvarchar**|這是元素或屬性資料列的實際資料類型，否則為 NULL。 資料類型是從內嵌 DTD 或內嵌結構描述推斷。|  
|**prev**|**bigint**|這是前一個同層級元素的 XML 識別碼。 如果沒有直接的前一個同層級，則為 NULL。|  
|**text**|**ntext**|包含文字形式的屬性值或項目內容 (如果**邊緣**資料表項目不需要值，則為 NULL)。|  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-a-simple-select-statement-with-openxml"></a>A. 以 OPENXML 使用簡單的 SELECT 陳述式  
 下列範例會使用 `sp_xml_preparedocument` 來建立 XML 影像的內部表示法。 然後對 XML 文件的內部表示法執行使用 `SELECT` 資料列集提供者的 `OPENXML` 陳述式。  
  
 *flag* 值是設為 `1`。 此值指出**屬性中心**對應。 因此 XML 屬性是對應到資料列集中的資料行。 指定為 `/ROOT/Customer` 的 *rowpattern* 會識別要處理的 `<Customers>` 節點。  
  
 此處並未指定選擇性的 *ColPattern* (資料行模式) 參數，因為資料行名稱與 XML 屬性名稱相符。  
  
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
  
 如果相同的 `SELECT` 陳述式是以 「旗標」  設為 `2` 的方式 (表示**項目中心**對應) 來執行，則 XML 文件中兩個客戶的 `CustomerID` 及 `ContactName` 值都會以 NULL 傳回，因為 XML 文件中沒有任何名為 `CustomerID` 或 `ContactName` 的項目。  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName  
---------- -----------  
NULL       NULL  
NULL       NULL  
```  
  
### <a name="b-specifying-colpattern-for-mapping-between-columns-and-the-xml-attributes"></a>B. 指定資料行與 XML 屬性間對應的 ColPattern  
 下列查詢會從 XML 文件傳回客戶識別碼、訂單日期、產品識別碼與數量屬性。 *rowpattern* 會識別 `<OrderDetails>` 元素。 `ProductID` 和 `Quantity` 是 `<OrderDetails>` 元素的屬性。 然而，`OrderID`、`CustomerID` 和 `OrderDate` 是父元素 (`<Orders>`) 的屬性。  
  
 選擇性的 *ColPattern* 已針對下列對應指定：  
  
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
  
