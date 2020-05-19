---
title: 建立 XML 資料的執行個體 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- type casting string instances [XML in SQL Server]
- XML [SQL Server], typed
- xml data type [SQL Server], generating instances
- casting string instances [XML in SQL Server]
- typed XML
- generating XML instances [SQL Server]
- XML [SQL Server], generating instances
- white space [XML in SQL Server]
ms.assetid: dbd6c06f-db6e-44a7-855a-6a55bf374907
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6f0ba7f39d3c95fe992d6603707b2a67d6726b7e
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717114"
---
# <a name="create-instances-of-xml-data"></a>建立 XML 資料的執行個體
  這個主題描述如何產生 XML 執行個體。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，您可以用下列方式產生 XML 執行個體：  
  
-   類型轉換字串執行個體。  
  
-   使用含有 FOR XML 子句的 SELECT 陳述式。  
  
-   使用常數指派。  
  
-   使用大量載入。  
  
## <a name="type-casting-string-and-binary-instances"></a>類型轉換字串和二進位執行個體  
 您可以藉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 由轉換（CAST）或將字串轉換（轉換）為資料類型，將任何字串資料類型（例如 [**n**] [**var**]**char**、 **[n] text**、 **Varbinary**及**image**）剖析成 `xml` 資料類型 `xml` 。 將會檢查不具類型的 XML 以確認它的格式正確。 如果有與類型相關聯的架構 `xml` ，也會執行驗證。 如需詳細資訊，請參閱 [比較具類型的 XML 與不具類型的 XML](compare-typed-xml-to-untyped-xml.md)。  
  
 XML 文件可以使用不同的編碼 (例如，UTF-8、UTF-16、windows-1252) 加以編碼。 以下是字串與二進位來源類型如何與 XML 文件編碼互動以及剖析器作用方式的規則。  
  
 由於 **nvarchar** 假設使用兩個位元組的 Unicode 編碼 (例如 UTF-16 或 UCS-2)，因此 XML 剖析器會將字串值視為兩個位元組的 Unicode 編碼 XML 文件或片段。 這表示必須將 XML 文件以兩個位元組的 Unicode 編碼加以編碼，才能與來源資料類型相容。 雖然 UTF-16 編碼的 XML 文件可有 UTF-16 位元組順序標示 (BOM)，但它並不需要，因為來源類型的內容已經清楚表示，它只能為兩個位元組的 Unicode 編碼文件。  
  
 XML 剖析器會將 **varchar** 字串的內容視為一個位元組編碼的 XML 文件/片段。 由於 **varchar** 來源字串有相關聯的字碼頁，當 XML 本身未明確指定編碼時，剖析器將使用該字碼頁進行編碼。如果 XML 執行個體具有 BOM 編碼宣告，此 BOM 或宣告必須與字碼頁一致，否則剖析器將會報告錯誤。  
  
 **varbinary** 的內容會被視為是直接傳送至 XML 剖析器的字碼指標資料流。 因此，XML 文件或片段必須以內嵌方式提供 BOM 或其他編碼資訊。 剖析器只會查看資料流來決定編碼。 這表示 UTF-16 編碼的 XML 必須提供 UTF-16 BOM，不具有 BOM 和宣告編碼的執行個體將被解譯為 UTF-8。  
  
 如果預先不知道 XML 文件的編碼，且在轉換成 XML 之前，將資料傳送為字串或二進位資料而非 XML 資料，則建議將資料視為 **varbinary**。 例如，使用 OpenRowset() 讀取 XML 檔案的資料時，必須將要讀取的資料指定為 **varbinary(max)** 值：  
  
