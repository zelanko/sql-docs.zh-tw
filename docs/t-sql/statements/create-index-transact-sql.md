---
title: "建立索引 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE INDEX
- INDEX
- INDEX_TSQL
- CREATE_INDEX_TSQL
dev_langs: TSQL
helpviewer_keywords:
- CREATE XML INDEX statement
- PRIMARY XML INDEX statement
- indexes [SQL Server], creating
- online index operations
- index keys [SQL Server]
- PROPERTY INDEX statement
- computed columns, index creation
- clustered indexes, creating
- indexed views [SQL Server], index creation
- partitioned indexes [SQL Server], creating
- VALUE INDEX statement
- index creation [SQL Server], CREATE INDEX statement
- DROP_EXISTING clause
- row locks [SQL Server]
- composite indexes
- MAXDOP index option, CREATE INDEX statement
- filtered indexes [SQL Server], creating
- PATH INDEX statement
- locking [SQL Server], indexes
- unique indexes, creating
- primary indexes [SQL Server]
- CREATE PRIMARY XML INDEX statement
- SET statement, index creation
- index options [SQL Server]
- included columns
- ONLINE option
- nonclustered indexes [SQL Server], creating
- CREATE INDEX statement
- IGNORE_DUP_KEY option
- deterministic functions
- keys [SQL Server], index
- SECONDARY XML INDEX statement
- page locks [SQL Server]
- secondary indexes [SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: d2297805-412b-47b5-aeeb-53388349a5b9
caps.latest.revision: "223"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 92e32f9a86265376a67466aa389f29ec9608a061
ms.sourcegitcommit: 4a462c7339dac7d3951a4e1f6f7fb02a3e01b331
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/07/2017
---
# <a name="create-index-transact-sql"></a>CREATE INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在資料表或檢視表上建立關聯式索引。 因為它是其中一個非叢集或非叢集 btree 索引時，也稱為資料列存放區索引。 資料表中有資料之前，您可以建立資料列存放區索引。 若要改善查詢效能，特別是在查詢從特定資料行中選取，或需要特定的順序排序值時，才使用資料列存放區索引。  
  
  
> [!NOTE]  
>  Azure SQL 資料倉儲和平行處理資料倉儲目前不支援 Unique 條件約束。 參考唯一的條件約束的任何範例僅適用於 SQL Server 和 Azure SQL Database    
  
 **簡單的範例：**  
  
```  
-- Create a nonclustered index on a table or view  
CREATE INDEX i1 ON t1 (col1);  
```  
  
```  
--Create a clustered index on a table and use a 3-part name for the table  
CREATE CLUSTERED INDEX i1 ON d1.s1.t1 (col1);  
```  
  
```  
-- Syntax for SQL Server and Azure SQL Database
-- Create a nonclustered index with a unique constraint 
-- on 3 columns and specify the sort order for each column  
CREATE UNIQUE INDEX i1 ON t1 (col1 DESC, col2 ASC, col3 DESC);  
```  
  
 **重要的案例：**  
  
-   在 SQL Server 2016 和 Azure SQL Database 中，使用非叢集索引資料行存放區索引來改善資料倉儲查詢效能。 請參閱[資料行存放區索引的資料倉儲](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
  
 **需要建立不同類型的索引？**  
  
-   [建立 XML 索引 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)  
  
-   [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)  
  
-   [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database
  
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON <object> ( column [ ASC | DESC ] [ ,...n ] )   
    [ INCLUDE ( column_name [ ,...n ] ) ]  
    [ WHERE <filter_predicate> ]  
    [ WITH ( <relational_index_option> [ ,...n ] ) ]  
    [ ON { partition_scheme_name ( column_name )   
         | filegroup_name   
         | default   
         }  
    ]  
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]  
  
[ ; ]  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
  
<relational_index_option> ::=  
{  
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | STATISTICS_INCREMENTAL = { ON | OFF }  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = { ON | OFF }  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = { NONE | ROW | PAGE}   
     [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
     [ , ...n ] ) ]  
}  
  
<filter_predicate> ::=   
    <conjunct> [ AND <conjunct> ]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,...n)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    { IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !< }  
  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
  
Backward Compatible Relational Index  
Important   The backward compatible relational index syntax structure 
will be removed in a future version of SQL Server. Avoid using this 
syntax structure in new development work, and plan to modify 
applications that currently use the feature. Use the syntax structure 
specified in <relational_index_option> instead.  
  
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON <object> ( column_name [ ASC | DESC ] [ ,...n ] )   
    [ WITH <backward_compatible_index_option> [ ,...n ] ]  
    [ ON { filegroup_name | "default" } ]  
  
<object> ::=  
{  
    [ database_name. [ owner_name ] . | owner_name. ]   
    table_or_view_name  
}  
  
<backward_compatible_index_option> ::=  
{   
    PAD_INDEX  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB  
  | IGNORE_DUP_KEY  
  | STATISTICS_NORECOMPUTE   
  | DROP_EXISTING   
}  
```  

  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON [ database_name . [ schema ] . | schema . ] table_name   
        ( { column [ ASC | DESC ] } [ ,...n ] )  
    WITH ( DROP_EXISTING = { ON | OFF } )  
[;]  
  
```  
  
## <a name="arguments"></a>引數  
 UNIQUE  
 在資料表或檢視表上建立唯一索引。 在唯一索引中，任兩個資料列都不能有相同的索引鍵值。 檢視表中的叢集索引必須是唯一的。  
  
 不論 IGNORE_DUP_KEY 是否設為 ON，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 都不允許在已包含重複值的資料行上建立唯一索引。 如果嘗試執行這項作業，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會顯示錯誤訊息。 必須先移除重複值，才能在資料行上建立唯一索引。 唯一索引中使用的資料行應設為 NOT NULL，因為當建立唯一索引時，多個 Null 值會被視為重複值。  
  
 CLUSTERED  
 建立一個索引，在該索引中，索引鍵值的邏輯順序會決定資料表中對應資料列的實體順序。 叢集索引的層級 (底部或分葉) 包含資料表的實際資料列。 資料表或檢視表一次只允許一個叢集索引。  
  
 含有唯一叢集索引的檢視表稱為索引檢視表。 在檢視表上建立唯一叢集索引，可將檢視表實際具體化。 必須先在檢視表上建立唯一叢集索引，才能在相同檢視表上定義任何其他索引。 如需詳細資訊，請參閱 [建立索引檢視表](../../relational-databases/views/create-indexed-views.md)。  
  
 先建立叢集索引，再建立任何非叢集索引。 當建立叢集索引時，會重建資料表上現有的非叢集索引。  
  
 如果未指定 CLUSTERED，就會建立非叢集索引。  
  
