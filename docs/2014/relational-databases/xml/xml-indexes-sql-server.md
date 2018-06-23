---
title: XML 索引 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- removing indexes
- deleting indexes
- secondary indexes [XML in SQL Server]
- xml data type [SQL Server], indexes
- dropping indexes
- PATH index
- DROP_EXISTING clause
- XML [SQL Server], indexes
- primary indexes [XML in SQL Server]
- indexes [SQL Server], XML
- XML indexes [SQL Server], secondary
- BLOBs, XML indexes
- disabling indexes
- XML indexes [SQL Server], modifying
- XML indexes [SQL Server]
- XML indexes [SQL Server], primary
- modifying indexes
- XML indexes [SQL Server], dropping
- VALUE index
- XML indexes [SQL Server], xml data type
- PROPERTY index
- XML indexes [SQL Server], creating
ms.assetid: f5c9209d-b3f3-4543-b30b-01365a5e7333
caps.latest.revision: 58
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: aeb1c0f282e0cb46bcb1e35af933a67b84eb4e0d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033195"
---
# <a name="xml-indexes-sql-server"></a>XML 索引 (SQL Server)
  上可以建立 XML 索引`xml`資料類型資料行。 它們會在資料行中為整個 XML 執行個體的所有標記、值和路徑編制索引，進而提高查詢效能。 在下列情況下，您的應用程式可從 XML 索引獲益：  
  
-   在您的工作負載中，經常會查詢 XML 資料行。 必須將資料修改期間的 XML 索引維護成本納入考量。  
  
-   您的 XML 值相對較大，而所擷取的部份相對較小。 建立索引可避免在執行階段剖析整份資料，並有助於索引查閱，增進查詢處理的效率。  
  
 XML 索引可分成下列類別：  
  
-   主要 XML 索引  
  
-   次要 XML 索引  
  
 在 `xml` 類型資料行上的第一個索引必須是主要的 XML 索引。 使用主要 XML 索引時，可支援下列次要索引類型：PATH、VALUE 及 PROPERTY。 視查詢類型而定，這些次要索引可協助改善查詢效能。  
  
> [!NOTE]  
>  除非您已正確設定資料庫選項來處理 `xml` 資料類型一起運作，否則無法建立或修改 XML 索引。 如需詳細資訊，請參閱 [使用 XML 資料行進行全文檢索搜尋](use-full-text-search-with-xml-columns.md)。  
  
 XML 執行個體是以大型二進位物件 (BLOB) 儲存在 `xml` 類型資料行中。 這些 XML 執行個體可以是大型的，而且所儲存之 `xml` 資料類型執行個體的二進位表示法最多可達 2 GB。 如果沒有索引，這些二進位大型物件就會在執行階段切割，以便評估查詢。 這項切割作業可能會很費時。 例如，請考慮下列查詢：  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 為了選取符合 `WHERE` 子句中條件的 XML 執行個體，在執行階段會切割 `Production.ProductModel` 資料表之每個資料列中的 XML 二進位大型物件 (BLOB)。 然後，便評估 `(/PD:ProductDescription/@ProductModelID[.="19"]`方法中的運算式 `exist()` )。 此執行階段的切割可能會非常費時，端視資料行中所儲存的執行個體之大小與數目而定。  
  
 如果查詢 XML 二進位大型物件 (Blob) 常在應用程式環境中，它可協助索引`xml`類型資料行。 但是，在修改資料期間會有維護索引的相關成本。  
  
## <a name="primary-xml-index"></a>主要 XML 索引  
 主要 XML 索引會在 XML 資料行中檢索 XML 執行個體內的所有標記、值與路徑。 若要建立主要 XML 索引，出現 XML 資料行之資料表必須在資料表的主索引鍵上，具有叢集索引。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用此主索引鍵，以將主要 XML 索引中的資料列與內含 XML 資料行之資料表中的資料列相互關聯。  
  
 主要 XML 索引是中的 XML Blob 的切割和保存表示`xml`資料類型資料行。 對於資料行中的每個 XML 二進位大型物件 (BLOB) 而言，索引可建立幾個資料列。 索引中的資料列數目大約等於 XML 二進位大型物件中的節點數目。 當查詢擷取完整 XML 執行個體時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會從 XML 資料行提供此執行個體。 XML 執行個體中的查詢會使用主要 XML 索引，並使用索引本身來傳回純量值或 XML 子樹。  
  
 每個資料列都會儲存下列節點資訊：  
  
-   類似元素或屬性名稱的標記名稱。  
  
-   節點值。  
  
-   如元素節點、屬性節點或文字節點等節點類型。  
  
-   文件順序資訊，以內部節點識別碼表示。  
  
-   從每個節點至 XML 樹狀結構根節點的路徑。 在查詢中會為路徑運算式搜尋資料行。  
  
