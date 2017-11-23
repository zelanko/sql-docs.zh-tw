---
title: "OPENXML (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENXML_TSQL
- OPENXML
dev_langs: TSQL
helpviewer_keywords:
- OPENXML statement
- rowsets [SQL Server], XML documents
- XML [SQL Server], rowset views
ms.assetid: 8088b114-7d01-435a-8e0d-b81abacc86d6
caps.latest.revision: "24"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7b1fb1d28c4bddb679bd4aab8ce6cb11f21caca5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
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
 這是 XML 文件內部表示的文件控制代碼。 XML 文件的內部表示法由呼叫**sp_xml_preparedocument**。  
  
 *rowpattern*  
 是用來識別之節點的 XPath 模式 (在 XML 文件控制代碼會傳入*idoc*參數) 處理成資料列。  
  
 *旗標*  
 表示應該使用在 XML 資料和關聯式資料列集之間的對應，以及應如何填入溢出的資料行。 *旗標*是選擇性的輸入的參數，而且可以是下列值之一。  
  
|位元組值|Description|  
|----------------|-----------------|  
|**0**|預設為**屬性中心**對應。|  
|**1**|使用**屬性中心**對應。 可以和 XML_ELEMENTS 合併使用。 在此情況下，**屬性中心**對應會先套用，然後**元素中心**的對應套用於所有尚未使用的資料行。|  
|**2**|使用**元素中心**對應。 可以和 XML_ATTRIBUTES 合併使用。 在此情況下，**屬性中心**對應會先套用，然後**元素中心**對應已套用的所有資料行尚未處理。|  
|**8**|可以和 XML_ATTRIBUTES 或 XML_ELEMENTS 合併使用 (邏輯 OR)。 在擷取的內容，這個旗標表示耗用的資料不會複製到溢位屬性 **@mp:xmltext** 。|  
  
 *SchemaDeclaration*  
 在表單的結構描述定義： *ColName**Colpattern* [*ColPattern* | *中繼屬性*] [*ColNameColType* [*ColPattern* | *中繼屬性*]...]  
  
 *ColName*  
 這是資料列集中的資料行名稱。  
  
 *Colpattern*  
 這是資料列集中資料行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 如果資料行類型與不同的基礎**xml**屬性、 類型強制型轉的資料類型，就會發生。  
  
 *ColPattern*  
 這是描述 XML 節點應該如何對應到資料行的選擇性、一般 XPath 模式。 如果*ColPattern*未指定，預設對應 (**屬性中心**或**元素中心**對應所指定*旗標*) 進行。  
  
 為指定的 XPath 模式*ColPattern*用來指定對應的特殊本質 (如果是**屬性中心**和**元素中心**對應)，覆寫或加強所指定的預設對應*旗標*。  
  
 為指定的一般 XPath 模式*ColPattern*也支援中繼屬性。  
  
 *中繼屬性*  
 這是 OPENXML 提供的中繼屬性之一。 如果*中繼屬性*指定，則資料行包含的中繼屬性所提供的資訊。 中繼屬性可讓您擷取 XML 節點的相關資訊 (如相對位置和命名空間資訊)。 這提供比文字表示更詳細的資訊。  
  
 *TableName*  
 可以指定的資料表名稱 (而不是*SchemaDeclaration*) 如果已經有具有所需的結構描述的資料表和所需的任何資料行模式。  
  
## <a name="remarks"></a>備註  
 使用資料列集格式 （和所需的額外的對應資訊），提供 WITH 子句*SchemaDeclaration*或指定現有*TableName*。 如果選擇性的 WITH 子句未指定，結果都會傳回到**邊緣**資料表格式。 邊緣資料表代表單一資料表中的細粒 XML 文件結構 (如元素/屬性名稱、文件階層、命名空間、PI 等等)。  
  
 下表描述的結構**邊緣**資料表。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**bigint**|這是文件節點的唯一識別碼。<br /><br /> 根元素的識別碼值為 0。 負的識別碼值會保留。|  