> [!NOTE]  
>  因為叢集的索引和資料頁的分葉層級是以相同方式定義，建立叢集的索引，並使用 ON *partition_scheme_name*或 ON *filegroup_name*子句有效從建立資料表的檔案群組的資料表移到新的分割區配置或檔案群組中。 在特定檔案群組上建立資料表或索引之前，請先確認檔案群組是可用的，而且它們有足夠的空間可供索引使用。  
  
 在某些情況下，建立叢集索引可啟用先前停用的索引。 如需詳細資訊，請參閱[Enable Indexes and Constraints](../../relational-databases/indexes/enable-indexes-and-constraints.md)和[停用索引和條件約束](../../relational-databases/indexes/disable-indexes-and-constraints.md)。  
  
 **非叢集**  
 建立索引來指定資料表的邏輯排序。 如果是非叢集索引，資料列的實體順序和它們的索引順序無關。  
  
 不論索引的建立方式為何，每一份資料表最多只能有 999 個非叢集索引：以隱含的方式使用 PRIMARY KEY 和 UNIQUE 條件約束或以明確的方式使用 CREATE INDEX。  
  
 如果是索引檢視表，只能在已定義唯一叢集索引的檢視表上建立非叢集索引。  
  
 預設值是 NONCLUSTERED。  
  
 *index_name*  
 這是索引的名稱。 在資料表或檢視表內，索引名稱必須是唯一的，但在資料庫內就不一定要是唯一的。 索引名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。  
  
 *column*  
 這是做為索引根據的資料行。 您可以指定兩個或兩個以上的資料行名稱，在指定之資料行的合計值上建立複合索引。 列出要包含在複合的索引，排序優先權順序之後, 在括號內的資料行*table_or_view_name*。  
  
 最多 32 個資料行可以結合成單一複合索引鍵。 複合索引鍵中的所有資料行都必須在相同的資料表或檢視表中。 結合的索引值的允許大小上限是 900 個位元組的叢集索引或非叢集索引為 1,700。 限制為 16 個資料行與之前的版本 900 個位元組[!INCLUDE[ssSDS](../../includes/sssds-md.md)]V12 和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。  
  
 大型物件 (LOB) 資料類型的資料行**ntext**，**文字**， **varchar （max)**， **nvarchar （max)**， **varbinary （max)**， **xml**，或**映像**不能指定為索引鍵資料行。 此外，不能包含檢視定義**ntext**，**文字**，或**映像**資料行，即使它們不能以 CREATE INDEX 陳述式參考。  
  
 如果 CLR 使用者定義型別支援二進位排序，您可以在該型別的資料行上建立索引。 只要方法標示為具決定性且不執行資料存取作業，您也可以在定義為使用者定義型別資料行方法引動過程的計算資料行上建立索引。 如需有關 CLR 使用者定義型別資料行編製索引的詳細資訊，請參閱[CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
 [ **ASC** |DESC]  
 決定特定索引資料行的遞增或遞減排序方向。 預設值是 ASC。  
  
 包含**(***資料行*[ **，**...*n* ] **)**  
 指定要加入至非叢集索引分葉層級的非索引鍵資料行。 非叢集索引可以是唯一或非唯一的。  
  
 資料行名稱在 INCLUDE 清單中不能重複，且不能同時做為索引鍵資料行和非索引鍵資料行。 如果資料表上有定義叢集索引，非叢集索引一定會包含叢集索引資料行。 如需詳細資訊，請參閱 [建立內含資料行的索引](../../relational-databases/indexes/create-indexes-with-included-columns.md)。  
  
 允許所有的資料類型，除了 **text**、 **ntext**和 **image**以外。 必須建立或離線重建索引 （ONLINE = OFF） 所指定的非索引鍵資料任何的行一個是否**varchar （max)**， **nvarchar （max)**，或**varbinary （max)**資料型別。  
  
 具決定性之精確或非精確的計算資料行都可以當做內含資料行。 計算資料行，衍生自**映像**， **ntext**，**文字**， **varchar （max)**， **nvarchar （max)**，**varbinary （max)**，和**xml**資料類型可以包含非索引鍵資料行中，只要計算資料行資料類型時，才允許內含資料行。 如需詳細資訊，請參閱 [計算資料行的索引](../../relational-databases/indexes/indexes-on-computed-columns.md)。  
  
 如需建立 XML 索引資訊，請參閱[CREATE XML INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md).  
  
 其中\<filter_predicate > 藉由指定要在索引中包含的資料列建立篩選的索引。 已篩選的索引必須是資料表上的非叢集索引。 針對已篩選之索引中的資料列建立已篩選的統計資料。  
  
 篩選述詞會使用簡單比較邏輯，而且無法參考計算資料行、UDT 資料行、空間資料類型資料行或 hierarchyID 資料類型資料行。 比較運算子不允許使用 NULL 常值的比較。 請改用 IS NULL 和 IS NOT NULL 運算子。  
  
 下面是一些 `Production.BillOfMaterials` 資料表之篩選述詞的範例：  
  
 * `WHERE StartDate > '20000101' AND EndDate <= '20000630'`  
  
 * `WHERE ComponentID IN (533, 324, 753)`  
  
 * `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
  
 已篩選的索引不適用於 XML 索引和全文檢索索引。 如果是 UNIQUE 索引，只有選取的資料列必須有唯一的索引值。 已篩選的索引不允許 IGNORE_DUP_KEY 選項。  
  
 ON *partition_scheme_name***(***column_name***)**  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定分割區配置來定義要做為分割區索引之分割區對應目標的檔案群組。 資料分割配置必須存在於資料庫中執行[CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)或[ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md)。 *column_name*指定資料分割的索引將會分割依據的資料行。 此資料行必須符合資料類型、 長度和有效位數引數的資料分割函式， *partition_scheme_name*使用。 *column_name*未限制為索引定義中的資料行。 基底資料表中的任何資料行都可以指定，但在分割唯一索引， *column_name*必須選擇從做的唯一索引鍵。 這項限制可讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 只在單一分割區內驗證索引鍵值的唯一性。  
  
> [!NOTE]  
>  當您分割一個非唯一的叢集索引時，如果尚未指定分割區資料行，依預設，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將它加入至叢集索引鍵清單。 當您分割一個非唯一的非叢集索引時，如果尚未指定分割區資料行，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將它新增為索引的非索引鍵 (內含) 資料行。  
  
 如果*partition_scheme_name*或*檔案群組*未指定和資料表資料分割，此索引會放在相同的資料分割配置，使用相同的分割資料行，做為基礎的資料表。  
  
> [!NOTE]  
>  您無法在 XML 索引上指定分割區配置。 如果基底資料表已分割，XML 索引會使用與資料表相同的分割區配置。  
  
 如需有關資料分割索引， [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。  
  
 ON *filegroup_name*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 在指定的檔案群組上建立指定的索引。 如果未指定位置，且資料表或檢視表未分割，則索引會使用與基礎資料表或檢視表相同的檔案群組。 此檔案群組必須已存在。  
  
 ON **"**預設**"**  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssCurrent](../../includes/sssdsfull-md.md)]。  
  
 在預設的檔案群組上建立指定的索引。  
  
 在這個內容中，default 這個字不是關鍵字。 它是預設檔案群組的識別碼，必須加以分隔，如 ON **"**預設**"**或 ON **[**預設**]**。 如果指定了 "default"，目前工作階段的 QUOTED_IDENTIFIER 選項就必須是 ON。 這是預設值。 如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
 [FILESTREAM_ON { *filestream_filegroup_name* | *partition_scheme_name* |"NULL"}]  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定在建立叢集索引時，資料表之 FILESTREAM 資料的位置。 FILESTREAM_ON 子句允許將 FILESTREAM 資料移到不同的 FILESTREAM 檔案群組或分割區配置。  
  
 *filestream_filegroup_name*是 FILESTREAM 檔案群組的名稱。 此檔案群組必須有一個檔案群組使用檔案群組定義[CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md)或[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)陳述式; 否則就會引發錯誤。  
  
 如果分割此資料表，則必須包含 FILESTREAM_ON 子句，而且必須指定 FILESTREAM 檔案群組的分割區配置，此配置會使用與資料表之分割區配置相同的分割區函數和分割區資料行。 否則，就會引發錯誤。  
  
 如果此資料表未分割，FILESTREAM 資料行將無法分割。 此資料表的 FILESTREAM 資料必須儲存在 FILESTREAM_ON 子句中指定的單一檔案群組內。  
  
 如果正在建立叢集索引，而且此資料表不包含 FILESTREAM 資料行，則可以在 CREATE INDEX 陳述式內指定 FILESTREAM_ON NULL。  
  
 如需詳細資訊，請參閱 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)。  
  
 **\<物件 >:: =**  
  
 這是要建立索引的完整或非完整物件。  
  
 *database_name*  
 這是資料庫的名稱。  
  
 *schema_name*  
 這是資料表或檢視表所屬的結構描述名稱。  
  
 *table_or_view_name*  
 這是要建立索引之資料表或檢視表的名稱。  
  
 必須利用 SCHEMABINDING 定義檢視表，才能在該檢視表上建立索引。 必須先在檢視表上建立唯一叢集索引，才能建立任何非叢集索引。 如需有關索引檢視表的詳細資訊，請參閱「備註」一節。  
  
 開頭為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，此物件可以儲存具有叢集資料行存放區索引的資料表。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]支援三部分名稱格式*database_name***。**[*schema_name*]**。***object_name*時*database_name*是目前的資料庫或*database_name*是 tempdb 和*object_name*開頭為 #。  
  
 **\<relational_index_option >:: =**  
  
 指定當您建立索引時所需使用的選項。  
  
 PAD_INDEX = {ON |**OFF** }  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定索引填補。 預設值為 OFF。  
  
 ON  
 所指定的可用空間百分比*填滿因數*會套用到索引的中繼層級頁面。  
  
 關閉或*填滿因數*未指定  
 中繼層級頁面會幾乎填滿整個容量，但會考量中繼頁面上的索引鍵集，而保留至少可供索引所能擁有之大小上限的一個資料列使用的足夠空間。  
  
 只有在指定 FILLFACTOR 時，才能使用 PAD_INDEX 選項，因為 PAD_INDEX 會使用 FILLFACTOR 所指定的百分比。 如果 FILLFACTOR 所指定的百分比不夠，無法允許一個資料列，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會在內部覆寫該百分比以允許最小值。 中繼索引頁上的資料列數目絕不會是小於兩個，不論如何低的值為何*填滿因數*。  
  
 在與舊版本相容的語法中，WITH PAD_INDEX 相當於 WITH PAD_INDEX = ON。  
  
 填滿因數 **=** *填滿因數*  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定用以指出建立或重建索引時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 填滿各索引頁面分葉層級之程度的百分比。 *填滿因數*必須是介於 1 到 100 之間的整數值。 如果*填滿因數*是 100，[!INCLUDE[ssDE](../../includes/ssde-md.md)]會利用已填滿容量的分葉頁面建立索引。  
  
 只有在建立或重建索引時才會套用 FILLFACTOR 設定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 不會動態保留頁面中空白空間的指定百分比。 若要檢視填滿因數設定，請使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目錄檢視。  
  
> [!IMPORTANT]  
>  利用小於 100 的 FILLFACTOR 來建立叢集索引，會影響資料所佔用的儲存空間數量，因為 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 在建立叢集索引時會轉散發資料。  
  
 如需詳細資訊，請參閱 [指定索引的填滿因素](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)。  
  
 SORT_IN_TEMPDB = {ON |**OFF** }  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定是否要將暫時排序結果儲存在**tempdb**。 預設值為 OFF。  
  
 ON  
 用來建立索引的中繼排序結果會儲存在**tempdb**。 這可能會減少建立索引，如果所需的時間**tempdb**是一組不同的使用者資料庫以外的磁碟上。 不過，這會增加建立索引時所使用的磁碟空間量。  
  
 OFF  
 中繼排序結果會儲存在與用來儲存索引相同的資料庫中。  
  
 除了建立索引，請在使用者資料庫所需的空間**tempdb**還需要大約相同數量的額外空間來容納中繼排序結果。 如需詳細資訊，請參閱[索引的 SORT_IN_TEMPDB 選項](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)。  
  
 在與舊版本相容的語法中，WITH SORT_IN_TEMPDB 相當於 WITH SORT_IN_TEMPDB = ON。  
  
 IGNORE_DUP_KEY = {ON |**OFF** }  
 指定當插入作業嘗試將重複的索引鍵值插入唯一索引時所產生的錯誤回應。 IGNORE_DUP_KEY 選項只適用於在建立或重建索引之後所發生的插入作業。 選項沒有任何作用，執行時[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)， [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)，或[更新](../../t-sql/queries/update-transact-sql.md)。 預設值為 OFF。  
  
 ON  
 當重複的索引鍵值插入唯一索引時，就會出現警告訊息。 只有違反唯一性條件約束的資料列才會失敗。  
  
 OFF  
 當重複的索引鍵值插入唯一索引時，就會出現錯誤訊息。 整個 INSERT 作業將會回復。  
  
 若為針對檢視表所建立的索引、非唯一索引、XML 索引、空間索引和篩選索引，IGNORE_DUP_KEY 不得設為 ON。  
  
 若要檢視 IGNORE_DUP_KEY，請使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。  
  
 在與舊版本相容的語法中，WITH IGNORE_DUP_KEY 相當於 WITH IGNORE_DUP_KEY = ON。  
  
 STATISTICS_NORECOMPUTE = {ON |**OFF**}  
 指定是否要重新計算散發統計資料。 預設值為 OFF。  
  
 ON  
 不會自動重新計算過期的統計資料。  
  
 OFF  
 啟用自動統計資料更新。  
  
 若要還原自動統計資料更新，請將 STATISTICS_NORECOMPUTE 設為 OFF，或執行不含 NORECOMPUTE 子句的 UPDATE STATISTICS。  
  
> [!IMPORTANT]  
>  停用散發統計資料的自動重新計算，可防止查詢最佳化工具取得與資料表有關之查詢的最佳執行計畫。  
  
 在與舊版本相容的語法中，WITH STATISTICS_NORECOMPUTE 相當於 WITH STATISTICS_NORECOMPUTE = ON。  
  
 STATISTICS_INCREMENTAL = {ON |**OFF** }  
 當**ON**，建立的統計資料是以每個分割區統計資料。 當**OFF**，卸除統計資料樹狀結構和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新計算統計資料。 預設值是**OFF**。  
  
 如果不支援每個分割區區的統計資料，則會忽略該選項，並產生警告。 針對下列統計資料類型，不支援累加統計資料：  
  
-   建立統計資料時，所使用的索引未與基底資料表進行分割區對齊。  
-   在 AlwaysOn 可讀取次要資料庫上建立的統計資料。  
-   在唯讀資料庫上建立的統計資料。  
-   在篩選的索引上建立的統計資料。  
-   在檢視上建立的統計資料。  
-   在內部資料表上建立的統計資料。  
-   使用空間索引或 XML 索引建立的統計資料。  
  
 DROP_EXISTING = {ON |**OFF** }  
 是要卸除和重建現有的叢集或非叢集索引，以修改資料行規格，並保留相同名稱的索引選項。 預設值為 OFF。  
  
 ON  
 若要卸除和重建現有索引中，必須具有相同的名稱做為參數指定*index_name*。  
  
 OFF  
 指定不卸除和重建現有的索引。 如果指定的索引名稱已經存在，SQL Server 就會顯示錯誤。  
  
 您可以利用 DROP_EXISTING，變更：  
  
-   叢集資料列存放區索引的非叢集資料列存放區索引。  
  
 With DROP_EXISTING，您無法變更：  
  
-   非叢集資料列存放區索引做為叢集資料列存放區索引。  
  
-   任何類型的資料列存放區索引的叢集資料行存放區索引。  
  
 在與舊版本相容的語法中，WITH DROP_EXISTING 相當於 WITH DROP_EXISTING = ON。  
  
 ONLINE = {ON |**OFF** }  
 指定在索引作業期間，查詢和資料修改是否能夠使用基礎資料表和相關聯的索引。 預設值為 OFF。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的所有版本都無法使用線上索引作業。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2016 版本和支援的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ON  
 索引作業持續期間不會保留長期資料表鎖定。 在索引作業的主要階段期間，來源資料表上只保留意圖共用 (IS) 鎖定。 這可使基礎資料表和索引的查詢或更新能夠進行。 在作業開始時，共用 (S) 鎖定會在來源物件上保留一段很短的時間。 在作業結束時，如果正在建立非叢集索引，則有一段短時間會在來源上取得 S (共用) 鎖定；或者，當以線上方式建立或卸除叢集索引時，以及正在重建叢集索引或非叢集索引時，則會取得 SCH-M (結構描述修改) 鎖定。 建立本機暫存資料表的索引時，ONLINE 不可設為 ON。  
  
 OFF  
 在索引作業期間會套用資料表鎖定。 建立、重建或卸除叢集索引的離線索引作業，或重建或卸除非叢集索引的離線索引作業，會取得資料表的結構描述修改 (Sch-M) 鎖定。 這可防止所有使用者在作業持續期間存取基礎資料表。 建立非叢集索引的離線索引作業會取得資料表的共用 (S) 鎖定。 這可避免對基礎資料表進行更新，但仍可執行讀取作業，如 SELECT 陳述式。  
  
 如需詳細資訊，請參閱[線上索引作業的運作方式](../../relational-databases/indexes/how-online-index-operations-work.md)。  
  
 您可以採用線上方式建立索引，包括全域暫存資料表上的索引，但以下是例外狀況：  
  
-   XML 索引  
-   本機暫存資料表上的索引。  
-   檢視表上的初始唯一叢集索引。  
-   停用的叢集索引。  
-   如果基礎資料表包含 LOB 資料類型的叢集的索引：**映像**， **ntext**，**文字**，以及空間類型。  
-   **varchar （max)**和**varbinary （max)**資料行不能是索引的一部分。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開頭為[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ) 然後在[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]，當資料表包含**varchar （max)**或**varbinary （max)**可以有資料行，包含其他資料行的叢集索引建立或重新使用**線上**選項。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]不允許**線上**選項時，基底資料表包含**varchar （max)**或**varbinary （max)**資料行。  
  
 如需詳細資訊，請參閱 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)。  
  
 ALLOW_ROW_LOCKS = { **ON** |OFF}  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定是否允許資料列鎖定。 預設值是 ON。  
  
 ON  
 當存取索引時，允許資料列鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會決定使用資料列鎖定的時機。  
  
 OFF  
 不使用資料列鎖定。  
  
 ALLOW_PAGE_LOCKS = { **ON** |OFF}  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定是否允許頁面鎖定。 預設值是 ON。  
  
 ON  
 當存取索引時，允許頁面鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會決定使用頁面鎖定的時機。  
  
 OFF  
 不使用頁面鎖定。  
  
 MAXDOP = *max_degree_of_parallelism*  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 覆寫**的最大平行處理原則程度**索引作業期間的組態選項。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 請利用 MAXDOP 來限制執行平行計畫所用的處理器數目。 最大值是 64 個處理器。  
  
 *max_degree_of_parallelism*可以是：  
  
 1  
 隱藏平行計畫的產生。  
  
 \>1  
 根據目前的系統工作負載，將平行索引作業所使用的處理器數目上限，限制為所指定的數目或更少的數目。  
  
 0 (預設值)  
 根據目前的系統工作負載，使用實際數目或比實際數目更少的處理器。  
  
 如需詳細資訊，請參閱 [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
> [!NOTE]  
>  並非每個版本都可使用平行索引作業[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2016 版本和支援的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 DATA_COMPRESSION  
 針對指定的索引、分割區編號或分割區範圍指定資料壓縮選項。 選項如下：  
  
 無  
 不壓縮索引或指定的分割區。  
  
 ROW  
 使用資料列壓縮來壓縮索引或指定的分割區。  
  
 PAGE  
 使用頁面壓縮來壓縮索引或指定的分割區。  
  
 如需有關壓縮的詳細資訊，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
 在資料分割上**(** {\<編號運算式 > |\<範圍 >}[ **,**... *n*  ] **)** **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定套用 DATA_COMPRESSION 設定的分割區。 如果未分割此索引，ON PARTITIONS 引數將會產生錯誤。 如果未提供 ON PARTITIONS 子句，DATA_COMPRESSION 選項會套用到分割區索引的所有分割區。  
  
 \<編號運算式 > 可以下列方式指定：  
  
-   提供分割區的編號，例如：ON PARTITIONS (2)。  
  
-   為數個個別分割區提供以逗號分隔的分割區編號，例如：ON PARTITIONS (1, 5)。  
  
-   同時提供範圍和個別分割區，例如：ON PARTITIONS (2, 4, 6 TO 8)。  
  
 \<範圍 > 可以指定為資料分割數分隔的例如： ON PARTITIONS (6 TO 8)。  
  
 若要為不同的分割區設定不同類型的資料壓縮，請指定 DATA_COMPRESSION 選項一次以上，例如：  
  
```  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
);  
```  
  
## <a name="remarks"></a>備註  
 CREATE INDEX 陳述式的最佳化方式與其他任何查詢一樣。 若要儲存在 I/O 作業上，查詢處理器可以選擇掃描另一個索引，而不是執行資料表掃描。 在某些情況下，排序作業可以省略。 在多處理器電腦上，CREATE INDEX 可以利用更多的處理器來執行與建立索引相關聯的掃描和排序作業，執行方式與其他查詢的執行方式相同。 如需詳細資訊，請參閱 [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
 如果資料庫復原模式設為大量記錄或簡單模式，建立索引作業就可以利用最低限度記錄。  
  
 索引可以在暫存資料表上建立。 當資料表卸除或工作階段結束時，就會卸除索引。  
  
 索引支援擴充屬性。  
  
## <a name="clustered-indexes"></a>叢集索引  
 若要在資料表 (堆積) 上建立叢集索引，或要卸除及重新建立現有的叢集索引，則資料庫中必須有可用的其他工作空間，才能容納資料排序和原始資料表或現有叢集索引資料的暫存複本。 如需叢集索引的詳細資訊，請參閱[建立叢集索引](../../relational-databases/indexes/create-clustered-indexes.md)。  
  
## <a name="nonclustered-indexes"></a>非叢集索引  
 開頭為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，您可以儲存成叢集資料行存放區索引的資料表上建立非叢集索引。 如果您第一次建立非叢集索引儲存的資料表為堆積或叢集的索引，索引會持續保留，如果您稍後將資料表轉換成叢集資料行存放區索引。 它也是不必要卸除叢集索引時重建叢集資料行存放區索引。  
  
 限制事項：  
  
-   FILESTREAM_ON 選項無效，當您儲存成叢集資料行存放區索引的資料表上建立非叢集索引。  
  
## <a name="unique-indexes"></a>唯一索引  
 如果唯一索引存在，每當插入作業新增資料時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 都會確認是否有重複的值。 可能產生重複索引鍵值的插入作業會回復，且 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會顯示錯誤訊息。 即使插入作業變更多個資料列但只造成一個重複的值，一樣會發生這種情況。 如果嘗試輸入資料，而該資料有唯一索引，且該資料的 IGNORE_DUP_KEY 子句設為 ON，則只有違反 UNIQUE 索引規則的資料列會失敗。  
  
## <a name="partitioned-indexes"></a>分割區索引  
 分割區索引與分割區資料表的建立和維護方式類似，不過，跟一般索引一樣，分割區索引會當做個別資料庫物件來處理。 未進行分割的資料表上可以有分割區索引；已進行分割的資料表上也可以有非分割區索引。  
  
 如果您要在分割區資料表上建立索引，且不指定要從中放置索引的檔案群組，則索引的分割區方式與基礎資料表相同。 這是因為索引及其基礎資料表預設會置於同一個檔案群組內，且索引會供相同分割區配置中，使用相同分割區資料行的分割區資料表使用。 當索引使用相同分割區配置及分割資料行的資料表時，則索引是*對齊*與資料表。  
  
> [!WARNING]  
>  您可以對包含超過 1,000 個分割區的資料表，建立及重建不以資料表為準的索引，但不予支援。 此做法可能會導致在作業期間效能降低或耗用過多記憶體。 建議當分割區數超過 1,000 時，一律使用以資料表為準的索引。  
  
 分割區不是唯一的叢集索引時若未指定分割區資料行，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 預設會將其加入叢集索引鍵清單。  
  
 您可以對分割區資料表建立索引檢視表，其方法與建立資料表索引相同。 如需有關分割區索引的詳細資訊，請參閱＜ [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)＞。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 並不會在建立或重建分割區索引之後掃描資料表中所有的資料列建立統計資料。 反之，查詢最佳化工具會使用預設的採樣演算法來產生統計資料。 如果要在掃描資料表中所有資料列時取得分割區索引的統計資料，請使用 CREATE STATISTICS 或 UPDATE STATISTICS 搭配 FULLSCAN 子句。  
  
## <a name="filtered-indexes"></a>篩選的索引  
 已篩選的索引是最佳化的非叢集索引，適用於從資料表選取小型資料列百分比的查詢使用。 它會使用篩選述詞，針對資料表中的部分資料建立索引。 設計良好的已篩選索引可以提升查詢效能、降低儲存成本，並減少維護成本。  
  
### <a name="required-set-options-for-filtered-indexes"></a>需要已篩選之索引的 SET 選項  
 每當發生下列任何一個狀況時，都需要必要值資料行中的 SET 選項：  
  
-   建立已篩選的索引。  
  
-   INSERT、UPDATE、DELETE 或 MERGE 作業修改已篩選之索引中的資料。  
  
-   篩選的索引用於查詢最佳化工具產生查詢計劃。  
  
    |Set 選項|必要值|預設伺服器值|預設值<br /><br /> OLE DB 與 ODBC 值|預設值<br /><br /> DB-Library 值|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|   
  
     *當資料庫的相容性層級設定為 90 或更高層級時，將 ANSI_WARNINGS 設定為 ON 也會將 ARITHABORT 隱含設定為 ON。 如果資料庫的相容性層級設定為 80 或更低，ARITHABORT 選項就必須明確地設定為 ON。  
  
 當 SET 選項不正確時，可能會發生下列狀況：  
  
-   不會建立已篩選的索引。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會產生錯誤，並回復可變更索引中資料的 INSERT、UPDATE、DELETE 或 MERGE 陳述式。  
  
-   查詢最佳化工具不會針對任何 Transact-SQL 陳述式考量執行計畫中的索引。  
  
 如需篩選索引的詳細資訊，請參閱[Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)。  
  
## <a name="spatial-indexes"></a>空間索引  
 空間索引的相關資訊，請參閱[CREATE SPATIAL INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)和[空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)。  
  
## <a name="xml-indexes"></a>XML 索引  
 如需有關 XML 索引，請參閱[CREATE XML INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)和[XML 索引 &#40;SQL Server &#41;](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
## <a name="index-key-size"></a>索引鍵大小  
 叢集索引為 900 個位元組，而非叢集索引為 1,700 個位元組的索引鍵的大小上限。 (之前[!INCLUDE[ssSDS](../../includes/sssds-md.md)]V12 和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]限制永遠都是 900 個位元組。)上的索引**varchar**可以建立超過位元組限制的資料行，如果資料行中的現有資料不能超過限制時，索引會建立; 不過，後續的插入或更新動作所造成的資料行總計大小大於此限制將會失敗。 叢集索引的索引鍵所包含的 **varchar** 資料行不能在 ROW_OVERFLOW_DATA 配置單位中有現有的資料。 如果在 **varchar** 資料行上建立叢集索引，且現有的資料在 IN_ROW_DATA 配置單位中，則後續在可能發送資料非資料列的資料行上進行的插入或更新動作會失敗。  
  
 非叢集索引可將非索引鍵資料行併入索引的分葉層級中。 這些資料行不會考慮[!INCLUDE[ssDE](../../includes/ssde-md.md)]時計算索引鍵大小。 如需詳細資訊，請參閱 [建立內含資料行的索引](../../relational-databases/indexes/create-indexes-with-included-columns.md)。  
  
> [!NOTE]  
>  分割資料表時，如果分割區索引鍵資料行原本不存在非唯一的叢集索引中，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 就會將它們加入至索引。 在非唯一的叢集索引中，索引資料行 (不計算包含的資料行) 再加上任何加入之分割區資料行的組合大小不得超過 1800 個位元組。  
  
## <a name="computed-columns"></a>計算資料行  
 索引可以在計算資料行上建立。 此外，計算資料行可以有 PERSISTED 屬性。 這表示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將計算值儲存在資料表中，並在更新計算資料行所根據的任何其他資料行時更新這些計算值。 當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 在資料行上建立某索引，且查詢中參考該索引時，它會使用這些保存值。  
  
 若要為計算資料行建立索引，則計算資料行必須具決定性且精確。 不過，您可以利用 PERSISTED 屬性，擴充可建立索引的計算資料行類型，使其包括：  
  
-   根據 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 CLR 函數及使用者標示為具決定性的 CLR 使用者定義型別方法所產生的計算資料行。  
  
-   根據具決定性 (如 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 所定義) 但不精確的運算式所產生的計算資料行。  
  
 保存的計算資料行需要設定前一節＜需要索引檢視表的 SET 選項＞中所示的下列 SET 選項。  
  
 UNIQUE 或 PRIMARY KEY 條件約束只要符合索引作業的所有條件就可以包含計算資料行。 更具體的說法是，計算資料行必須具決定性且精確，或是具決定性且一直保存。 如需決定性的詳細資訊，請參閱[決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
 計算資料行，衍生自**映像**， **ntext**，**文字**， **varchar （max)**， **nvarchar （max)**，**varbinary （max)**，和**xml**資料類型可以建立索引做為索引鍵或內含非索引鍵資料行，只要計算資料行資料類型時，才允許做為索引鍵資料行或非索引鍵資料行。 例如，您無法建立主要 XML 索引上計算**xml**資料行。 如果索引鍵大小超過 900 個位元組，畫面上會顯示警告訊息。  
  
 在計算資料行上建立索引，可能會使先前有效的插入或更新作業失敗。 當計算資料行導致算術錯誤時，就可能發生這類失敗。 例如在下表中，雖然計算資料行 `c` 導致算術錯誤，但 `INSERT` 陳述式仍可運作。  
  
```  
CREATE TABLE t1 (a int, b int, c AS a/b);  
INSERT INTO t1 VALUES (1, 0);  
```  
  
 但是，如果在建立資料表之後，您在計算資料行 `c` 上建立索引，相同的 `INSERT` 陳述式在這種情況下則會失敗。  
  
```  
CREATE TABLE t1 (a int, b int, c AS a/b);  
CREATE UNIQUE CLUSTERED INDEX Idx1 ON t1(c);  
INSERT INTO t1 VALUES (1, 0);  
```  
  
 如需詳細資訊，請參閱 [計算資料行的索引](../../relational-databases/indexes/indexes-on-computed-columns.md)。  
  
## <a name="included-columns-in-indexes"></a>將資料行併入索引中  
 您可以將非索引鍵資料行 (稱為內含資料行) 加入至非叢集索引的分葉層級，以處理查詢來提升查詢效能。 換句話說，查詢中參考的所有資料行都會併入索引中當做索引鍵資料行或非索引鍵資料行。 這可讓查詢最佳化工具從索引掃描中尋找所有的必要資訊；但不存取資料表或叢集索引。 如需詳細資訊，請參閱 [建立內含資料行的索引](../../relational-databases/indexes/create-indexes-with-included-columns.md)。  
  
## <a name="specifying-index-options"></a>指定索引選項  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 導入新的索引選項，並修改選項的指定方式。 在回溯相容語法中，WITH *option_name*相當於 WITH **(** \<option_name >  **=**  ON **)**. 當您設定索引選項時，適用下列規則： 
  
-   新的索引選項只能指定使用 WITH **(***option_name*  **=**  ON |關閉**)**。  
  
-   不能在相同的陳述式中同時利用與舊版本相容的語法和新語法來指定選項。 例如，指定 WITH **(**DROP_EXISTING**，**線上 **=**  ON**)**會導致陳述式失敗。  
  
-   當您建立 XML 索引時，必須使用與指定的選項**(***option_name*  **=**  ON |關閉**)**。  
  
## <a name="dropexisting-clause"></a>DROP_EXISTING 子句  
 您可以利用 DROP_EXISTING 子句來重建索引、加入或卸除資料行、修改選項、修改資料行排序次序，或變更分割區配置或檔案群組。  
  
 如果索引強制執行 PRIMARY KEY 或 UNIQUE 條件約束，且索引定義完全沒有變更，則會卸除索引並重新建立索引以保留現有的條件約束。 不過，如果索引定義變更了，陳述式就會失敗。 若要變更 PRIMARY KEY 或 UNIQUE 條件約束的定義，請卸除該條件約束，然後利用新的定義來新增條件約束。  
  
 當您在一份也有非叢集索引的資料表上利用一組相同或不同的索引鍵來重新建立叢集索引時，DROP_EXISTING 可以增強效能。 DROP_EXISTING 會取代舊叢集索引上之 DROP INDEX 陳述式的執行，然後再針對新叢集索引執行 CREATE INDEX 陳述式。 非叢集索引只重建一次，之後，只有在索引定義變更時才會再重建。 當索引定義的索引名稱、索引鍵資料行和分割區資料行、唯一性屬性及排序次序與原始索引相同時，DROP_EXISTING 子句不會重建非叢集索引。  
  
 不論非叢集索引是否重建，它們一律會保留在它們的原始檔案群組或分割區配置中，且會使用原始的分割區函數。 如果將叢集索引重建至不同的檔案群組或分割區配置中，則不會移動非叢集索引來符合叢集索引的新位置。 因此，即使非叢集索引先前與叢集索引對齊，它們也可能不再與叢集索引對齊。 如需有關分割區索引對齊的詳細資訊，請參閱。  
  
 除非索引陳述式指定非叢集索引且 ONLINE 選項設為 OFF，否則，如果您以相同的順序使用相同的索引鍵資料行，且相同的索引鍵資料行含有相同的遞增或遞減順序，則 DROP_EXISTING 子句不會再次排序資料。 如果叢集索引已停用，則執行 CREATE INDEX WITH DROP_EXISTING 作業時必須將 ONLINE 設為 OFF。 如果非叢集索引已停用，且與停用的叢集索引無關，則執行 CREATE INDEX WITH DROP_EXISTING 作業時可以將 ONLINE 設為 OFF，也可以將它設為 ON。  
  
 當卸除或重新建立含有 128 個 (含) 以上之範圍的索引時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會延遲實際的頁面取消配置及其相關聯的鎖定，直到認可交易之後。  
  
## <a name="online-option"></a>ONLINE 選項  
 以線上方式執行索引作業時，適用下列方針：  
  
-   當線上索引作業進行中時，不能變更、截斷或卸除基礎資料表。  
  
-   在索引作業進行期間，需要其他暫存磁碟空間。  
  
-   線上作業可在下列索引上執行：分割區索引，以及包含保存的計算資料行或內含資料行的索引。  
  
 如需詳細資訊，請參閱 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)。  
  
## <a name="row-and-page-locks-options"></a>資料列和頁面鎖定選項  
 如果 ALLOW_ROW_LOCKS = ON 且 ALLOW_PAGE_LOCK = ON，當您在存取索引時，允許使用資料列、頁面和資料表層級的鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會選擇適當的鎖定，且可以將鎖定從資料列或頁面鎖定擴大到資料表鎖定。  
  
 如果 ALLOW_ROW_LOCKS = OFF 且 ALLOW_PAGE_LOCK = OFF，當您存取索引時，只允許使用資料表層級的鎖定。  
  
## <a name="viewing-index-information"></a>檢視索引資訊  
 若要傳回有關索引的資訊，您可以使用目錄檢視、系統函數和系統預存程序。  
  
## <a name="data-compression"></a>資料壓縮  
 主題會說明資料壓縮[資料壓縮](../../relational-databases/data-compression/data-compression.md)。 以下是考量的幾個要點：  
  
-   壓縮可讓更多的資料列儲存在頁面上，但是不會變更最大資料列大小。  
  
-   索引的非分葉頁面不會進行頁面壓縮，但是可以進行資料列壓縮。  
  
-   每一個非叢集索引都有個別的壓縮設定，而且不會繼承基礎資料表的壓縮設定。  
  
-   在堆積上建立叢集索引時，此叢集索引會繼承堆積的壓縮狀態，除非指定了替代的壓縮狀態。  
  
 下列限制適用於分割區索引：  
  
-   您無法在資料表具有非對齊索引時變更單一分割區的壓縮設定。  
  
-   ALTER INDEX\<索引 >...REBUILD PARTITION ... 語法會重建此索引的指定資料分割。  
  
-   ALTER INDEX\<索引 >...REBUILD WITH ... 語法會重建此索引的所有資料分割。  
  
 若要評估變更壓縮狀態如何影響資料表、索引或分割區，請使用 [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) 預存程序。  
  
## <a name="permissions"></a>Permissions  
 需要資料表或檢視表的 ALTER 權限。 使用者必須是 **系統管理員** 固定伺服器角色的成員，或是 **db_ddladmin** 和 **db_owner** 固定資料庫角色的成員。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，您無法建立：  
  
-   資料倉儲資料表已存在的資料行存放區索引上的叢集或非叢集資料列存放區索引。 此行為是不同於 SMP SQL Server 可讓要共存於相同的資料表上的資料列存放區和資料行存放區索引。  
  
-   您無法在檢視上建立索引。  
  
## <a name="metadata"></a>中繼資料  
 若要檢視現有索引上的資訊，您可以查詢[sys.indexes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目錄檢視。  
  
## <a name="version-notes"></a>版本資訊  
 SQL Database 不支援的檔案群組和 filestream 選項。  
  
## <a name="examples-all-versions-uses-the-adventureworks-database"></a>範例： 所有版本。 使用的 AdventureWorks 資料庫。  
  
### <a name="a-create-a-simple-nonclustered-rowstore-index"></a>A. 建立簡單的非叢集資料列存放區索引  
 下列範例會建立非叢集索引上`VendorID`資料行`Purchasing.ProductVendor`資料表。  
  
```  
CREATE INDEX IX_VendorID ON ProductVendor (VendorID);  
CREATE INDEX IX_VendorID ON dbo.ProductVendor (VendorID DESC, Name ASC, Address DESC);  
CREATE INDEX IX_VendorID ON Purchasing..ProductVendor (VendorID);  
```  
  
### <a name="b-create-a-simple-nonclustered-rowstore-composite-index"></a>B. 建立簡單的非叢集資料列存放區的複合索引  
 下列範例會建立非叢集複合索引上`SalesQuota`和`SalesYTD`的資料行`Sales.SalesPerson`資料表。  
  
```  
CREATE NONCLUSTERED INDEX IX_SalesPerson_SalesQuota_SalesYTD ON Sales.SalesPerson (SalesQuota, SalesYTD);  
```  
  
### <a name="c-create-an-index-on-a-table-in-another-database"></a>C. 另一個資料庫中的資料表上建立索引  
 下列範例會建立非叢集索引上`VendorID`資料行`ProductVendor`資料表中`Purchasing`資料庫。  
  
```  
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID ON Purchasing..ProductVendor (VendorID);   
```  
  
### <a name="d-add-a-column-to-an-index"></a>D. 資料行加入索引  
 下列範例會建立索引 IX_FF 含有 dbo 的兩個資料行。FactFinance 資料表。  下一個陳述式會重建多個資料行索引，並保留現有的名稱。  
  
```  
CREATE INDEX IX_FF ON dbo.FactFinance ( FinanceKey ASC, DateKey ASC );  
  