```  
select CAST(x as XML)   
from OpenRowset(BULK 'filename.xml', SINGLE_BLOB) R(x)  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在內部以 UTF-16 編碼之有效率的二進位表示法來表示 XML。 不會保留使用者提供的編碼，但是會在剖析過程中考慮該編碼。  
  
### <a name="type-casting-clr-user-defined-types"></a>類型轉換 CLR 使用者定義型別  
 如果 CLR 使用者定義型別具有 XML 序列化，即可將該類型的執行個體明確轉換成 XML 資料類型。 如需有關 CLR 使用者定義型別之 XML 序列化的詳細資料，請參閱 [從 CLR 資料庫物件進行 XML 序列化](../../database-engine/dev-guide/xml-serialization-from-clr-database-objects.md)。  
  
### <a name="white-space-handling-in-typed-xml"></a>以具類型的 XML 處理空白  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，元素內容中的空白如果發生在以標記 (如開始或結束標記) 所分隔的僅空白字元資料序列內且未實體化，則會將它視為無意義。 (將會忽略 CDATA 區段。)空白處理的方式與 XML 1.0 規格 (由全球資訊網協會 (W3C) 所發佈) 所述的空白處理方式不同。 這是因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 XML 剖析器，只能辨識有限的 DTD 子集數目，如 XML 1.0 中所定義。 如需有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中所支援之有限 DTD 子集的詳細資訊，請參閱 [CAST 和 CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)。  
  
 依預設，只要下列任一項為真，當 XML 剖析器將字串資料轉換成 XML 時，將會捨棄無意義的空白。  
  
-   `The xml:space` 未在項目或其上階項目定義屬性。  
  
-   在某個元素或在其中一個它的上階元素生效的 `xml:space` 屬性，具有預設值。  
  
 例如：  
  
```  
declare @x xml  
set @x = '<root>      <child/>     </root>'  
select @x   
```  
  
 以下是結果：  
  
```  
<root><child/></root>  
```  
  
 然而，您可以變更此行為。 若要保留 XML DT 執行個體的空白字元，請使用 CONVERT 運算子並將其選擇性的 *style* 參數值設為 1。 例如：  
  
```  
SELECT CONVERT(xml, N'<root>      <child/>     </root>', 1)  
```  
  
 如果未使用 *style* 參數或是將其值設為 0，在轉換 xml DT 執行個體時，將不會保留不重要的空白。 如需如何使用 CONVERT 運算子以及將字串資料轉換成 xmlDT 執行個體時其 *style* 參數的詳細資訊，請參閱 [CAST 和 CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)。  
  
### <a name="example-cast-a-string-value-to-typed-xml-and-assign-it-to-a-column"></a>範例：將字串值轉換成具類型的 xml 並將它指派給資料行  
 下列範例會將包含 XML 片段的字串變數轉換成 `xml` 資料類型，然後將它儲存在類型資料 `xml` 行中：  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
go  
DECLARE  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
```  
  
 下列插入作業會將字串隱含地轉換為 `xml` 類型：  
  
```  
INSERT INTO T VALUES (3, @s)   
```  
  
 您可以明確地將字串轉換為類型（） `xml` ：  
  
```  
INSERT INTO T VALUES (3, cast (@s as xml))  
```  
  
 或者您可以使用 convert()，如下列所示：  
  
```  
INSERT INTO T VALUES (3, convert (xml, @s))   
```  
  
### <a name="example-convert-a-string-to-typed-xml-and-assign-it-to-a-variable"></a>範例：將字串轉換成具類型的 xml 並將它指派給變數  
 在下列範例中，會將字串轉換成 `xml` 類型，並將其指派給 `xml` 資料類型的變數：  
  
```  
declare @x xml  
declare  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
set @x =convert (xml, @s)  
select @x  
```  
  
## <a name="using-the-select-statement-with-a-for-xml-clause"></a>使用含有 FOR XML 子句的 SELECT 陳述式  
 您可以在 SELECT 陳述式中使用 FOR XML 子句以傳回 XML 的結果。 例如：  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = (SELECT Column1, Column2  
               FROM   Table1, Table2  
               WHERE   Some condition  
               FOR XML AUTO)  
 ...  