-   基底資料表的主索引鍵。 基底資料表的主索引鍵會在主要 XML 索引中重複，以利向後聯結基底資料表，而基底資料表主索引鍵中資料行的最大數目是限定為 15。  
  
 此節點資訊是用以評估和建構指定查詢的 XML 結果。 為了達到最佳化，標記名稱與節點類型資訊將會編碼成整數值，而 Path 資料行則會使用相同的編碼。 另外，當只知道路徑後置詞時，會以相反順序儲存路徑以允許比對路徑。 例如：  
  
-   `//ContactRecord/PhoneNumber` 只知道最後兩個步驟  
  
 或  
  
-   `/Book/*/Title` 於運算式的中間指定了萬用字元 (`*`)。  
  
 查詢處理器會使用主要 XML 索引來進行包含 [xml 資料類型方法](/sql/t-sql/xml/xml-data-type-methods) 的查詢，並從主要索引本身傳回純量值或 XML 子樹。 (這個索引會儲存重新建構 XML 執行個體的所有必要資訊)。  
  
 例如，下列查詢會傳回摘要資訊儲存在`CatalogDescription``xml`類型資料行中的`ProductModel`資料表。 此查詢只會針對目錄描述也儲存 <`Features`> 描述的產品型號傳回其 <`Summary`> 資訊。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")SELECT CatalogDescription.query('  /PD:ProductDescription/PD:Summary') as ResultFROM Production.ProductModelWHERE CatalogDescription.exist ('/PD:ProductDescription/PD:Features') = 1  
```  
  
 至於主要 XML 索引，而不是切割基底資料表中每個 XML 二進位大型物件的執行個體，會針對 `exist()` 方法中所指定的運算式，循序搜尋索引中與每個 XML 二進位大型物件相對應的資料列。 如果在索引中的 Path 資料行找到了路徑，就會從主要 XML 索引擷取 <`Summary`> 元素及其子樹，並將其轉換為 XML 二進位大型物件，當做 `query()` 方法的結果。  
  
 請注意，在擷取完整 XML 執行個體時不會使用主要 XML 索引。 例如，下列查詢會從資料表擷取整個 XML 執行個體，該執行個體描述了特定產品型號的製造指示。  
  
```  
USE AdventureWorks2012;SELECT InstructionsFROM Production.ProductModel WHERE ProductModelID=7;  
```  
  
## <a name="secondary-xml-indexes"></a>次要 XML 索引  
 若要增強搜尋效能，您可以建立次要的 XML 索引。 在建立次要索引之前，必須先有主要 XML 索引存在。 以下為其類型：  
  
-   PATH 次要 XML 索引  
  
-   VALUE 次要 XML 索引  
  
-   PROPERTY 次要 XML 索引  
  
 以下是建立一或多個次要索引的一些指導方針：  
  
-   如果您的工作負載在 XML 資料行上大量使用路徑運算式，PATH 次要 XML 索引就可能會加速您的工作負載。 最常見的情況是將 **exist()** 方法使用在 Transact-SQL 的 WHERE 子句中的 XML 資料行上。  
  
-   如果您的工作負載使用路徑運算式，從個別的 XML 執行個體中擷取多個值，則在 PROPERTY 索引中將路徑叢集在每個 XML 執行個體中，可能會有所幫助。 當物件的屬性被提取，且已知其主索引鍵值時，此案例通常會發生在屬性包案例中。  
  
-   如果您的工作負載需要查詢 XML 執行個體中的值，但您不知道含有那些值的元素或屬性名稱，您可能會想要建立 VALUE 索引。 這通常會發生在子系座標軸查閱，例如 //author[last-name="Howard"]，其中 \<author> 項目可出現在階層中的任何層級。 這也會發生在萬用字元查詢中，例如 /book [@* = "novel"]，此查詢是要尋找屬性中具有 "novel" 值的 \<book> 項目。  
  
### <a name="path-secondary-xml-index"></a>PATH 次要 XML 索引  
 如果您的查詢通常會在 `xml` 類型資料行上指定路徑運算式，則使用 PATH 次要索引將可使搜尋速度變快。 如本主題前面所述，當您的查詢在 WHERE 子句中指定 **exist()** 方法時，主索引就非常有用。 如果您加入 PATH 次要索引，也可以改善這類查詢的搜尋效能。  
  
 雖然主要 XML 索引可避免必須在執行階段切割 XML 二進位大型物件，但是它可能無法為以路徑運算式為基礎的查詢提供最佳的效能。 由於會針對大型 XML 執行個體，循序搜尋與 XML 二進位大型物件相對應的主要 XML 索引中的所有資料列，因此循序搜尋可能會很慢。 在此情況下，將次要索引建立在主要索引的路徑值與節點值上，將可大幅增加索引搜尋的速度。 在 PATH 次要索引中，路徑與節點值都是索引鍵資料行，可在搜尋路徑時進行更有效率的搜尋。 查詢最佳化工具可以針對如下列所示的運算式使用 PATH 索引：  
  
-   `/root/Location` 其僅指定路徑  
  
 或  
  
-   `/root/Location/@LocationID[.="10"]` 其中同時指定了路徑與節點值。  
  
 下列查詢顯示 PATH 索引非常有用：  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 在查詢中， `/PD:ProductDescription/@ProductModelID` 方法中的路徑運算式 `"19"` 與 `exist()` 值會對應至 PATH 索引的索引鍵欄位。 這允許在 PATH 索引中進行直接搜尋，並對主索引中的路徑值提供比循序搜尋更佳的搜尋效能。  
  
### <a name="value-secondary-xml-index"></a>VALUE 次要 XML 索引  
 如果查詢是以值為基礎，例如， `/Root/ProductDescription/@*[. = "Mountain Bike"]` 或 `//ProductDescription[@Name = "Mountain Bike"]`，且並未完整指定路徑，或是路徑中包含萬用字元，您可以透過在主要 XML 索引的節點值上建立次要 XML 索引，以獲得更快的結果。  
  
 VALUE 索引的索引鍵資料行是主要 XML 索引的節點值與路徑。 如果您的工作負載需要在不知道包含值的元素或屬性名稱的情況下，從 XML 執行個體查詢值，VALUE 索引將會非常有用。 例如，下列運算式將可從擁有 VALUE 索引而獲益：  
  