--Rebuild and add the OrganizationKey  
CREATE INDEX IX_FF ON dbo.FactFinance ( FinanceKey, DateKey, OrganizationKey DESC)  
WITH ( DROP_EXISTING = ON );  
 ```  
  
## <a name="examples-sql-server-azure-sql-database"></a>範例： SQL Server 的 Azure SQL Database  
  
### <a name="e-create-a-unique-nonclustered-index"></a>E. 建立唯一的非叢集索引  
 下列範例會在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中 `Name` 資料表的 `Production.UnitMeasure` 資料行上建立唯一非叢集索引。 索引會強制將資料上的唯一性插入 `Name` 資料行中。  
  
```  
CREATE UNIQUE INDEX AK_UnitMeasure_Name   
    ON Production.UnitMeasure(Name);  
```  
  
 下列查詢會藉由嘗試插入與現有資料列具有相同值的資料列，以測試條件約束的唯一性。  
  
```  
--Verify the existing value.  
SELECT Name FROM Production.UnitMeasure WHERE Name = N'Ounces';  
GO  
INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name, ModifiedDate)  
    VALUES ('OC', 'Ounces', GetDate());  
```  
  
 產生的錯誤訊息如下：  
  
```  
Server: Msg 2601, Level 14, State 1, Line 1  
Cannot insert duplicate key row in object 'UnitMeasure' with unique index 'AK_UnitMeasure_Name'. The statement has been terminated.  
```  
  
### <a name="f-use-the-ignoredupkey-option"></a>F. 使用 IGNORE_DUP_KEY 選項  
 下列範例分別利用兩種不同的選項設定 (先將選項設為 `IGNORE_DUP_KEY`，再將選項設為 `ON`) 將多個資料列插入暫存資料表中，示範 `OFF` 選項的效果。 單一資料列會插入 `#Test` 資料表中，該資料表則會在第二個多重資料列 `INSERT` 陳述式執行時刻意造成重複的值。 資料表中的資料列計數會傳回所插入的資料列數目。  
  