|**parentid**|**bigint**|識別節點的父系。 這個識別碼所識別的父系不一定是父元素，這要視其父系由這個識別碼所識別之節點的 NodeType 而定。 例如，如果節點是文字節點，則其父系可能是屬性節點。<br /><br />  如果節點位於 XML 文件的最上層，其 ParentID 為 NULL。|  
|**節點類型**|**int**|識別節點類型。 這是對應到 XML DOM 節點類型編號的整數。<br /><br /> 節點類型有：<br /><br /> 1 = 元素節點<br /><br /> 2 = 屬性節點<br /><br /> 3 = 文字節點|  
|**localname**|**nvarchar**|提供元素或屬性的本機名稱。 如果 DOM 物件不具有名稱，則為 NULL。|  
|**prefix**|**nvarchar**|這是節點名稱的命名空間前置詞。|  
|**namespaceuri**|**nvarchar**|這是節點的命名空間 URI。 如果值是 NULL，表示沒有命名空間。|  
|**datatype**|**nvarchar**|這是元素或屬性資料列的實際資料類型，否則為 NULL。 資料類型是從內嵌 DTD 或內嵌結構描述推斷。|  
|**prev**|**bigint**|這是前一個同層級元素的 XML 識別碼。 如果沒有直接的前一個同層級，則為 NULL。|  
|**text**|**ntext**|包含的屬性值或文字格式的項目內容 (如果是 NULL 或**邊緣**資料表項目不需要值)。|  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-a-simple-select-statement-with-openxml"></a>A. 以 OPENXML 使用簡單的 SELECT 陳述式  
 下列範例會使用 `sp_xml_preparedocument` 來建立 XML 影像的內部表示法。 然後對 XML 文件的內部表示法執行使用 `SELECT` 資料列集提供者的 `OPENXML` 陳述式。  
  
 *旗標*值設定為`1`。 這表示**屬性中心**對應。 因此 XML 屬性是對應到資料列集中的資料行。 *Rowpattern*指定為`/ROOT/Customer`識別`<Customers>`節點進行處理。  
  
 選擇性*ColPattern* （資料行模式） 參數未指定因為資料行名稱符合 XML 屬性名稱。  
  
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
  
 如果相同`SELECT`執行陳述式與*旗標*設`2`，這表示**元素中心**的值，對應`CustomerID`和`ContactName`這兩個XML 文件中的客戶會傳回為 NULL，因為沒有任何項目，名為`CustomerID`或`ContactName`XML 文件中。  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName  
---------- -----------  
NULL       NULL  
NULL       NULL  
```  
  
### <a name="b-specifying-colpattern-for-mapping-between-columns-and-the-xml-attributes"></a>B. 指定資料行與 XML 屬性間對應的 ColPattern  
 下列查詢從 XML 文件傳回客戶識別碼、訂單日期、產品識別碼與數量屬性。 *Rowpattern*識別`<OrderDetails>`項目。 `ProductID` 和 `Quantity` 是 `<OrderDetails>` 元素的屬性。 然而，`OrderID`、`CustomerID` 和 `OrderDate` 是父元素 (`<Orders>`) 的屬性。  
  
 選擇性*ColPattern*指定。 這表示下列項目：  
  
-   `OrderID`， `CustomerID`，和`OrderDate`所識別節點的父屬性的資料列集對應中*rowpattern* XML 文件中。  
  
-   `ProdID`資料列集中的資料行對應到`ProductID`屬性，而`Qty`資料列集中的資料行對應到`Quantity`中識別之節點的屬性*rowpattern*。  
  
 雖然**元素中心**對應由指定*旗標*參數中指定的對應*ColPattern*會覆寫此對應。  
  
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
 下列範例中的取樣 XML 文件是由 `<Customers>`、`<Orders>` 和 `<Order_0020_Details>` 元素組成。 首先， **sp_xml_preparedocument**呼叫以取得文件控制代碼。 接著將這個文件控制代碼傳送到 `OPENXML`。  
  
 在`OPENXML`陳述式， *rowpattern* (`/ROOT/Customers`) 識別`<Customers>`節點處理。 因為未提供 WITH 子句，所以`OPENXML`傳回資料列集**邊緣**資料表格式。  
  
 最後`SELECT`陳述式會擷取所有的資料行**邊緣**資料表。  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [範例：使用 OPENXML](../../relational-databases/xml/examples-using-openxml.md)  
  
  