```  
  
 SELECT 語句會傳回文字 XML 片段，然後在指派至 `xml` 資料類型變數期間進行剖析。  
  
 您也可以在 FOR XML 子句中使用[type](type-directive-in-for-xml-queries.md)指示詞，以直接傳回 for xml 查詢結果作為 `xml` 類型：  
  
```  
Declare @xmlDoc xml  
SET @xmlDoc = (SELECT ProductModelID, Name  
               FROM   Production.ProductModel  
               WHERE  ProductModelID=19  
               FOR XML AUTO, TYPE)  
SELECT @xmlDoc  
```  
  
 以下是結果：  
  
```  
<Production.ProductModel ProductModelID="19" Name="Mountain-100" />...  
```  
  
 在下列範例中， `xml` FOR XML 查詢的具類型結果會插入至類型資料 `xml` 行：  
  
```  
CREATE TABLE T1 (c1 int, c2 xml)  
go  
INSERT T1(c1, c2)  
SELECT 1, (SELECT ProductModelID, Name  
           FROM Production.ProductModel  
           WHERE ProductModelID=19  
           FOR XML AUTO, TYPE)  
SELECT * FROM T1  
go  
```  
  
 如需 FOR XML 的詳細資訊，請參閱 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將 `xml` 資料類型執行個體傳回用戶端，作為不同伺服器建構的結果 (例如使用 TYPE 指示詞的 FOR XML 查詢)，或者使用 `xml` 資料類型從 SQL 資料行、變數和輸出參數傳回 XML。 在用戶端應用程式的程式碼中，ADO.NET 提供者會要求從伺服器以二進位編碼傳送這項 `xml` 資料類型資訊。 但若您使用的 FOR XML 不含 TYPE 指示詞，XML 資料就會以字串類型傳回。 在任一情況下，用戶端提供者將永遠可以處理任一 XML 形式。  
  
## <a name="using-constant-assignments"></a>使用常數指派  
 在預期資料類型的實例時，可以使用字串常數 `xml` 。 這與使用 CAST 將字串隱含轉換成 XML 是相同的。 例如：  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
-- Or  
SET @xmlDoc = N'<?xml version="1.0" encoding="ucs-2"?><doc/>'  
```  
  
 先前的範例會將字串隱含地轉換成 `xml` 資料類型，並將它指派給 `xml` 類型變數。  
  
 下列範例會將常數位串插入型別資料 `xml` 行：  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
INSERT INTO T VALUES (3, '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>')   
```  
  
> [!NOTE]  
>  對於具類型的 XML，將會針對指定的結構描述驗證 XML。 如需詳細資訊，請參閱 [比較具類型的 XML 與不具類型的 XML](compare-typed-xml-to-untyped-xml.md)。  
  
## <a name="using-bulk-load"></a>使用大量載入  
 增強的 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql) 功能，可讓您在資料庫中大量載入 XML 文件。 您可以從檔案將 XML 實例大量載入 `xml` 資料庫中的類型資料行。 如需實用範例，請參閱[大量匯入與匯出 XML 文件的範例 &#40;SQL Server&#41;](../import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)。 如需有關載入 XML 文件的詳細資訊，請參閱 [載入 XML 資料](load-xml-data.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[擷取及查詢 XML 資料](retrieve-and-query-xml-data.md)|描述當 XML 執行個體儲存於資料庫中時，未保留的 XML 執行個體部分。|  
  
## <a name="see-also"></a>另請參閱  
 [比較具類型的 XML 與不具類型的 XML](compare-typed-xml-to-untyped-xml.md)   
 [xml 資料類型方法](/sql/t-sql/xml/xml-data-type-methods)   
 [XML 資料修改語言 &#40;XML DML&#41;](/sql/t-sql/xml/xml-data-modification-language-xml-dml)   
 [XML 資料 &#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