```  
CREATE TABLE #Test (C1 nvarchar(10), C2 nvarchar(50), C3 datetime);  
GO  
CREATE UNIQUE INDEX AK_Index ON #Test (C2)  
    WITH (IGNORE_DUP_KEY = ON);  
GO  
INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());  
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;  
GO  
SELECT COUNT(*)AS [Number of rows] FROM #Test;  
GO  
DROP TABLE #Test;  
GO  
```  
  
 以下是第二個 `INSERT` 陳述式的結果。  
  
```  
Server: Msg 3604, Level 16, State 1, Line 5 Duplicate key was ignored.  
  
Number of rows   
--------------   
38  
```  
  
 請注意，從 `Production.UnitMeasure` 資料表插入之未違反唯一性條件約束的資料列已順利插入。 發出警告且忽略重複的資料列，但不回復整個交易。  
  
 重新執行相同的陳述式，但將 `IGNORE_DUP_KEY` 設為 `OFF`。  
  
```  
CREATE TABLE #Test (C1 nvarchar(10), C2 nvarchar(50), C3 datetime);  
GO  
CREATE UNIQUE INDEX AK_Index ON #Test (C2)  
    WITH (IGNORE_DUP_KEY = OFF);  
GO  
INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());  
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;  
GO  
SELECT COUNT(*)AS [Number of rows] FROM #Test;  
GO  
DROP TABLE #Test;  
GO  
```  
  
 以下是第二個 `INSERT` 陳述式的結果。  
  
