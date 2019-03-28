---
title: 建立 XML 索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- indexes [XML in SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: 6ecac598-355d-4408-baf7-1b2e8d4cf7c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7da89810a92c14f5b59ebcd546c4fb4cfa256f02
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527512"
---
# <a name="create-xml-indexes"></a>建立 XML 索引
  此主題描述如何建立主要和次要 XML 索引。  
  
## <a name="creating-a-primary-xml-index"></a>建立主要 XML 索引  
 若要建立主要 XML 索引，請使用 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 陳述式。 並非所有供 XML 索引使用的選項都有在 XML 索引中受到支援。  
  
 在建立 XML 索引時請注意下列項目：  
  
-   若要建立主要 XML 索引，包含要索引的 XML 資料行之資料表 (稱為基底資料表)，必須在主索引鍵上有叢集索引。 這將可確保如果基底資料表已分割，可使用相同的資料分割結構描述與資料分割函數來分割主要 XML 索引。  
  
-   如果 XML 索引存在，將無法修改資料表的叢集索引鍵、主索引鍵。 您必須在修改主索引鍵前，先卸除資料表上的所有 XML 索引。  
  
-   在單一 `xml` 類型資料行上可建立主要 XML 索引。 您無法以作為索引鍵資料行的 XML 類型資料行，建立任何其他類型的索引。 不過，您可以在非 XML 索引中包含 `xml` L 類型資料行。 在資料表中的每個 `xml` 類型資料行都有其自己的主要 XML 索引。 不過，每個 `xml` 類型資料行只允許一個主要 XML 索引。  
  
-   XML 索引是存在於與非 XML 索引相同的命名空間中。 因此，在相同名稱的相同資料表上將無法同時擁有 XML 索引與非 XML 索引。  
  
-   IGNORE_DUP_KEY 與 ONLINE 選項永遠為 XML 索引設定為 OFF。 您可用 OFF 的值指定這些選項。  
  
-   使用者資料表的檔案群組或資料分割資訊可套用於 XML 索引。 使用者無法在 XML 索引上分開指定這些選項。  
  
-   DROP_EXISTING 索引選項可卸除主要 XML 索引並建立新的主要 XML 索引，或是卸除次要 XML 索引並建立新的次要 XML 索引。 不過，這個選項無法卸除次要 XML 索引以建立新主要 XML 索引，反之亦然。  
  
-   主要 XML 索引名稱的限制與檢視名稱的限制相同。  
  
 您無法建立 XML 索引上`xml`資料行在檢視中，輸入上**表格**值的變數`xml`類型資料行，或`xml`類型變數。  
  
-   若要使用 ALTER TABLE ALTER COLUMN 選項，將 `xml` 類型資料行從不具類型變更為具類型的 XML (反之亦然)，則在資料行上就不應存在任何 XML 索引。 如果 XML 索引確實存在，必須在嘗試變更資料行類型前先卸除它。  
  
-   在建立 XML 索引時，必須將 ARITHABORT 選項設定為 ON。 若要使用 XML 資料類型方法查詢、插入、刪除或更新 XML 資料行中的值，必須在連接上設定相同的選項。 若未設定，XML 資料類型方法將會失敗。  
  
    > [!NOTE]  
    >  在目錄檢視中可以找到關於 XML 索引的相關資訊。 不過，並不支援 **sp_helpindex** 。 在本主題後面所提供的範例將示範如何查詢目錄檢視，以尋找 XML 索引資訊。  
  
 在包含 XML 結構描述類型 **xs:date** 或 **xs:dateTime** (或是這些類型的任何子類型) 值 (該值的年份小於 1) 的 XML 資料類型資料行上建立或重新建立主要 XML 索引時， [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中的索引建立會失敗。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 允許這些值，所以在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中產生之資料庫內建立索引時，可能會發生這個問題。 如需詳細資訊，請參閱 [比較具類型的 XML 與不具類型的 XML](../xml/compare-typed-xml-to-untyped-xml.md)。  
  
### <a name="example-creating-a-primary-xml-index"></a>範例建立主要 XML 索引  
 在大部分的範例中，都是使用資料表 T (pk INT PRIMARY KEY, xCol XML) 和不具類型的 XML 資料行。 這些都可以用一種直接的方法來擴充成具類型的 XML。 為求簡單明瞭，我們針對 XML 資料執行個體來說明查詢，如下所示：  
  
```  
<book genre="security" publicationdate="2002" ISBN="0-7356-1588-2">  
   <title>Writing Secure Code</title>  
   <author>  
      <first-name>Michael</first-name>  
      <last-name>Howard</last-name>  
   </author>  
   <author>  
      <first-name>David</first-name>  
      <last-name>LeBlanc</last-name>  
   </author>  
   <price>39.99</price>  
</book>  
```  
  
 下列陳述式會在資料表 T 的 XML 資料行 xCol 上建立一個名為 idx_xCol 的 XML 索引：  
  
```  
CREATE PRIMARY XML INDEX idx_xCol on T (xCol)  
```  
  
## <a name="creating-a-secondary-xml-index"></a>建立次要 XML 索引  
 您可以使用 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 陳述式來建立次要 XML 索引，並指定您所需的次要 XML 索引類型。  
  
 在建立次要 XML 索引時請注意下列項目：  
  
-   除了 IGNORE_DUP_KEY 與 ONLINE 之外，所有套用至非叢集索引的索引選項都可在次要 XML 索引上使用。 對於次要 XML 索引，有兩個選項必須永遠設定為 OFF。  
  
-   次要索引會像主要 XML 索引一樣進行分割。  
  
-   DROP_EXISTING 可以卸除使用者資料表上的次要索引，並在使用者資料表上建立其他次要索引。  
  
 您可以查詢 **sys.xml_indexes** 目錄檢視，以便擷取 XML 索引資訊。 請注意，在 **sys.xml_indexes** 目錄檢視中的 **secondary_type_desc** 資料行會提供次要索引的類型：  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 在 **secondary_type_desc** 資料行中傳回的值可以是 NULL、PATH、VALUE 或 PROPERTY。 對於主要 XML 索引而言，傳回的值是 NULL。  
  
### <a name="example-creating-secondary-xml-indexes"></a>範例建立次要 XML 索引  
 下列範例說明如何建立次要 XML 索引。 此範例也會顯示您已建立之 XML 索引的相關資訊。  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML);  
GO  
-- Create primary index.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol);  
GO  
-- Create secondary indexes (PATH, VALUE, PROPERTY).  
CREATE XML INDEX PIdx_T_XmlCol_PATH ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PATH;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_VALUE ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR VALUE;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_PROPERTY ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PROPERTY;  
GO  
```  
  
 您可以查詢 `sys.xml_indexes` 來擷取 XML 索引資訊。 `secondary_type_desc` 資料行會提供次要索引類型。  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 您也可以查詢目錄檢視以便取得索引資訊。  
  
```  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T');  
```  
  
 您可以加入範例資料，然後檢閱 XML 索引資訊。  
  
```  
INSERT INTO T VALUES (1,  
'<doc id="123">  
<sections>  
<section num="2">  
<heading>Background</heading>  
</section>  
<section num="3">  
<heading>Sort</heading>  
</section>  
<section num="4">  
<heading>Search</heading>  
</section>  
</sections>  
</doc>');  
GO  
-- Check XML index information.  
SELECT *  
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, NULL, 'DETAILED');  
GO  
-- Space usage of primary XML index  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id  
FROM    sys.xml_indexes i   
WHERE   i.name = 'PIdx_T_XmlCol' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
--- Space usage of secondary XML index (for example PATH secondary index)  PIdx_T_XmlCol_PATH  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id   
FROM    sys.xml_indexes i   
WHERE  i.name = 'PIdx_T_XmlCol_PATH' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
  
-- Space usage of all secondary XML indexes for a particular table  
SELECT i.name, object_name(i.object_id), stats.*   
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, DEFAULT, 'DETAILED') stats  
JOIN sys.xml_indexes i ON (stats.object_id = i.object_id and stats.index_id = i.index_id)  
WHERE secondary_type is not null;  
-- Drop secondary indexes.  
DROP INDEX PIdx_T_XmlCol_PATH ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_VALUE ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_PROPERTY ON T;  
GO  
-- Drop primary index.  
DROP INDEX PIdx_T_XmlCol ON T;  
-- Drop table T.  
DROP TABLE T;  
Go  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 索引 &#40;SQL Server&#41;](xml-indexes-sql-server.md)   
 [XML 資料 &#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
