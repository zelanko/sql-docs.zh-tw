---
title: OPENXML (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ColPattern [XML in SQL Server]
- OPENXML statement, about OPENXML statement
- writing XML, OPENXML statement
- OPENXML statement, querying XML
- attribute-centric mapping
- SELECT statement [SQL Server], OPENXML keyword
- column patterns [XML in SQL Server]
- row patterns [XML in SQL Server]
- rowpattern [XML in SQL Server]
- queries [XML in SQL Server], OPENXML statement
- XML [SQL Server], OPENXML statement
- element-centric mapping [SQL Server]
ms.assetid: 060126fc-ed0f-478f-830a-08e418d410dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb674ea7bd9540f7ae74bf9ad8737bdb83c237f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68195640"
---
# <a name="openxml-sql-server"></a>OPENXML (SQL Server)
  OPENXML 是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 關鍵字，可透過類似資料表或檢視表的記憶體中 XML 文件，提供資料列集。 OPENXML 允許對 XML 資料的存取像是關聯式資料列集一樣。 其做法是，提供 XML 文件內部表示法的資料列集檢視。 資料列集的記錄可以儲存在資料庫的資料表中。  
  
 OPENXML 可用於 SELECT 及 SELECT INTO 陳述式，其中出現的資料列集提供者、檢視或 OPENROWSET 都可做為來源。 如需 OPENXML 語法的相關資訊，請參閱 [OPENXML &#40;Transact-SQL&#41;](/sql/t-sql/functions/openxml-transact-sql)。  
  
 若要使用 OPENXML 針對 XML 檔撰寫查詢，您必須先呼叫`sp_xml_preparedocument`。 這樣會剖析 XML 文件，並將控制代碼傳回至準備要使用的已剖析文件。 剖析過的文件就是 XML 文件中，各種節點的文件物件模型 (DOM) 樹狀表示法。 接著文件控制代碼會傳遞至 OPENXML。 然後 OPENXML 會依據傳給它的參數，提供該文件的資料列集檢視。  
  
> [!NOTE]  
>  `sp_xml_preparedocument`會使用 SQL 更新版本的 MSXML 剖析器（Msxmlsql.dll）。 這個版本的 MSXML 剖析器的設計目的，是要支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並維持與 MSXML 2.6 舊版的相容性。  
  
 若要釋放記憶體空間，必須呼叫 **sp_xml_removedocument** 系統預存程序，將 XML 文件的內部表示法從記憶體中移除。  
  
 下圖說明此程序。  
  
 ![正在使用 OPENXML 剖析 XML](../../database-engine/media/xmlsp.gif "正在使用 OPENXML 剖析 XML")  
  
 請注意，若要了解 OPENXML，您必須先熟悉 XPath 查詢，並了解 XML。 如需 SQL Server 中 XPath 支援的詳細資訊，請參閱 [在 SQLXML 4.0 中使用 XPath 查詢](../sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)。  
  
> [!NOTE]  
>  OpenXML 允許將資料列及資料行的 XPath 模式參數化為變數。 如果程式設計人員將參數化內容向外部使用者公開 (例如，透過從外部呼叫的預存程序提供參數)，則這些參數化內容可能會導致 XPath 運算式的植入式攻擊。 為避免這些潛在的安全性問題，建議您絕不要對外部呼叫端公開 XPath 參數。  
  
## <a name="example"></a>範例  
 
  `OPENXML` 下列範例示範在 `INSERT` 陳述式和 `SELECT` 陳述式中使用 。 
  `<Customers>` 範例 XML 文件包含 `<Orders>` 和  元素。  
  
 首先， `sp_xml_preparedocument` 預存程序會剖析 XML 文件。 這份已剖析的文件以樹狀目錄表示 XML 文件中之節點 (元素、屬性、文字及註解)。 
  `OPENXML` 之後會參照這份已剖析的 XML 文件，並提供這份 XML 文件的所有或部分資料列集檢視。 
  `INSERT` 使用 `OPENXML` 的  陳述式，便可從這樣的資料列集將資料插入資料庫資料表。 
  `OPENXML` 有數個  呼叫可用來提供 XML 文件各個部分的資料列集檢視並處理它們，例如，將它們插入不同的資料表。 此處理序又稱為將 XML 切割成資料表。  
  
 
  `<Customers>` 下列範例將 XML 文件分成兩部分的方法是使用兩個 `Customers` 陳述式，將其 `<Orders>` 元素儲存在 `Orders` 資料表中，以及將其 `INSERT` 元素儲存在  資料表中。 
  `SELECT` 此範例同時也顯示帶有 `OPENXML` 的 `CustomerID` 陳述式，從 XML 文件中擷取 `OrderDate` 和 。 
  `sp_xml_removedocument`在此程序中的最一個步驟是呼叫 。 這是為了釋放已配置的記憶體，該記憶體是用來包含在剖析階段期間所建立的內部 XML 樹狀表示法。  
  
```  
-- Create tables for later population using OPENXML.  
CREATE TABLE Customers (CustomerID varchar(20) primary key,  
                ContactName varchar(20),   
                CompanyName varchar(20));  
GO  
CREATE TABLE Orders( CustomerID varchar(20), OrderDate datetime);  
GO  
DECLARE @docHandle int;  
DECLARE @xmlDocument nvarchar(max); -- or xml type  
SET @xmlDocument = N'<ROOT>  
<Customers CustomerID="XYZAA" ContactName="Joe" CompanyName="Company1">  
<Orders CustomerID="XYZAA" OrderDate="2000-08-25T00:00:00"/>  
<Orders CustomerID="XYZAA" OrderDate="2000-10-03T00:00:00"/>  
</Customers>  
<Customers CustomerID="XYZBB" ContactName="Steve"  
CompanyName="Company2">No Orders yet!  
</Customers>  
</ROOT>';  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument;  
-- Use OPENXML to provide rowset consisting of customer data.  
INSERT Customers   
SELECT *   
FROM OPENXML(@docHandle, N'/ROOT/Customers')   
  WITH Customers;  
-- Use OPENXML to provide rowset consisting of order data.  
INSERT Orders   
SELECT *   
FROM OPENXML(@docHandle, N'//Orders')   
  WITH Orders;  
-- Using OPENXML in a SELECT statement.  
SELECT * FROM OPENXML(@docHandle, N'/ROOT/Customers/Orders') WITH (CustomerID nchar(5) '../@CustomerID', OrderDate datetime);  
-- Remove the internal representation of the XML document.  
EXEC sp_xml_removedocument @docHandle;   
```  
  
 下圖針對先前使用 sp_xml_preparedocument 所建立的 XML 文件，顯示其剖析後的 XML 樹狀結構。  
  
 ![剖析的 XML 樹狀結構](../../database-engine/media/xmlparsedtree.gif "剖析的 XML 樹狀結構")  
  
## <a name="openxml-parameters"></a>OPENXML 參數  
 OPENXML 的參數包括：  
  
-   XML 文件控制代碼 (*idoc*)  
  
-   XPath 運算式，用來識別要對應到資料列的節點 (*rowpattern*)  
  
-   所要產生資料列集的描述  
  
-   資料列集資料行與 XML 節點之間的對應  
  
### <a name="xml-document-handle-idoc"></a>XML 文件控制代碼 (idoc)  
 `sp_xml_preparedocument`預存程式會傳回檔案控制代碼。  
  
### <a name="xpath-expression-to-identify-the-nodes-to-be-processed-rowpattern"></a>用來識別欲處理之節點的 XPath 運算式 (rowpattern)  
 
  *
  * 指定為 rowpattern的 XPath 運算式識別 XML 文件中的節點集。 
  *
  * 每個由 rowpattern 識別的節點，都會對應到由 OPENXML 所產生之資料列集中的單一資料列。  
  
 由 XPath 運算式所識別的節點，可以是 XML 文件中的任何 XML 節點。 
  *
  * 若 rowpattern 識別 XML 文件中的一組元素，則每個元素節點在資料列集中都有一識別的資料列。 
  *
  * 例如，若 *rowpattern*在屬性中結束，將會為每個 rowpattern 所選取的屬性節點建立資料列。  
  
### <a name="description-of-the-rowset-to-be-generated"></a>欲產生的資料列集說明  
 OPENXML 會使用資料列集結構描述，來產生結果資料列集。 指定資料列集結構描述時，可以使用下列選項。  
  
#### <a name="using-the-edge-table-format"></a>使用邊緣資料表格式  
 您應使用邊緣資料表格式來指定資料列集結構描述。 請不要使用 WITH 子句。  
  
 當您這麼做時，OPENXML 會以邊緣資料表格式來傳回資料列集。 之所以稱為邊緣資料表，是因為已剖析之 XML 文件樹狀目錄中的每個邊緣，都會對應到資料列集中的一個資料列。  
  
 在單一資料表中，邊緣資料表代表了較細部的 XML 文件結構。 此結構包含元素和屬性名稱、文件階層、命名空間及處理指示。 邊緣資料表的格式可讓您取得未透過中繼屬性公開的額外資訊。 
  [Specify Metaproperties in OPENXML](../xml/specify-metaproperties-in-openxml.md)如需有關中繼內容的詳細資訊，請參閱＜＞。  
  
 邊緣資料表所提供的額外資訊，可讓您儲存及查詢元素和屬性的資料類型，以及節點類型，也可以儲存及查詢 XML 文件結構的相關資訊。 有了這項額外資訊，您還可能建立自己的 XML 文件管理系統。  
  
 藉由使用邊緣資料表，您可以撰寫預存程序以將 XML 文件當作二進位大型物件 (BLOB) 輸入、產生邊緣資料表，然後在更詳細的層級中擷取及分析文件。 此詳細層級可以包含尋找文件階層、元素和屬性名稱、命名空間及處理指示。  
  
 當對應至其他關聯格式不合邏輯，且 ntext 欄位未能提供足夠的結構資訊時，邊緣資料表也可以當作 XML 文件的儲存格式。  
  
 在您可以使用 XML 剖析器來檢查 XML 文件的情況下，您都可以改用邊緣資料表來取得同樣的資訊。  
  
 下表說明邊緣資料表的結構。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**號**|**Bigint**|這是文件節點的唯一識別碼。<br /><br /> 根元素具有識別碼值 0； 負的識別碼值會保留。|  
|**parentid**|**Bigint**|識別節點的父系。 此識別碼所識別的父系，不一定就是父元素； 這一點需根據此識別碼所識別父系的節點 NodeType 而定。 例如，若該節點是文字節點，其父系可能是屬性節點。<br /><br /> 
  **
  ** 如果節點位於 XML 文件的最上層，其 ParentID 為 NULL。|  
|**節點類型**|**int**|用以識別節點類型，而且是對應於 XML 物件模型 (DOM) 節點類型編號的整數。<br /><br /> 以下是可以出現在此資料行中，用來指出節點類型的值：<br /><br /> **1** = 元素節點<br /><br /> **2** = 屬性節點<br /><br /> **3** = 文位元組點<br /><br /> **4** = CDATA 區段節點<br /><br /> **5** = 實體參考節點<br /><br /> **6** = 實體節點<br /><br /> **7** = 處理指示節點<br /><br /> **8** = 批註節點<br /><br /> **9** = 檔節點<br /><br /> **10** = 檔案類型節點<br /><br /> **11** = 檔片段節點<br /><br /> **12** = 標記法節點<br /><br /> 如需詳細資訊，請參閱 Microsoft XML (MSXML) SDK 中的＜nodeType 屬性＞主題。|  
|**localname**|**nvarchar(max)**|提供元素或屬性的本機名稱。 如果 DOM 物件不具有名稱，則為 NULL。|  
|**前置詞**|**nvarchar(max)**|這是節點名稱的命名空間前置詞。|  
|**namespaceuri**|**nvarchar(max)**|這是節點的命名空間 URI。 如果值是 NULL，表示沒有命名空間。|  
|**資料**|**nvarchar(max)**|是元素或屬性資料列的實際資料類型，否則為 NULL。 資料類型是從內嵌 DTD 或內嵌結構描述推斷。|  
|**前**|**Bigint**|這是前一個同層級元素的 XML 識別碼。 如果沒有直接的前一個同層級，則為 NULL。|  
|**text**|**ntext**|包含文字格式的屬性值或元素內容。 若邊緣資料表項目不需要值，則為 NULL。|  
  
#### <a name="using-the-with-clause-to-specify-an-existing-table"></a>使用 WITH 子句指定現有的資料表  
 您可以使用 WITH 子句來指定現有資料表的名稱。 若要這麼做，只需指定現有的資料表名稱，而此資料表的結構描述可讓 OPENXML 用來產生資料列集。  
  
#### <a name="using-the-with-clause-to-specify-a-schema"></a>使用 WITH 子句指定結構描述  
 您可以使用 WITH 子句來指定完整的結構描述。 在指定資料列集結構描述時，您需指定資料行名稱、其資料類型，以及其與 XML 文件的對應。  
  
 您可以利用 SchemaDeclaration 中的 ColPattern 參數來指定資料行模式。 所指定的資料行模式可用來將資料列集資料行對應到由 rowpattern 識別的 XML 節點，並可用來決定對應類型。  
  
 
  *flags* 如果沒有為資料行指定 ColPattern，資料列集資料行會根據  參數所指定的對應，對應至具有相同名稱的 XML 節點。 
  *flags* 但若在 WITH 子句中將 ColPattern 指定成結構描述規格的一部份，則 ColPattern 會覆寫  參數中所指定的對應。  
  
### <a name="mapping-between-the-rowset-columns-and-the-xml-nodes"></a>資料列集資料行與 XML 節點之間的對應  
 在 OPENXML 陳述式中，您可以選擇在資料列集資料行以及 *rowpattern*所識別的 XML 節點之間，指定對應的類型，例如：屬性中心或元素中心。 這項資訊是用於 XML 節點與資料列集資料行之間的轉換。  
  
 您可以用兩種方式來指定對應，也可以兩個項目都指定：  
  
-   
  *
  * 使用 flags 參數  
  
     
  *
  * 由 flags 參數所指定的對應會假設下列條件的名稱對應：XML 節點對應至具有相同名稱的對應資料列集資料行。  
  
-   
  *
  * 使用 ColPattern 參數  
  
     *ColPattern*（XPath 運算式）會在 WITH 子句中指定為*SchemaDeclaration*的一部分。 
  *
  * 在 *ColPattern* 中指定的對應，會覆寫由 flags 參數所指定的對應。  
  
     *ColPattern*可以用來指定對應的類型（例如屬性中心或元素中心），以覆寫或增強*旗*標所指示的預設對應。  
  
     在下列情況下，會指定*ColPattern* ：  
  
    -   資料列集中的資料行名稱，與其對應的元素或屬性名稱不同。 
  *
  * 在此情況下，ColPattern 是用來識別資料列集資料行所對應的 XML 元素及屬性名稱。  
  
    -   您希望將中繼屬性的屬性對應到資料行。 
  *
  * 在此情況下，ColPattern 是用來識別資料列集資料行對應的中繼屬性。 如需如何使用中繼屬性的詳細資訊，請參閱 [在 OPENXML 中指定中繼屬性](../xml/specify-metaproperties-in-openxml.md)。  
  
 
  *flags* 和 *ColPattern* 參數均是選擇性的。 如果未指定對應，則會採用屬性中心對應。 屬性中心對應是 *flags* 參數的預設值。  
  
#### <a name="attribute-centric-mapping"></a>以屬性為主的對應  
 在 OPENXML 中將 *flags* 參數設為 1 (XML_ATTRIBUTES)，就是指定 **屬性中心** 對應。 如果 *flags* 包含 XML_ATTRIBUTES，所公開的資料列集就會提供或取用以每個 XML 元素各代表一個資料列的資料列。 依據名稱對應，XML 屬性會對應至 SchemaDeclaration 中所定義的屬性，或是對應至由 WITH 子句的 Tablename 所提供的屬性。 名稱對應意味著，特定名稱的 XML 屬性會以相同的名稱儲存在資料列集的資料行中。  
  
 
  *
  * 若資料行名稱與其所對應的屬性名稱不同，則必須指定 ColPattern。  
  
 若 XML 屬性具有命名空間限定詞，則資料列集的資料行名稱也必須具有限定詞。  
  
#### <a name="element-centric-mapping"></a>元素中心的對應  
 在 OPENXML 中將 *flags* 參數設為 2 (XML_ELEMENTS)，就是指定 **元素中心** 對應。 它和 **屬性中心** 對應類似，但有以下的差別：  
  
-   除非指定了資料行層級模式，否則對應範例的名稱對應 (例如，資料行對應至具有相同名稱的 XML 元素) 將會選擇非複合式子元素。 在擷取的過程中，若子元素是複合式的 (因為含有額外的子元素)，則資料行將設為 NULL。 所以會忽略子元素的屬性值。  
  
-   若有多個具相同名稱的子元素，則會傳回第一個節點。  
  
## <a name="see-also"></a>另請參閱  
 [sp_xml_preparedocument &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql)   
 [sp_xml_removedocument &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql)   
 [OPENXML &#40;Transact-SQL&#41;](/sql/t-sql/functions/openxml-transact-sql)   
 [XML 資料 &#40;SQL Server&#41;](../xml/xml-data-sql-server.md)  
  
  