```  
Server: Msg 2601, Level 14, State 1, Line 5  
Cannot insert duplicate key row in object '#Test' with unique index  
'AK_Index'. The statement has been terminated.  
  
Number of rows   
--------------   
1  
```  
  
 請注意，即便 `Production.UnitMeasure` 資料表只有一個資料列違反 `UNIQUE` 索引條件約束，皆會導致資料表中所有的資料列無法插入資料表。  
  
### <a name="g-using-dropexisting-to-drop-and-re-create-an-index"></a>G. 使用 DROP_EXISTING 卸除及重新建立索引  
 下列範例會利用 `ProductID` 選項，在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中 `Production.WorkOrder` 資料表的 `DROP_EXISTING` 資料行上卸除及重新建立現有的索引。 也會設定 `FILLFACTOR` 和 `PAD_INDEX` 選項。  
  
```  
CREATE NONCLUSTERED INDEX IX_WorkOrder_ProductID  
    ON Production.WorkOrder(ProductID)  
    WITH (FILLFACTOR = 80,  
        PAD_INDEX = ON,  
        DROP_EXISTING = ON);  
GO  
  
```  
  
### <a name="h-create-an-index-on-a-view"></a>H. 在檢視上建立索引  
 下列範例會在該檢視表上建立檢視表和索引。 內含使用索引檢視的兩項查詢。  
  