-   `//author[LastName="someName"]`，其中您知道 <`LastName`> 元素的值，但是 <`author`> 父系可存在於任何位置。  
  
-   在 `/book[@* = "someValue"]` 中，查詢會尋找某些屬性中包含值 `"someValue"` 的 <`book`> 元素。  
  
 下列查詢會從 `ContactID` 資料表傳回 `Contact` 。 `WHERE`子句可指定篩選，中尋找值`AdditionalContactInfo``xml`類型資料行。 如果對應的其他連絡資訊 XML 二進位大型物件包含特定的電話號碼，就會傳回連絡識別碼。 因為 <`telephoneNumber`> 元素有可能出現在 XML 的任何位置，所以路徑運算式會指定 descendent-or-self 軸。  
  
```  
WITH XMLNAMESPACES (  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS CI,  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.exist('//ACT:telephoneNumber/ACT:number[.="111-111-1111"]') = 1  
```  
  
 在此情況下，雖然已得知 <`number`> 的搜尋值，但它有可能以 <`telephoneNumber`> 元素的子系出現在 XML 執行個體中的任何位置。 此類的查詢可從以特定值為基礎的索引查閱獲益。  
  
### <a name="property-secondary-index"></a>PROPERTY 次要索引  
 從個別 XML 執行個體擷取一或多個值的查詢可從 PROPERTY 索引獲益。 當您擷取物件屬性使用時，就會發生這種情況下**value （)** 方法`xml`類型和當物件的主索引鍵值為已知的。  
  
 PROPERTY 索引是建立在主要 XML 索引的資料行 (PK、Path 以及節點值) 上，在主要 XML 索引中 PK 是基底資料表的主索引鍵。  
  
 例如，若為產品型號 `19`，下列查詢就會使用 `ProductModelID` 方法來擷取 `ProductModelName` 和 `value()` 屬性值。 PROPERTY 索引可提供比使用主要 XML 索引或其他次要 XML 索引更快的執行。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.value('(/PD:ProductDescription/@ProductModelID)[1]', 'int') as ModelID,  
       CatalogDescription.value('(/PD:ProductDescription/@ProductModelName)[1]', 'varchar(30)') as ModelName          
FROM Production.ProductModel     
WHERE ProductModelID = 19  
```  
  
 本主題稍後所述的差異，除了建立 XML 索引上`xml`類型資料行是類似於建立非索引`xml`類型資料行。 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 陳述式可用以建立及管理 XML 索引：  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)  
  
-   [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
## <a name="getting-information-about-xml-indexes"></a>取得有關 XML 索引的資訊  
 XML 索引項目會出現在目錄檢視 sys.indexes 中，且具有索引 "type" 3。 名稱資料行包含此 XML 索引的名稱。  
  
 XML 索引也會記錄在目錄檢視 sys.xml_indexes 中。 其中包含 sys.indexes 的所有資料行，以及對 XML 索引有助益的一些特定資料行。 資料行 secondary_type 中的 NULL 值是指主要 XML 索引；'P'、'R' 和 'V' 這三個值分別代表 PATH、PROPERTY 和 VALUE 次要 XML 索引。  
  
 XML 索引使用的空間可以在資料表值函式 [sys.dm_db_index_physical_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql)中找到。 其提供所有索引類型的資訊，例如：所佔用的磁碟分頁數量、平均資料列大小 (位元組)，以及記錄的數量。 另外還包含 XML 索引。 每個資料庫分割區都有此資訊。 XML 索引使用相同的基底資料表分割區配置及分割區功能。  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql)   
 [XML 資料 &#40;SQL Server&#41;](../xml/xml-data-sql-server.md)  
  
  