```  
--Set the options to support indexed views.  
SET NUMERIC_ROUNDABORT OFF;  
SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,  
    QUOTED_IDENTIFIER, ANSI_NULLS ON;  
GO  
--Create view with schemabinding.  
IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL  
DROP VIEW Sales.vOrders ;  
GO  
CREATE VIEW Sales.vOrders  
WITH SCHEMABINDING  
AS  
    SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Revenue,  
        OrderDate, ProductID, COUNT_BIG(*) AS COUNT  
    FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o  
    WHERE od.SalesOrderID = o.SalesOrderID  
    GROUP BY OrderDate, ProductID;  
GO  
--Create an index on the view.  
CREATE UNIQUE CLUSTERED INDEX IDX_V1   
    ON Sales.vOrders (OrderDate, ProductID);  
GO  
--This query can use the indexed view even though the view is   
--not specified in the FROM clause.  
SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev,   
    OrderDate, ProductID  
FROM Sales.SalesOrderDetail AS od  
    JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
        AND ProductID BETWEEN 700 and 800  
        AND OrderDate >= CONVERT(datetime,'05/01/2002',101)  
GROUP BY OrderDate, ProductID  
ORDER BY Rev DESC;  
GO  
--This query can use the above indexed view.  
SELECT  OrderDate, SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev  
FROM Sales.SalesOrderDetail AS od  
    JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
        AND DATEPART(mm,OrderDate)= 3  
        AND DATEPART(yy,OrderDate) = 2002  
GROUP BY OrderDate  
ORDER BY OrderDate ASC;  
GO  
  
```  
  
### <a name="i-create-an-index-with-included-non-key-columns"></a>I. 建立內含 （非索引鍵） 資料行索引  
 下列範例會利用一個索引鍵資料行 (`PostalCode`) 和四個非索引鍵資料行 (`AddressLine1`、`AddressLine2`、`City`、`StateProvinceID`) 來建立非叢集索引。 其後有一個由索引處理的查詢。 若要顯示所選取的查詢最佳化工具在索引**查詢**功能表[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，選取**顯示實際執行計畫**之前執行查詢。  
  
```  
CREATE NONCLUSTERED INDEX IX_Address_PostalCode  
    ON Person.Address (PostalCode)  
    INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
GO  
SELECT AddressLine1, AddressLine2, City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE PostalCode BETWEEN N'98000' and N'99999';  
GO  
```  
  
### <a name="j-create-a-partitioned-index"></a>J. 建立資料分割的索引  
 下列範例會在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中現有的分割區配置 `TransactionsPS1` 上建立非叢集分割區索引。 此範例假設您已安裝分割區索引範例。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```  
CREATE NONCLUSTERED INDEX IX_TransactionHistory_ReferenceOrderID  
    ON Production.TransactionHistory (ReferenceOrderID)  
    ON TransactionsPS1 (TransactionDate);  
GO  
```  
  
### <a name="k-creating-a-filtered-index"></a>K. 建立篩選的索引  
 下列範例會對 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中的 Production.BillOfMaterials 資料表建立篩選的索引。 篩選述詞可以包含在已篩選之索引中不是索引鍵資料行的資料行。 此範例中的述詞只會選取 EndDate 不是 NULL 的資料列。  
  
```  
CREATE NONCLUSTERED INDEX "FIBillOfMaterialsWithEndDate"  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL;  
```  
  
### <a name="l-create-a-compressed-index"></a>L. 建立壓縮的索引  
 下列範例會使用資料列壓縮，在非分割區資料表上建立索引。  
  
```  
CREATE NONCLUSTERED INDEX IX_INDEX_1   
    ON T1 (C2)  
WITH ( DATA_COMPRESSION = ROW ) ;   
GO  
```  
  
 下列範例會在索引的所有分割區上使用資料列壓縮，以便在分割區資料表上建立索引。  
  
```  
CREATE CLUSTERED INDEX IX_PartTab2Col1  
ON PartitionTable1 (Col1)  
WITH ( DATA_COMPRESSION = ROW ) ;  
GO  
```  
  
 下列範例會在分割區資料表上建立索引，其方式是在索引的分割區 `1` 上使用頁面壓縮，並在索引的分割區 `2` 到 `4` 上使用資料列壓縮。  
  
```  
CREATE CLUSTERED INDEX IX_PartTab2Col1  
ON PartitionTable1 (Col1)  
WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(1),  
    DATA_COMPRESSION = ROW ON PARTITIONS (2 TO 4 ) ) ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="m-basic-syntax"></a>M. 基本語法  
  
```  
CREATE INDEX IX_VendorID   
    ON ProductVendor (VendorID);  
CREATE INDEX IX_VendorID   
    ON dbo.ProductVendor (VendorID DESC, Name ASC, Address DESC);  
CREATE INDEX IX_VendorID   
    ON Purchasing..ProductVendor (VendorID);  
```  
  
### <a name="n-create-a-non-clustered-index-on-a-table-in-the-current-database"></a>N. 目前資料庫中的資料表上建立非叢集索引  
 下列範例會建立非叢集索引上`VendorID`資料行`ProductVendor`資料表。  
  
```  
CREATE INDEX IX_ProductVendor_VendorID   
    ON ProductVendor (VendorID);   
```  
  
### <a name="o-create-a-clustered-index-on-a-table-in-another-database"></a>O. 在另一個資料庫中的資料表上建立叢集的索引  
 下列範例會建立非叢集索引上`VendorID`資料行`ProductVendor`資料表中`Purchasing`資料庫。  
  
```  
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID   
    ON Purchasing..ProductVendor (VendorID);   
```  
  
## <a name="see-also"></a>請參閱  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [建立空間索引 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [建立 XML 索引 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [XML 索引 &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
 

