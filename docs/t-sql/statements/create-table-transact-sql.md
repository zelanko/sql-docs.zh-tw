---
title: "建立資料表 (TRANSACT-SQL) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILESTREAM_TSQL
- TABLE
- CREATE_TABLE_TSQL
- CREATE TABLE
- FILESTREAM
- TABLE_TSQL
- FILESTREAM_ON
- FILESTREAM_ON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHECK constraints
- global temporary tables [SQL Server]
- local temporary tables [SQL Server]
- size [SQL Server], tables
- UNIQUE constraints [SQL Server], creating
- constraints [SQL Server], columns
- maximum number of indexes per table
- number of tables per database
- number of indexes per table
- table creation [SQL Server], CREATE TABLE
- temporary tables [SQL Server], creating
- table size [SQL Server]
- nullability [SQL Server]
- partitioned tables [SQL Server], creating
- DEFAULT definition
- null values [SQL Server], columns
- number of rows per table
- maximum number of columns per table
- FOREIGN KEY constraints, creating
- PRIMARY KEY constraints
- number of bytes per row
- CREATE TABLE statement
- number of columns per table
- maximum number of bytes per row
ms.assetid: 1e068443-b9ea-486a-804f-ce7b6e048e8b
caps.latest.revision: 256
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0978041b1c2683f6af3f6c531ddc10edc6b9bcbf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-transact-sql"></a>CREATE TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  建立新的資料表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
> [!NOTE]   
>  如[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]語法，請參閱[CREATE TABLE （Azure SQL 資料倉儲）](../../t-sql/statements/create-table-azure-sql-data-warehouse.md)。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
--Simple CREATE TABLE Syntax (common if not using options)  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    ( { <column_definition> } [ ,...n ] )   
[ ; ]  
```  
  
## <a name="syntax"></a>語法  
  
```  
--Disk-Based CREATE TABLE Syntax  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    [ AS FileTable ]  
    ( {   <column_definition>   
        | <computed_column_definition>    
        | <column_set_definition>   
        | [ <table_constraint> ]   
        | [ <table_index> ] }  
          [ ,...n ]    
          [ PERIOD FOR SYSTEM_TIME ( system_start_time_column_name   
             , system_end_time_column_name ) ]  
      )  
    [ ON { partition_scheme_name ( partition_column_name )   
           | filegroup   
           | "default" } ]   
    [ TEXTIMAGE_ON { filegroup | "default" } ]   
    [ FILESTREAM_ON { partition_scheme_name   
           | filegroup   
           | "default" } ]  
    [ WITH ( <table_option> [ ,...n ] ) ]  
[ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ FILESTREAM ]  
    [ COLLATE collation_name ]   
    [ SPARSE ]  
    [ MASKED WITH ( FUNCTION = ' mask_function ') ]  
    [ CONSTRAINT constraint_name [ DEFAULT constant_expression ] ]   
    [ IDENTITY [ ( seed,increment ) ]  
    [ NOT FOR REPLICATION ]   
    [ GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] ]   
    [ NULL | NOT NULL ]  
    [ ROWGUIDCOL ]  
    [ ENCRYPTED WITH   
        ( COLUMN_ENCRYPTION_KEY = key_name ,  
          ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED } ,   
          ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'  
        ) ]  
    [ <column_constraint> [ ...n ] ]   
    [ <column_index> ]  
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
        [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
[ CONSTRAINT constraint_name ]   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH FILLFACTOR = fillfactor    
          | WITH ( < index_option > [ , ...n ] )   
        ]   
        [ ON { partition_scheme_name ( partition_column_name )   
            | filegroup | "default" } ]  
  
  | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
  
  | CHECK [ NOT FOR REPLICATION ] ( logical_expression )   
}   
  
<column_index> ::=   
 INDEX index_name [ CLUSTERED | NONCLUSTERED ]  
    [ WITH ( <index_option> [ ,... n ] ) ]  
    [ ON { partition_scheme_name (column_name )   
         | filegroup_name  
         | default   
         }  
    ]   
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]  
  
<computed_column_definition> ::=  
column_name AS computed_column_expression   
[ PERSISTED [ NOT NULL ] ]  
[   
    [ CONSTRAINT constraint_name ]  
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [   
            WITH FILLFACTOR = fillfactor   
          | WITH ( <index_option> [ , ...n ] )  
        ]  
        [ ON { partition_scheme_name ( partition_column_name )   
        | filegroup | "default" } ]  
  
    | [ FOREIGN KEY ]   
        REFERENCES referenced_table_name [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE } ]   
        [ ON UPDATE { NO ACTION } ]   
        [ NOT FOR REPLICATION ]   
  
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )   
]   
  
<column_set_definition> ::=  
column_set_name XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
  
< table_constraint > ::=  
[ CONSTRAINT constraint_name ]   
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        (column [ ASC | DESC ] [ ,...n ] )   
        [   
            WITH FILLFACTOR = fillfactor   
           |WITH ( <index_option> [ , ...n ] )   
        ]  
        [ ON { partition_scheme_name (partition_column_name)  
            | filegroup | "default" } ]   
    | FOREIGN KEY   
        ( column [ ,...n ] )   
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
 

  
< table_index > ::=   
{  
    {  
      INDEX index_name [ CLUSTERED | NONCLUSTERED ]   
         (column_name [ ASC | DESC ] [ ,... n ] )   
    | INDEX index_name CLUSTERED COLUMNSTORE  
    | INDEX index_name [ NONCLUSTERED ] COLUMNSTORE (column_name [ ,... n ] )  
    }  
    [ WITH ( <index_option> [ ,... n ] ) ]   
    [ ON { partition_scheme_name (column_name )   
         | filegroup_name  
         | default   
         }  
    ]   
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]  
  
}   


<table_option> ::=  
{  
    [DATA_COMPRESSION = { NONE | ROW | PAGE }  
      [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
      [ , ...n ] ) ]]  
    [ FILETABLE_DIRECTORY = <directory_name> ]   
    [ FILETABLE_COLLATE_FILENAME = { <collation_name> | database_default } ]  
    [ FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME = <constraint_name> ]  
    [ FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME = <constraint_name> ]  
    [ FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME = <constraint_name> ]  
    [ SYSTEM_VERSIONING = ON [ ( HISTORY_TABLE = schema_name . history_table_name  
        [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] ) ] ]  
    [ REMOTE_DATA_ARCHIVE =   
      {   
          ON [ ( <table_stretch_options> [,...n] ) ]  
        | OFF ( MIGRATION_STATE = PAUSED )   
      }   
    ]  
}  
  
<table_stretch_options> ::=  
{  
     [ FILTER_PREDICATE = { null | table_predicate_function } , ]  
       MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED }  
 }  
  
<index_option> ::=  
{   
    PAD_INDEX = { ON | OFF }   
  | FILLFACTOR = fillfactor   
  | IGNORE_DUP_KEY = { ON | OFF }   
  | STATISTICS_NORECOMPUTE = { ON | OFF }   
  | ALLOW_ROW_LOCKS = { ON | OFF}   
  | ALLOW_PAGE_LOCKS ={ ON | OFF}   
  | COMPRESSION_DELAY= {0 | delay [Minutes]}  
  | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
       [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
       [ , ...n ] ) ]  
}  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
```  
  
```  
  
      --Memory optimized CREATE TABLE Syntax  
CREATE TABLE  
    [database_name . [schema_name ] . | schema_name . ] table_name  
    ( { <column_definition>  
    | [ <table_constraint> ] [ ,... n ]  
    | [ <table_index> ]  
      [ ,... n ] }   
      [ PERIOD FOR SYSTEM_TIME ( system_start_time_column_name   
        , system_end_time_column_name ) ]  
)  
    [ WITH ( <table_option> [ ,... n ] ) ]  
 [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]  
    [ GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] ]   
    [ NULL | NOT NULL ]  
[  
    [ CONSTRAINT constraint_name ] DEFAULT memory_optimized_constant_expression ]  
    | [ IDENTITY [ ( 1, 1 ) ]  
]  
    [ <column_constraint> ]  
    [ <column_index> ]  
  
<data type> ::=  
 [type_schema_name . ] type_name [ (precision [ , scale ]) ]  
  
<column_constraint> ::=  
 [ CONSTRAINT constraint_name ]  
{   
  { PRIMARY KEY | UNIQUE }    
      {   NONCLUSTERED   
        | NONCLUSTERED HASH WITH (BUCKET_COUNT = bucket_count)   
      }   
  | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]   
  | CHECK ( logical_expression )   
}  
  
< table_constraint > ::=  
 [ CONSTRAINT constraint_name ]  
{    
   { PRIMARY KEY | UNIQUE }  
     {   
       NONCLUSTERED (column [ ASC | DESC ] [ ,... n ])  
       | NONCLUSTERED HASH (column [ ,... n ] ) WITH ( BUCKET_COUNT = bucket_count )   
                    }   
    | FOREIGN KEY   
        ( column [ ,...n ] )   
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]   
    | CHECK ( logical_expression )   
}  
  
<column_index> ::=  
  INDEX index_name  
{ [ NONCLUSTERED ] | [ NONCLUSTERED ] HASH WITH (BUCKET_COUNT = bucket_count)  }  
  
<table_index> ::=  
  INDEX index_name  
{   [ NONCLUSTERED ] HASH (column [ ,... n ] ) WITH (BUCKET_COUNT = bucket_count)   
  | [ NONCLUSTERED ] (column [ ASC | DESC ] [ ,... n ] )   
      [ ON filegroup_name | default ]  
  | CLUSTERED COLUMNSTORE [WITH ( COMPRESSION_DELAY = {0 | delay [Minutes]})]  
      [ ON filegroup_name | default ]  
  
}  
  
<table_option> ::=  
{  
    MEMORY_OPTIMIZED = ON   
  | DURABILITY = {SCHEMA_ONLY | SCHEMA_AND_DATA}  
  | SYSTEM_VERSIONING = ON [ ( HISTORY_TABLE = schema_name . history_table_name  
        [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] ) ]   
  
}  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 資料表據以建立之資料庫的名稱。 *database_name*必須指定現有資料庫的名稱。 如果未指定， *database_name*預設為目前的資料庫。 目前連接的登入必須與所指定的資料庫中的現有使用者識別碼相關聯*database_name*，而且該使用者識別碼必須具有 CREATE TABLE 權限。  
  
 *schema_name*  
 這是新的資料表所屬的結構描述名稱。  
  
 *table_name*  
 這是新資料表的名稱。 資料表名稱必須遵循的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。 *table_name*最多可有 128 個字元，除了本機暫存資料表名稱 (名稱加上一個數字符號 （#）)，不能超過 116 個字元。  
  
 AS FileTable 
 
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
 
 將新資料表建立為 FileTable。 因為 FileTable 有固定的結構描述，所以您不必指定資料行。 如需有關 Filetable 的詳細資訊，請參閱[FileTables &#40;SQL Server &#41;](../../relational-databases/blob/filetables-sql-server.md).  
  
 *column_name*  
 *computed_column_expression*  
 這是定義計算資料行值的運算式。 計算資料行是一個虛擬資料行，除非資料行標示了 PERSISTED，否則，並未實際儲存在資料表中。 這個資料行是從使用相同資料表之其他資料行的運算式得出的。 例如，計算資料行可以有的定義：**成本**AS**價格** \* **qty**。這個運算式可以是非計算的資料行名稱、常數、函數、變數，以及一個或多個運算子所連接的這些項目的任何組合。 這個運算式不能是子查詢，也不能包含別名資料類型。  
  
 計算資料行可用在選取清單、WHERE 子句、ORDER BY 子句中，或任何能夠使用規則運算式的其他位置中，但下列狀況例外：  
  
-   計算資料行必須標示為 PERSISTED，才能參與 FOREIGN KEY 或 CHECK 條件約束。  
  
-   如果以決定性的運算式定義計算資料行的值，而且索引資料行允許結果的資料類型，則計算資料行可以用來做為索引的索引鍵資料行，或任何 PRIMARY KEY 或 UNIQUE 條件約束的一部分。  
  
     例如，如果資料表有整數資料行和**b**，計算資料行**a + b**可能要編製索引，但是計算資料行**a + DATEPART (dd，GETDATE())**無法進行索引，因為值可能會變更在後續叫用。  
  
-   計算資料行不能是 INSERT 或 UPDATE 陳述式的目標。  
  
> [!NOTE]  
>  對於計算資料行所涉及的資料行，資料表中的每個資料列都可能有不同的值；因此，每個資料列的計算資料行可能各有不同的值。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會依據所用的運算式，來自動判斷計算資料行的 Null 屬性。 大部分運算式的結果都會視為可為 Null，即使只存在不可為 Null 的資料行也是如此，這是因為可能出現的反向溢位或溢位也會產生 NULL 結果。 使用 COLUMNPROPERTY 函數與**AllowsNull**來調查資料表中的任何計算資料行的 null 屬性的屬性。 可為 null 的運算式可以轉換成 null 的一個來指定 ISNULL 與*check_expression*常數，其中常數位於非 null 值用來替代任何 NULL 結果。 以 Common Language Runtime (CLR) 使用者定義型別運算式為基礎的計算資料行，需要類型的 REFERENCES 權限。  
  
 PERSISTED  
 指定 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會實際將計算值儲存在資料表中，以及在計算資料行所依賴的任何其他資料行有了更新時，也會更新這些值。 將計算資料行標示為 PERSISTED，可讓您在具決定性但不精確的計算資料行上建立索引。 如需詳細資訊，請參閱 [計算資料行的索引](../../relational-databases/indexes/indexes-on-computed-columns.md)。 任何用為分割資料表之分割資料行的計算資料行，皆須明確標示為 PERSISTED。 *computed_column_expression*指定 PERSISTED 時，必須是具決定性。  
  
 ON {*一概* | *檔案群組* | **"**預設**"** }  

 指定儲存資料表的分割區配置或檔案群組。 如果*一概*指定時，資料表便是資料分割的資料表的分割區儲存一組的其中一個或多個檔案群組中指定*一概*。 如果*檔案群組*指定時，資料表儲存在具名檔案群組。 檔案群組必須在資料庫內。 如果**"**預設**"**指定，或完全未指定 ON，如果資料表儲存在預設檔案群組。 CREATE TABLE 所指定的資料表儲存機制無法進行後續的改變。  
  
 ON {*一概* | *檔案群組* | **"**預設**"**} 也可以指定主索引鍵或 UNIQUE 條件約束。 這些條件約束會建立索引。 如果*檔案群組*指定，則索引會儲存在具名檔案群組。 如果**"**預設**"**指定，或完全未指定 ON，索引會儲存在資料表的相同檔案群組。 如果 PRIMARY KEY 或 UNIQUE 條件約束建立叢集索引，資料表的資料頁面會儲存在索引的相同檔案群組中。 如果指定了 CLUSTERED，或其他條件約束建立叢集的索引，且*一概*指定不同於*一概*或*的檔案群組*資料表定義，或反之亦然，將會接受條件約束定義，且其他會被忽略。  
  
> [!NOTE]  
>  在此內容中，default 不是關鍵字。 它是預設檔案群組的識別碼，必須加以分隔，如 ON **"**預設**"**或 ON **[**預設**]**。 如果**"**預設**"**指定，將 QUOTED_IDENTIFIER 選項必須是 ON，目前工作階段。 這是預設值。 如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
> [!NOTE]  
>  在您建立分割區資料表之後，請考慮將資料表的 LOCK_ESCALATION 選項設定為 AUTO。 如此一來可以讓鎖定從資料表擴大至分割區 (HoBT) 階層，進而改善並行作業。 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)。  
  
 TEXTIMAGE_ON {*檔案群組*| **"**預設**"** }  
 表示**文字**， **ntext**，**映像**， **xml**， **varchar （max)**， **nvarchar （max)**， **varbinary （max)**，及 CLR 使用者定義型別資料行 （包括 geometry 和 geography） 都會儲存在指定的檔案群組。  
  
 如果資料表中沒有大數值資料行，即不可使用 TEXTIMAGE_ON。 如果無法指定 TEXTIMAGE_ON*一概*指定。 如果**"**預設**"**指定，或完全未指定 TEXTIMAGE_ON，大數值資料行儲存在預設檔案群組。 CREATE TABLE 所指定的任何大數值資料行的儲存體，無法進行後續的改變。  

> [!NOTE]  
> Varchar （max）、 nvarchar （max）、 varbinary （max）、 xml 和大型 UDT 值直接儲存在資料列，最多 8000 個位元組長達此值可容納的記錄。 如果值不適合在記錄中，指標會排序在 LOB 儲存空間中的資料列外儲存同資料列和 rest。 預設值為 0。
TEXTIMAGE_ON 只變更 「 LOB 儲存空間 」 的位置，不會影響資料儲存在資料列時。 使用大型的 value types out of row 選項的 sp_tableoption 儲存整個資料列外的 LOB 值。 


> [!NOTE]  
>  在此內容中，default 不是關鍵字。 它是預設檔案群組的識別碼，必須加以分隔，如 TEXTIMAGE_ON **"**預設**"**或 TEXTIMAGE_ON **[**預設**]**. 如果**"**預設**"**指定，將 QUOTED_IDENTIFIER 選項必須是 ON，目前工作階段。 這是預設值。 如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
 FILESTREAM_ON { *partition_scheme_name* | 檔案群組 |**"**預設**"** }**適用於**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 
 
 為 FILESTREAM 資料指定檔案群組。  
  
 如果此資料表包含 FILESTREAM 資料，而且資料表已分割，則必須包含 FILESTREAM_ON 子句，而且必須指定 FILESTREAM 檔案群組的分割區配置。 這個分割區配置必須與資料表的分割區配置使用相同的分割區函數和分割區資料行。否則，就會引發錯誤。  
  
 如果此資料表未分割，FILESTREAM 資料行將無法分割。 此資料表的 FILESTREAM 資料必須儲存在單一檔案群組內。 這個檔案群組是在 FILESTREAM_ON 子句中指定。  
  
 如果此資料表未分割，而且沒有指定 FILESTREAM_ON 子句，就會使用具有 DEFAULT 屬性集的 FILESTREAM 檔案群組。 如果沒有任何 FILESTREAM 檔案群組，就會引發錯誤。  
  
-   如同 ON 和 TEXTIMAGE_ON，使用 FILESTREAM_ON 的 CREATE TABLE 所設定的值無法變更，但下列情況除外：  
  
-   A [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)陳述式將堆積轉換成叢集索引。 在此情況中，您就可以指定不同的 FILESTREAM 檔案群組、分割區配置或 NULL。  
  
-   A [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)陳述式將非叢集的索引轉換為堆積。 在此情況下，不同的 FILESTREAM 檔案群組、 分割區配置或**"**預設**"**可以指定。  
  
 中的檔案群組`FILESTREAM_ON <filegroup>`子句或在分割區配置中，名為每個 FILESTREAM 檔案群組必須有一個檔案群組定義的檔案。 這個檔案必須定義使用[CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md)或[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)陳述式; 否則就會引發錯誤。  
  
 如需相關的 FILESTREAM 主題，請參閱[二進位大型物件 &#40;Blob &#41;資料 &#40;SQL Server &#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 [ *type_schema_name***。** ] *type_name*  
 指定資料行的資料類型及其所屬的結構描述。 針對磁碟基礎的資料表，資料類型可以是下列其中一項：  
  
-   系統資料類型。  
  
-   依據 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型的別名資料類型。 別名資料類型是利用 CREATE TYPE 陳述式建立的，在這之後才能在資料表定義中使用它們。 在 CREATE TABLE 陳述式期間，可以覆寫別名資料類型的 NULL 或 NOT NULL 指派。 不過，長度規格不能變更；在 CREATE TABLE 陳述式中，不能指定別名資料類型的長度。  
  
-   CLR 使用者定義型別。 CLR 使用者定義型別是利用 CREATE TYPE 陳述式來建立的，之後，才能在資料表定義中使用它們。 若要建立 CLR 使用者定義型別的資料行，便需要類型的 REFERENCES 權限。  
  
 如果*type_schema_name*未指定，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]參考*type_name*順序如下：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型。  
  
-   目前資料庫中之目前使用者的預設結構描述。  
  
-   目前資料庫中的 **dbo** 結構描述。  
  
 對於記憶體最佳化的資料表，請參閱[記憶體中 OLTP 的支援資料型別](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)如需支援的系統類型的清單。  
  
 *有效位數*  
 這是指定之資料類型的有效位數。 如需有關有效位數值的詳細資訊，請參閱[有效位數、 小數位數和長度](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
 *scale*  
 這是指定資料類型的小數位數。 如需有關有效小數位數值的詳細資訊，請參閱[有效位數、 小數位數和長度](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
 **最大值**  
 僅適用於**varchar**， **nvarchar**，和**varbinary**資料類型來儲存 2 ^31 位元組的字元和二進位資料，以及 2 ^30 位元組的 Unicode 資料。  
  
 CONTENT  
 指定的每個執行個體**xml**中的資料類型*column_name*可以包含多個最上層元素。 CONTENT 只適用於**xml**資料類型，而且可以是只有當*xml_schema_collection*同時指定。 若未指定，CONTENT 便是預設行為。  
  
 DOCUMENT  
 指定的每個執行個體**xml**中的資料類型*column_name*可以只包含一個最上層元素。 DOCUMENT 只適用於**xml**資料類型，而且可以是只有當*xml_schema_collection*同時指定。  
  
 *xml_schema_collection*  
 僅適用於**xml**將 XML 結構描述集合與型別產生關聯的資料類型。 之前輸入**xml**結構描述資料行中的，結構描述必須先建立資料庫中使用[CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)。  
  
 DEFAULT  
 指定在插入期間未明確提供值時，提供給資料行的值。 可以套用 DEFAULT 定義，除了那些定義為任何資料行**時間戳記**，或含有 IDENTITY 屬性。 如果使用者定義型別資料行指定預設值，類型應該支援的隱含轉換*constant_expression*使用者定義型別。 當卸除資料表時，便會移除 DEFAULT 定義。 預設值只能使用常數值 (例如字元字串)、純量函數 (系統函數、使用者自訂函數或 CLR 函數) 或 NULL。 若要維護與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的相容性，您可以將條件約束名稱指派給 DEFAULT。  
  
 *constant_expression*  
 這是用來做為資料行預設值的常數、NULL 或系統函數。  
  
 *memory_optimized_constant_expression*  
 這是支援用來做為資料行預設值的常數、NULL 或系統函數。 必須在原生編譯的預存程序中受到支援。 如需原生編譯的預存程序中的內建函式的詳細資訊，請參閱[原生編譯 T-SQL 模組支援的功能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)。  
  
 IDENTITY  
 指出新資料行是識別欄位。 當新資料列加入資料表時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會提供資料行的唯一累加值。 識別欄位通常用來搭配 PRIMARY KEY 條件約束一起使用，做為資料表的唯一資料列識別碼。 IDENTITY 屬性可以指派給**tinyint**， **smallint**， **int**， **bigint**， **decimal(p,0)**，或**numeric(p,0)**資料行。 每份資料表都只能建立一個識別欄位。 繫結的預設值和 DEFAULT 條件約束無法搭配識別欄位使用。 您必須同時指定種子和遞增，或同時不指定這兩者。 如果同時不指定這兩者，預設值便是 (1,1)。  
  
 在記憶體最佳化資料表中，唯一允許的值兩者*種子*和*遞增*為 1。(1，1) 是預設值為*種子*和*遞增*。  
  
 *種子*  
 這是載入資料表的第一個資料列所用的值。  
  
 *遞增*  
 這是加入先前載入的資料列之識別值的累加值。  
  
 NOT FOR REPLICATION  
 在 CREATE TABLE 陳述式中，IDENTITY 屬性、FOREIGN KEY 條件約束和 CHECK 條件約束，都可以指定 NOT FOR REPLICATION 子句。 如果 IDENTITY 屬性指定了這個子句，當複寫代理程式執行插入時，值不會在識別欄位中累加。 如果條件約束指定了這個子句，當複寫代理程式執行插入、更新或刪除作業時，不會強制執行這個條件約束。  
  
 GENERATED ALWAYS AS 列 {開始 |結束} [隱藏] [NOT NULL]  
 **適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定指定之 datetime2 資料行使用由系統時記錄的記錄是有效的開始時間或記錄是有效的結束時間。 將資料行必須定義為 NOT NULL。 如果您嘗試將其指定為 NULL，系統將會擲回錯誤。 如果未明確指定的期間資料行的 NOT NULL，系統會依預設就為 NOT NULL 定義資料行。 使用這個引數搭配 PERIOD FOR SYSTEM_TIME 和與 SYSTEM_VERSIONING = ON 引數，若要啟用資料表上的系統版本設定。 如需相關資訊，請參閱 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)。  
  
 您可以使用的一或兩個期間資料行**隱藏**隱含地隱藏這些資料行的旗標，**選取\*FROM**  *`<table>`* 則否傳回這些資料行的值。 根據預設，將不會隱藏期間資料行。 才能加以使用，隱藏的資料行必須明確包含在所有查詢直接參考時態表中。 若要變更**隱藏**現有期間資料行的屬性**期間**必須卸除並重新建立以不同的隱藏旗標。  
  
 `INDEX *index_name* [ CLUSTERED | NONCLUSTERED ] (*column_name* [ ASC | DESC ] [ ,... *n* ] )`  
     
**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

指定要在資料表上建立索引。 這可以是叢集的索引或非叢集的索引。 包含資料行，列出，並會遞增或遞減順序資料進行排序的索引。  
  
 索引*index_name*叢集資料行存放區  
   
  
**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
 指定用來儲存整份資料表具有叢集資料行存放區索引的單欄式格式。 這一律會包含資料表中的所有資料行。 不，以字母或數字的順序來排序資料，因為資料列會組織來取得資料行存放區壓縮的優點。  
  
 索引*index_name* [非叢集] 資料行存放區 (*column_name* [，...*n* ] )  
   
  
**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
 指定要在資料表上建立非叢集資料行存放區索引。 基礎資料表可以是資料列存放區堆積或叢集的索引，或非叢集資料行存放區索引。 在所有情況下，在資料表上建立非叢集資料行存放區索引會儲存在索引中的資料行的資料的第二個複本。  
  
 非叢集資料行存放區索引會儲存，並以叢集資料行存放區索引進行管理。 因為資料行可能會受到限制，而且存在為次要索引的資料表上呼叫一個非叢集資料行存放區索引。  
  
 ON *partition_scheme_name***(***column_name***)**  
 指定分割區配置來定義要做為分割區索引之分割區對應目標的檔案群組。 資料分割配置必須存在於資料庫中執行[CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)或[ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md)。 *column_name*指定資料分割的索引將會分割依據的資料行。 此資料行必須符合資料類型、 長度和有效位數引數的資料分割函式， *partition_scheme_name*使用。 *column_name*未限制為索引定義中的資料行。 基底資料表中的任何資料行都可以指定，但在分割唯一索引， *column_name*必須選擇從做的唯一索引鍵。 這項限制可讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 只在單一分割區內驗證索引鍵值的唯一性。  
  
> [!NOTE]  
>  當您分割一個非唯一的叢集索引時，如果尚未指定分割區資料行，依預設，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將它加入至叢集索引鍵清單。 當您分割一個非唯一的非叢集索引時，如果尚未指定分割區資料行，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將它新增為索引的非索引鍵 (內含) 資料行。  
  
 如果*partition_scheme_name*或*檔案群組*未指定和資料表資料分割，此索引會放在相同的資料分割配置，使用相同的分割資料行，做為基礎的資料表。  
  
> [!NOTE]  
>  您無法在 XML 索引上指定分割區配置。 如果基底資料表已分割，XML 索引會使用與資料表相同的分割區配置。  
  
 如需有關資料分割索引， [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。  
  
 ON *filegroup_name*  
 在指定的檔案群組上建立指定的索引。 如果未指定位置，且資料表或檢視表未分割，則索引會使用與基礎資料表或檢視表相同的檔案群組。 此檔案群組必須已存在。  
  
 ON **"**預設**"**  
 在預設的檔案群組上建立指定的索引。  
  
 在這個內容中，default 這個字不是關鍵字。 它是預設檔案群組的識別碼，必須加以分隔，如 ON **"**預設**"**或 ON **[**預設**]**。 如果指定了 "default"，目前工作階段的 QUOTED_IDENTIFIER 選項就必須是 ON。 這是預設值。 如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
 [FILESTREAM_ON { *filestream_filegroup_name* | *partition_scheme_name* |"NULL"}]  
   
**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion.md)]。

 指定在建立叢集索引時，資料表之 FILESTREAM 資料的位置。 FILESTREAM_ON 子句允許將 FILESTREAM 資料移到不同的 FILESTREAM 檔案群組或分割區配置。  
  
 *filestream_filegroup_name*是 FILESTREAM 檔案群組的名稱。 此檔案群組必須有一個檔案群組使用檔案群組定義[CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md)或[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)陳述式; 否則就會引發錯誤。  
  
 如果分割此資料表，則必須包含 FILESTREAM_ON 子句，而且必須指定 FILESTREAM 檔案群組的分割區配置，此配置會使用與資料表之分割區配置相同的分割區函數和分割區資料行。 否則，就會引發錯誤。  
  
 如果此資料表未分割，FILESTREAM 資料行將無法分割。 此資料表的 FILESTREAM 資料必須儲存在 FILESTREAM_ON 子句中指定的單一檔案群組內。  
  
 如果正在建立叢集索引，而且此資料表不包含 FILESTREAM 資料行，則可以在 CREATE INDEX 陳述式內指定 FILESTREAM_ON NULL。  
  
 如需詳細資訊，請參閱 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)。  
  
 ROWGUIDCOL  
 指出新資料行是一個資料列 GUID 資料行。 只有一個**uniqueidentifier**每個資料表的資料行可以指定為 ROWGUIDCOL 資料行。 套用 ROWGUIDCOL 屬性後便可以利用 $ROWGUID 來參考資料行。 ROWGUIDCOL 屬性指派給只**uniqueidentifier**資料行。 使用者定義資料類型資料行不能用 ROWGUIDCOL 來指定。  
  
 ROWGUIDCOL 屬性不會強制執行資料行中所儲存之值的唯一性。 它也不會自動為插入資料表中的新資料列產生值。 若要產生每個資料行的唯一值，請使用[NEWID](../../t-sql/functions/newid-transact-sql.md)或[NEWSEQUENTIALID](../../t-sql/functions/newsequentialid-transact-sql.md)函式上[插入](../../t-sql/statements/insert-transact-sql.md)陳述式，或使用這些函式做為預設值資料行。  
  
 使用加密  
 指定加密的資料行使用[永遠加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md)功能。  
  
 COLUMN_ENCRYPTION_KEY = *key_name*  
 指定資料行加密金鑰。 如需詳細資訊，請參閱[CREATE COLUMN ENCRYPTION KEY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md).  
  
 ENCRYPTION_TYPE = {決定性 |隨機}  
 **確定性加密** 使用的方法一律會針對任何指定純文字值產生相同加密值。 使用確定性加密允許搜尋使用相等比較，群組及聯結資料表使用等號比較聯結根據加密值，但也可讓未經授權的使用者透過檢視中的模式，猜測加密值資訊加密的資料行。 決定性加密資料行上聯結兩個資料表時才可能會使用相同的資料行加密金鑰加密兩個資料行。 確定性加密必須針對字元資料行使用 binary2 排序次序的資料行定序。  
  
 **隨機加密** 使用的方法會以更難預測的方式來加密資料。 隨機的加密較為安全，但會防止等號比較搜尋、 分組和聯結加密的資料行。 使用隨機的加密資料行無法編製索引。  
  
 將會搜尋或分組參數，例如政府識別碼數字的資料行，請使用決定性加密。 使用隨機的加密，例如信用卡號碼的資料，其中未利用其它記錄，或用來聯結資料表，以及因為您用來尋找包含加密的資料列的其他資料行 （例如，交易號碼），這不會針對搜尋感興趣的資料行。  
  
 資料行必須為合格的資料類型。  
  
 演算法  
 必須是**'AEAD_AES_256_CBC_HMAC_SHA_256'**。  
  
 如需詳細資訊，包括功能條件約束，請參閱[永遠加密 &#40; Database engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。  
  
 **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 SPARSE  
 指出此資料行是疏鬆資料行。 疏鬆資料行的儲存體會針對 Null 值最佳化。 疏鬆資料行無法指定為 NOT NULL。 如需其他限制和疏鬆資料行的詳細資訊，請參閱[使用疏鬆資料行](../../relational-databases/tables/use-sparse-columns.md)。  
  
 遮罩與 (函式 = ' *mask_function* ')  
 **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定動態資料遮罩。 *mask_function*的遮罩函數，以適當的參數名稱。 有三個函式：  
  
-   default （)  
  
-   email()  
  
-   partial()  
  
-   random()  
  
 函式參數，請參閱[動態資料遮罩](../../relational-databases/security/dynamic-data-masking.md)。  
  
 FILESTREAM  
   
**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion.md)]。

 僅適用於**varbinary （max)**資料行。 指定 FILESTREAM 儲存體**varbinary （max)** BLOB 資料。  
  
 資料表也必須有的資料行**uniqueidentifier**具有 ROWGUIDCOL 屬性的資料類型。 這個資料行不能允許 null 值，且必須具有 UNIQUE 或 PRIMARY KEY 單一資料行條件約束。 資料行的 GUID 值必須在插入資料時由應用程式提供，或是由使用 NEWID () 函數的 DEFAULT 條件約束所提供。  
  
 ROWGUIDCOL 資料行無法卸除，而且當資料表有定義 FILESTREAM 資料行時，無法變更相關的條件約束。 只有當最後一個 FILESTREAM 資料行卸除之後，才可卸除 ROWGUIDCOL 資料行。  
  
 當有針對資料行指定 FILESTREAM 儲存屬性時，該資料行的所有值都會儲存在檔案系統的 FILESTREAM 資料容器內。  
  
 COLLATE *sys.databases*  
 指定資料行的定序。 定序名稱可以是 Windows 定序名稱，也可以是 SQL 定序名稱。 *sys.databases*只適用於資料行的**char**， **varchar**，**文字**， **nchar**， **nvarchar**，和**ntext**資料型別。 若未指定，當資料行是使用者自訂資料類型時，便會將使用者自訂資料類型的定序指派給這個資料行，否則，便會指派資料庫的預設定序。  
  
 如需有關 Windows 和 SQL 定序名稱的詳細資訊，請參閱[Windows 定序名稱](../../t-sql/statements/windows-collation-name-transact-sql.md)和[SQL 定序名稱](../../t-sql/statements/sql-server-collation-name-transact-sql.md)。  
  
 如需有關 COLLATE 子句的詳細資訊，請參閱[COLLATE &#40;TRANSACT-SQL &#41;](~/t-sql/statements/collations.md).  
  
 CONSTRAINT  
 這是一個選擇性的關鍵字，用來指示開始定義 PRIMARY KEY、NOT NULL、UNIQUE、FOREIGN KEY 或 CHECK 條件約束。  
  
 *constraint_name*  
 這是條件約束的名稱。 在資料表所屬的結構描述內，條件約束名稱必須是唯一的。  
  
 NULL | NOT NULL  
 決定資料行中是否允許使用 NULL 值。 嚴格來說，NULL 並不算是條件約束，但是您可以如同指定 NOT NULL 一樣加以指定。 只有在也指定了 PERSISTED 時，計算資料行才能指定 NOT NULL。  
  
 PRIMARY KEY  
 這是一個條件約束，它利用唯一索引來強制執行一個或多個指定資料行的實體完整性。 每份資料表都只能建立一個 PRIMARY KEY 條件約束。  
  
 UNIQUE  
 這是一項條件約束，它透過唯一索引為指定的一個或多個資料行提供實體完整性。 一份資料表可以有多個 UNIQUE 條件約束。  
  
 CLUSTERED | NONCLUSTERED  
 指出針對 PRIMARY KEY 或 UNIQUE 條件約束建立叢集或非叢集索引。 PRIMARY KEY 條件約束預設為 CLUSTERED，UNIQUE 條件約束預設為 NONCLUSTERED。  
  
 在 CREATE TABLE 陳述式中，您只能將 CLUSTERED 指定給單一條件約束。 如果 UNIQUE 條件約束指定了 CLUSTERED，且也指定了 PRIMARY KEY 條件約束，PRIMARY KEY 便預設為 NONCLUSTERED。  
  
 下列範例顯示如何在磁碟資料表中使用 NONCLUSTERED：  
  
```  
CREATE TABLE t1 ( c1 int, INDEX ix_1 NONCLUSTERED (c1))   
CREATE TABLE t2( c1 int INDEX ix_1 NONCLUSTERED (c1))   
CREATE TABLE t3( c1 int, c2 int INDEX ix_1 NONCLUSTERED)   
CREATE TABLE t4( c1 int, c2 int, INDEX ix_1 NONCLUSTERED (c1,c2))  
```  
  
 FOREIGN KEY REFERENCES  
 這是一個條件約束，它提供一個或多個資料行中之資料的參考完整性。 FOREIGN KEY 條件約束要求資料行中的每個值存在於所參考之資料表中的一個或多個對應的被參考資料行中。 FOREIGN KEY 條件約束所參考的資料行，必須是所參考的資料表中的 PRIMARY KEY 或 UNIQUE 條件約束，或是所參考的資料表之 UNIQUE INDEX 中所參考的資料行。 計算資料行的外部索引鍵也必須標示為 PERSISTED。  
  
 [ *schema_name***。**]*referenced_table_name*]  
 這是 FOREIGN KEY 條件約束所參考之資料表的名稱，及其所屬的結構描述。  
  
 **(** *ref_column* [ **，**...*n* ] **)**  
 這是 FOREIGN KEY 條件約束所參考之資料表中的某資料行或資料行清單。  
  
 ON DELETE {**採取任何動作**|CASCADE |SET NULL |SET DEFAULT}  
 指定如果建立的資料表中之資料列有參考關聯性，且在父資料表中刪除了所參考的資料列，建立的資料表中之資料列會發生什麼動作。 預設值是 NO ACTION。  
  
 NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會產生一則錯誤，且會回復父資料表中之資料列的刪除動作。  
  
 CASCADE  
 如果從父資料表中刪除資料列，便會從進行參考的資料表中刪除對應的資料列。  
  
 SET NULL  
 如果刪除父資料表中對應的資料列，所有組成外部索引鍵的值都會設為 NULL。 若要執行這個條件約束，外部索引鍵資料行必須可為 Null。  
  
 SET DEFAULT  
 如果刪除父資料表中對應的資料列，所有組成外部索引鍵的值都會設為預設值。 若要執行這個條件約束，所有外部索引鍵資料行都必須有預設定義。 如果有可為 Null 的資料行，但沒有設定明確的預設值，NULL 便成為這個資料行的隱含預設值。  
  
 如果資料表要包含在使用邏輯記錄的合併式發行集中，請勿指定 CASCADE。 如需邏輯記錄的詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
 如果資料表已有 INSTEAD OF 觸發程序 ON DELETE，便無法定義 ON DELETE CASCADE。  
  
 例如，在[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]資料庫**ProductVendor**資料表有參考關聯性**廠商**資料表。 **ProductVendor.BusinessEntityID**外部索引鍵參考**Vendor.BusinessEntityID**主索引鍵。  
  
 如果 DELETE 陳述式會執行中的資料列**廠商**資料表，且 ON DELETE CASCADE 動作指定了**ProductVendor.BusinessEntityID**、[!INCLUDE[ssDE](../../includes/ssde-md.md)]一或多個相依的檢查中的資料列**ProductVendor**資料表。 如果任何存在的相依資料列中**ProductVendor**會刪除資料表和資料列中的參考也**廠商**資料表。  
  
 相反地，如果指定了 NO ACTION，[!INCLUDE[ssDE](../../includes/ssde-md.md)]引發錯誤，並且會回復 delete 動作上**廠商**資料列中的至少一個資料列是否**ProductVendor**在參考的資料表。  
  
 在更新 {**採取任何動作**|CASCADE |SET NULL |SET DEFAULT}  
 指定當變更的資料表中之資料列有參考關聯性，且在父資料表中所參考的資料列有了更新時，變更的資料表中之資料列會發生什麼動作。 預設值是 NO ACTION。  
  
 NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會產生一則錯誤，且會回復父資料表中之資料列的更新動作。  
  
 CASCADE  
 當父資料表中的資料列有了更新時，在進行參考的資料表中，也會更新對應的資料列。  
  
 SET NULL  
 當更新父資料表中對應的資料列時，所有組成外部索引鍵的值都會設為 NULL。 若要執行這個條件約束，外部索引鍵資料行必須可為 Null。  
  
 SET DEFAULT  
 當更新父資料表中對應的資料列時，所有組成外部索引鍵的值都會設為預設值。 若要執行這個條件約束，所有外部索引鍵資料行都必須有預設定義。 如果有可為 Null 的資料行，但沒有設定明確的預設值，NULL 便成為這個資料行的隱含預設值。  
  
 如果資料表要包含在使用邏輯記錄的合併式發行集中，請勿指定 CASCADE。 如需邏輯記錄的詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
 如果在 INSTEAD OF 觸發程序 ON UPDATE 已經存在已警示的資料表，則無法定義ON UPDATE CASCADE、SET NULL、或 SET DEFAULT。  
  
 例如，在[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]資料庫**ProductVendor**資料表有參考關聯性**廠商**資料表： **ProductVendor.BusinessEntity**外部索引鍵參考**Vendor.BusinessEntityID**主索引鍵。  
  
 如果 UPDATE 陳述式會執行中的資料列**廠商**指定資料表和 ON UPDATE CASCADE 動作**ProductVendor.BusinessEntityID**、[!INCLUDE[ssDE](../../includes/ssde-md.md)]一或多個相依的檢查中的資料列**ProductVendor**資料表。 如果任何存在的相依資料列中**ProductVendor**資料表會更新，而且資料列中的參考也**廠商**資料表。  
  
 相反地，如果指定了 NO ACTION，[!INCLUDE[ssDE](../../includes/ssde-md.md)]引發錯誤，並且會回復更新動作上**廠商**資料列中的至少一個資料列是否**ProductVendor**在參考的資料表。  
  
 CHECK  
 這是一個條件約束，藉由限制可能輸入一個或多個資料行的值，強制執行範圍完整性。 計算資料行的 CHECK 條件約束也必須標示 PERSISTED。  
  
 *logical_expression*  
 這是一個傳回 TRUE 或 FALSE 的邏輯運算式。 這個運算式不能含有別名資料類型。  
  
 *資料行*  
 這是資料表條件約束中的一個資料行或一份資料行清單 (用括號括住)，用來指示條件約束定義中所用的各個資料行。  
  
 [ **ASC** |DESC]  
 指定一個或多個資料行參與資料表條件約束的排序順序。 預設值是 ASC。  
  
 *partition_scheme_name*  
 這是分割區配置的名稱，這個分割區配置定義了分割區資料表的分割區所對應的檔案群組。 分割區配置必須在資料庫內。  
  
 [ *partition_column_name***。** ]  
 指定分割區資料表將進行分割的資料行。 資料行必須符合指定資料分割中的函式， *partition_scheme_name*使用根據資料類型、 長度和有效位數。 參與分割區函數的計算資料行必須明確地標示為 PERSISTED。  
  
> [!IMPORTANT]  
>  我們建議您在分割區資料表的分割資料行上指定 NOT NULL，以及在非分割區資料表 (ALTER TABLE...SWITCH 作業的來源或目標) 上進行這項作業。 這樣做可以確保分割資料行上的任何 CHECK 條件約束都不需要檢查 Null 值。  
  
 FILLFACTOR  **=** *填滿因數*  
 指定用來儲存索引資料的每個索引頁面，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 所應加以填滿的程度。 使用者指定*填滿因數*值可以是從 1 到 100 之間。 如果未指定值，預設值為 0。 填滿因數值 0 和 100 在各方面都是一樣的。  
  
> [!IMPORTANT]  
>  WITH FILLFACTOR =*填滿因數*唯一的索引選項適用於 PRIMARY KEY 或 UNIQUE 條件約束，為了與舊版相容，但將不會記載在這種方式在未來的版本。  
  
 *create* XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
 這是資料行集的名稱。 資料行集是不具類型的 XML 表示，可將資料表的所有疏鬆資料行結合到結構化輸出中。 如需資料行集的詳細資訊，請參閱 [使用資料行集](../../relational-databases/tables/use-column-sets.md)。  
  
 導致 PERIOD FOR SYSTEM_TIME (*system_start_time_column_name* ， *system_end_time_column_name* )  
   
**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
 指定的名稱，系統會記錄的有效期間使用的資料行。 使用這個引數搭配產生一律 AS 列 {開始 |結束} 和 SYSTEM_VERSIONING = 啟用系統版本設定資料表上的引數。 如需相關資訊，請參閱 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)。  
  
 COMPRESSION_DELAY  
   
**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
 針對記憶體最佳化，延遲在資料表中，保持不變，適合壓縮到資料行存放區索引之前指定的分鐘的資料列必須維持的最小數目。 SQL Server 會選取特定的資料列壓縮根據上次更新時間。 例如，如果資料列要在兩小時期間內的時間經常變更，您可以設定 COMPRESSION_DELAY = 120 分鐘以確保 SQL Server 會壓縮資料列之前，會完成更新。  
  
 針對以磁碟為基礎的資料表，延遲指定分鐘的時間必須保持在關閉狀態的差異資料列群組的最小數目差異資料列群組之前中 SQL Server 可以壓縮到壓縮的資料列群組。 因為磁碟基礎的資料表不會追蹤插入和更新時間在個別的資料列，SQL Server 適用於延遲差異資料列群組處於已關閉狀態。  
  
 預設值是 0 分鐘。  
  
 如需何時使用 COMPRESSION_DELAY，建議，請參閱[開始使用資料行存放區進行即時作業分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
  
 \<table_option >:: = 指定一或多個資料表選項。  
  
 DATA_COMPRESSION  
 針對指定的資料表、分割區編號或分割區範圍指定資料壓縮選項。 選項如下：  
  
 無  
 不壓縮資料表或指定的分割區。  
  
 ROW  
 使用資料列壓縮來壓縮資料表或指定的分割區。  
  
 PAGE  
 使用頁面壓縮來壓縮資料表或指定的分割區。  
  
 COLUMNSTORE  
   
  
**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
 只適用於資料行存放區索引，包括非叢集資料行存放區索引和叢集資料行存放區索引。 資料行存放區指定壓縮與大部分的高效能資料行存放區壓縮。 這是典型的選擇。  
  
 COLUMNSTORE_ARCHIVE  
   
  
**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 只適用於資料行存放區索引，包括非叢集資料行存放區索引和叢集資料行存放區索引。 COLUMNSTORE_ARCHIVE 將進一步壓縮，資料表或資料分割成較小的大小。 這可用於封存，或是其他需要較小儲存體，而且可負擔更多時間來儲存和擷取的狀況。  
  
 如需有關壓縮的詳細資訊，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
 在資料分割上**(** { `<partition_number_expression>` |[ **,**...*n* ] **)**  
 指定套用 DATA_COMPRESSION 設定的分割區。 如果未分割此資料表，ON PARTITIONS 引數將會產生錯誤。 如果未提供 ON PARTITIONS 子句，DATA_COMPRESSION 選項將會套用到資料分割資料表的所有資料分割。  
  
 *編號運算式*可以下列方式指定：  
  
-   提供分割區的分割區編號，例如：ON PARTITIONS (2)。  
  
-   為數個個別分割區提供以逗號分隔的分割區編號，例如：ON PARTITIONS (1, 5)。  
  
-   同時提供範圍和個別分割區，例如：ON PARTITIONS (2, 4, 6 TO 8)。  
  
 `<range>`您可以指定為資料分割數字分隔的例如： ON PARTITIONS (6 TO 8)。  
  
 若要為不同的分割區設定不同類型的資料壓縮，請指定 DATA_COMPRESSION 選項一次以上，例如：  
  
```  
WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
)  
```  
  
 \<index_option >:: =  
 指定一個或多個索引選項。 如需這些選項的完整說明，請參閱[CREATE INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 PAD_INDEX = {ON |**OFF** }  
 當設為 ON 時，便會在索引的中繼層級頁面上，套用 FILLFACTOR 所指定的可用空間百分比。 當設為 OFF 或未指定 FILLFACTOR 值時，考慮到中繼頁面的各組索引鍵，中繼層級頁面容量的填滿程度，會保留至少足以容納一個資料列的空間，且資料列是索引所能擁有的大小上限。 預設值為 OFF。  
  
 填滿因數 **=** *填滿因數*  
 指定一個百分比來指出在建立或改變索引期間，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 應該使各索引頁面之分葉層級填滿的程度。 *填滿因數*必須是介於 1 到 100 之間的整數值。 預設值是 0。 填滿因數值 0 和 100 在各方面都是一樣的。  
  
 IGNORE_DUP_KEY = {ON |**OFF** }  
 指定當插入作業嘗試將重複的索引鍵值插入唯一索引時所產生的錯誤回應。 IGNORE_DUP_KEY 選項只適用於在建立或重建索引之後所發生的插入作業。 選項沒有任何作用，執行時[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)， [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)，或[更新](../../t-sql/queries/update-transact-sql.md)。 預設值為 OFF。  
  
 ON  
 當重複的索引鍵值插入唯一索引時，就會出現警告訊息。 只有違反唯一性條件約束的資料列才會失敗。  
  
 OFF  
 當重複的索引鍵值插入唯一索引時，就會出現錯誤訊息。 整個 INSERT 作業將會回復。  
  
 若為針對檢視表所建立的索引、非唯一索引、XML 索引、空間索引和篩選索引，IGNORE_DUP_KEY 不得設為 ON。  
  
 若要檢視 IGNORE_DUP_KEY，請使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。  
  
 在與舊版本相容的語法中，WITH IGNORE_DUP_KEY 相當於 WITH IGNORE_DUP_KEY = ON。  
  
 STATISTICS_NORECOMPUTE  **=**  {ON |**OFF** }  
 當設為 ON 時，不會自動重新計算過期的索引統計資料。 當設為 OFF 時，便會啟用統計資料的自動更新。 預設值為 OFF。  
  
 ALLOW_ROW_LOCKS  **=**  { **ON** |OFF}  
 當設為 ON 時，在您存取索引時，允許資料列鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會決定使用資料列鎖定的時機。 當設為 OFF 時，不會使用資料列鎖定。 預設值是 ON。  
  
 ALLOW_PAGE_LOCKS  **=**  { **ON** |OFF}  
 當設為 ON 時，在您存取索引時，允許頁面鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會決定使用頁面鎖定的時機。 當設為 OFF 時，不會使用頁面鎖定。 預設值是 ON。  
  
 FILETABLE_DIRECTORY = *directory_name*  
   
  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
  
 指定 Windows 相容的 FileTable 目錄名稱。 在資料庫的所有 FileTable 目錄名稱之間，此名稱必須是唯一的。 無論定序設定為何，唯一性比較皆不會區分大小寫。 如果未指定此值，就會使用 FileTable 的名稱。  
  
 FILETABLE_COLLATE_FILENAME = { *sys.databases* | database_default}  
   
  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
  
 指定定序名稱，用於套用至 FileTable 中的 **Name** 資料行。 定序必須不區分大小寫，以符合 Windows 檔案命名語義。 如果未指定此值，就會使用資料庫預設定序。 如果資料庫預設定序區分大小寫，則會引發錯誤，而且 CREATE TABLE 作業會失敗。  
  
 *sys.databases*  
 不區分大小寫的定序名稱。  
  
 database_default  
 指定所要使用的資料庫預設定序。 此定序不可區分大小寫。  
  
 FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME = *constraint_name*  
   
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
  
 指定在 FileTable 上自動建立的主索引鍵條件約束所要使用的名稱。 如果未指定此值，系統就會產生條件約束的名稱。  
  
 FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME = *constraint_name*  
   
  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
  
 指定要用於自動建立 unique 條件約束名稱**stream_id** FileTable 中的資料行。 如果未指定此值，系統就會產生條件約束的名稱。  
  
 FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME = *constraint_name*  
   
  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
  
 指定要用於自動建立 unique 條件約束名稱**parent_path_locator**和**名稱**FileTable 中的資料行。 如果未指定此值，系統就會產生條件約束的名稱。  
  
 SYSTEM_VERSIONING  **=**  ON [(HISTORY_TABLE  **=**  *schema_name* 。  *名稱*[，DATA_CONSISTENCY_CHECK  **=**  { **ON** |關閉}]）]  
   
  
**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。   
  
 如果符合的資料類型、 null 屬性的條件約束和主索引鍵條件約束需求，可讓系統版本設定的資料表。 如果**HISTORY_TABLE**不使用引數，系統就會產生新的記錄資料表，比對目前的資料表中，兩個資料表之間建立連結的相同檔案群組中的目前資料表的結構描述並可以讓系統記錄每一筆記錄歷程記錄資料表中目前的資料表中。 此歷程記錄資料表的名稱會是`MSSQL_TemporalHistoryFor<primary_table_object_id>`。 根據預設，歷程記錄資料表會採 **PAGE** 壓縮處理。 如果 HISTORY_TABLE 引數用來建立的連結，並使用現有的記錄資料表，是目前的資料表和指定的資料表之間建立連結。 若目前的資料表已分割，則會在預設檔案群組上建立歷程記錄資料表，這是因為資料分割設定不會自動從目前的資料表複寫至歷程記錄資料表。 若在建立歷程記錄資料表時指定歷程記錄資料表名稱，則您必須指定結構描述和資料表名稱。 建立現有記錄資料表的連結時，您可以選擇執行資料一致性檢查。 這項資料一致性檢查可確保現有的記錄沒有重疊。 預設執行資料一致性檢查。 使用這個引數搭配 PERIOD FOR SYSTEM_TIME 和產生一律 AS 列 {開始 |若要啟用系統版本設定資料表上的結束} 引數。 如需相關資訊，請參閱 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)。  
  
 REMOTE_DATA_ARCHIVE = {ON [( *table_stretch_options* [，… n])] |關閉 (MIGRATION_STATE = 暫停)}  
   
  
**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 建立新的資料表，啟用或停用 Stretch database。 如需詳細資訊，請參閱 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)。  
  
 **為資料表啟用 Stretch Database**  
  
 當您啟用 Stretch 的資料表指定`ON`，您可以選擇性地指定`MIGRATION_STATE = OUTBOUND`開始移轉資料的立即或`MIGRATION_STATE = PAUSED`延後資料移轉。 預設值是`MIGRATION_STATE = OUTBOUND`。 如需啟用 Stretch 的資料表的詳細資訊，請參閱[針對資料表啟用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)。  
  
 **必要條件**。 為資料表啟用 「 延展 」 之前，您必須在伺服器和資料庫上啟用 Stretch。 如需詳細資訊，請參閱 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)。  
  
 **權限**。 啟用 Stretch 的資料庫或資料表需要 db_owner 權限。 啟用 Stretch 的資料表也需要資料表的 ALTER 權限。  
  
 [FILTER_PREDICATE = {null |*述詞*}]  
   
  
**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 （選擇性） 指定篩選述詞來選取要移轉包含歷史和目前資料的資料表資料列。 此述詞必須呼叫決定性內嵌資料表值函式。 如需詳細資訊，請參閱[針對資料表啟用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)和[選取使用篩選函數來移轉的資料列](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)。 
   
> [!IMPORTANT]  
>  若您提供執行狀況不佳的篩選器述詞，資料移轉也無法順利執行。 Stretch Database 使用 CROSS APPLY 運算子，將篩選器述詞套用至資料表。  
  
 若您未指定篩選器述詞，則會遷移整個資料表。  
  
 當您指定篩選器述詞時，您也必須指定*MIGRATION_STATE*。  
  
 MIGRATION_STATE = {輸出 | 輸入 |暫停}  
   
  
**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，和 SQL Azure。 
  
-   指定`OUTBOUND`將資料從 SQL Server 移轉至 Azure。  
  
-   指定`INBOUND`複製遠端從 Azure 資料表的資料會備份到 SQL Server，以及針對資料表停用 Stretch。 如需詳細資訊，請參閱 [停用 Stretch Database 並帶回遠端資料](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)。  
  
     此作業會產生資料傳輸成本，且無法取消。  
  
-   指定`PAUSED`暫停或延後資料移轉。 如需詳細資訊，請參閱[暫停和繼續資料移轉 &#40;Stretch Database &#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
 MEMORY_OPTIMIZED  
   
  
**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 值，在表示資料表是記憶體最佳化。 記憶體最佳化資料表是記憶體中 OLTP 功能，可用來最佳化效能的交易處理的一部分。 若要開始使用記憶體中 OLTP 看到[快速入門 1: TRANSACT-SQL 效能更快的記憶體內部 OLTP 技術](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)。 如需記憶體最佳化資料表的更深入資訊，請參閱[記憶體最佳化資料表](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)。  
  
 預設值 OFF 表示資料表是以磁碟為基礎。  
  
 DURABILITY  
   
  
**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。   
  
 SCHEMA_AND_DATA 的值表示資料表是持久的也就是說，變更保存在磁碟上，而且不會被重新啟動或容錯移轉。  SCHEMA_AND_DATA 是預設值。  
  
 SCHEMA_ONLY 的值表示資料表是非持久的。 資料表結構描述會保存，但是任何資料更新不會保存在重新啟動或容錯移轉的資料庫。 DURABILITY = SCHEMA_ONLY 只能搭配 MEMORY_OPTIMIZED = ON。  
  
> [!WARNING]  
>  與建立資料表時**DURABILITY = SCHEMA_ONLY**，和**READ_COMMITTED_SNAPSHOT**使用後續變更**ALTER DATABASE**，資料表中的資料將會遺失。  
  
 BUCKET_COUNT  
   
  
**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 
  
 指出應該在雜湊索引中建立的貯體數目。 雜湊索引中 BUCKET_COUNT 的最大值是 1,073,741,824。 如需有關值區計數的詳細資訊，請參閱[記憶體最佳化資料表的索引](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)。  
  
 Bucket_count 是必要的引數。  
  
 INDEX  
   
  
**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 
  
資料行和資料表的索引，可以指定為 CREATE TABLE 陳述式的一部分。 如需加入和移除記憶體最佳化資料表上的索引詳細資料，請參閱：[改變記憶體最佳化資料表](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)
  
 HASH  
   
  
**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 
  
 表示已建立雜湊索引。  
  
 只有記憶體最佳化資料表才支援雜湊索引。  
  
## <a name="remarks"></a>備註  
 允許的資料表、 資料行、 條件約束和索引之數目的相關資訊，請參閱[Maximum Capacity Specifications for SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md)。  
  
 空間通常會以每次一個範圍的遞增方式配置給資料表及索引。 當 ALTER DATABASE 的 SET MIXED_PAGE_ALLOCATION 選項設定為 TRUE，或一律之前[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]、 建立資料表或索引時，它會從混合範圍配置頁面，直到有足夠的頁填滿統一範圍。 在它有足以填滿統一範圍的頁面之後，每當目前配置的範圍已滿之後，便會配置另一個範圍。 對於資料表所配置和使用的空間量的相關報表，請執行**sp_spaceused**。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 不會強制在資料行定義中指定 DEFAULT、IDENTITY、ROWGUIDCOL 或資料行條件約束的順序。  
  
 當建立資料表時，一律會在資料表的中繼資料中將 QUOTED IDENTIFIER 選項儲存成 ON，即使建立資料表時，將選項設成 OFF，也是如此。  
  
## <a name="temporary-tables"></a>暫存資料表  
 您可以建立本機和全域暫存資料表。 本機暫存資料表只在目前工作階段中才可以看見，全域暫存資料表則是所有工作階段都能夠看見。 暫存資料表不能進行分割。  
  
 本機暫存資料表名稱前面加上一個數字符號 (#*table_name*)，和全域暫存資料表名稱前面加上兩個數字符號 (# #*table_name*)。  
  
 SQL 陳述式使用指定的值來參考暫存資料表*table_name*的 CREATE TABLE 陳述式中，範例 # # #:  
  
```  
CREATE TABLE #MyTempTable (cola INT PRIMARY KEY);  
  
INSERT INTO #MyTempTable VALUES (1);  
```  
  
 如果在單一預存程序或批次內，建立了多個暫存資料表，它們必須有不同的名稱。  
  
 如果本機暫存資料表建立在多位使用者可以同時執行的預存程序或應用程式中，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 必須能夠區分不同使用者所建立的資料表。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會在內部將數值後置詞附加至每個本機暫存資料表名稱上，以便區分它們。 為儲存在暫存資料表的完整名稱**sysobjects**資料表中**tempdb**所組成的 CREATE TABLE 陳述式與系統產生的數字尾碼所指定的資料表名稱。 若要以便進行後置*table_name*指定給本機暫存名稱不能超過 116 個字元。  
  
 除非利用 DROP TABLE 來明確卸除暫存資料表，否則，暫存資料表會在超出範圍時自動卸除：  
  
-   當預存程序完成時，會自動卸除預存程序中所建立的本機暫存資料表。 建立資料表的預存程序所執行的任何巢狀預存程序，都可以參考這份資料表。 呼叫建立資料表的預存程序之處理序不能參考這份資料表。  
  
-   在目前工作階段結束時，會自動卸除所有其他本機暫存資料表。  
  
-   當建立全域暫存資料表的工作階段結束，且所有其他工作也都停止參考這些資料表，便會自動卸除這些全域暫存資料表。 工作和資料表之間的關聯，只在單一 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的生命期間進行維護。 這表示當建立工作階段結束時，在最後一個主動參考這份資料表的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式完成時，便會卸除這份全域暫存資料表。  
  
 在預存程序或觸發程序內建立的本機暫存資料表，名稱可以和呼叫這個預存程序或觸發程序之前所建立的暫存資料表相同。 不過，如果查詢參考一份暫存資料表，且同時有兩份同名的暫存資料表存在，便不會定義要針對哪一份資料表來解析這項查詢。 巢狀預存程序也可以建立與呼叫的預存程序所建立之暫存資料表同名的暫存資料表。 不過，若要將修正解析到巢狀程序中所建立的資料表，這份資料表與發出呼叫的程序所建立的資料表，必須有相同的結構和資料行名稱。 下列範例會顯示這一點。  
  
```  
CREATE PROCEDURE dbo.Test2  
AS  
    CREATE TABLE #t(x INT PRIMARY KEY);  
    INSERT INTO #t VALUES (2);  
    SELECT Test2Col = x FROM #t;  
GO  
  
CREATE PROCEDURE dbo.Test1  
AS  
    CREATE TABLE #t(x INT PRIMARY KEY);  
    INSERT INTO #t VALUES (1);  
    SELECT Test1Col = x FROM #t;  
EXEC Test2;  
GO  
  
CREATE TABLE #t(x INT PRIMARY KEY);  
INSERT INTO #t VALUES (99);  
GO  
  
EXEC Test1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 (1 row(s) affected) 
 Test1Col 
 ----------- 
 1 

 (1 row(s) affected) 
 Test2Col 
 ----------- 
 2 
 ```
  
 當您建立本機或全域暫存資料表時，CREATE TABLE 語法會支援 FOREIGN KEY 條件約束以外的條件約束定義。 如果在暫存資料表中指定 FOREIGN KEY 條件約束，陳述式會傳回一則說明已略過條件約束的警告訊息。 這份資料表仍會建立，但不含 FOREIGN KEY 條件約束。 FOREIGN KEY 條件約束不能參考暫存資料表。  
  
 如果您使用具名條件約束來建立暫存資料表，而且在使用者定義交易的範圍內建立此暫存資料表，則一次只有一位使用者能夠執行建立暫存資料表的陳述式。 例如，如果預存程序使用了具名的主索引鍵條件約束來建立暫存資料表，此預存程序就無法同時由多位使用者執行。  


## <a name="database-scoped-global-temporary-tables-azure-sql-database"></a>資料庫範圍的全域暫存資料表 (Azure SQL Database)

適用於 SQL Server 的全域暫存資料表 (使用起始 # # 資料表名稱) 會儲存在 tempdb 中和所有使用者的工作階段之間共用的整個 SQL Server 執行個體。 SQL 資料表類型的相關資訊，請參閱上建立資料表的上一節。  

Azure SQL Database 支援全域暫存資料表也儲存在 tempdb 中，而且範圍限定為資料庫層級。  這表示全域暫存資料表共用相同的 Azure SQL 資料庫中的所有使用者的工作階段。 與其他 Azure SQL 資料庫的使用者工作階段無法存取全域暫存資料表。

Azure SQL 資料庫的全域暫存資料表遵循相同的語法和語意，SQL Server 用於暫存資料表。  同樣地，全域的暫存預存程序也範圍為資料庫層級，在 Azure SQL DB。 本機暫存資料表 （使用 # 資料表名稱起始） 也支援 Azure SQL Database，並遵循相同的語法和語意，SQL Server 使用。  請參閱上一節[暫存資料表](#temporary-tables)。  

> [!IMPORTANT]
> 這項功能處於公開預覽狀態，供 Azure SQL Database。
>

### <a name="troubleshooting-global-temporary-tables-for-azure-sql-db"></a>疑難排解 Azure SQL 資料庫的全域暫存資料表 

如需疑難排解 tempdb，請參閱[疑難排解足夠的磁碟空間在 tempdb 中](https://technet.microsoft.com/library/ms176029%28v=sql.105%29.aspx?f=255&MSPPError=-2147217396)。 若要存取 Azure SQL Database 中的疑難排解 Dmv，您必須是伺服器管理員。
  
### <a name="permissions"></a>Permissions  

 任何使用者可以建立全域暫存物件。 除非收到其他權限，否則使用者只能存取自己的物件。 執行個體時提供 SQL Server 登入。  
  
### <a name="examples"></a>範例 

- 工作階段 A 中 Azure SQL Database testdb1 建立全域暫存資料表 ##test，並將加入 1 個資料列

```tsql
CREATE TABLE ##test ( a int, b int);
INSERT INTO ##test values (1,1);

--Obtain object ID for temp table ##test 
SELECT OBJECT_ID('tempdb.dbo.##test') AS 'Object ID'; 

---Result
1253579504

---Obtain global temp table name for a given object ID 1253579504 in tempdb (2)
SELECT name FROM tempdb.sys.objects WHERE object_id = 1253579504

---Result
##test
```
- 工作階段 B 會連接到 Azure SQL Database testdb1，而且可以存取資料表建立的工作階段 A ##test

```tsql
SELECT * FROM ##test
---Results
1,1
```

- C 的工作階段連接至 Azure SQL Database testdb2 中的另一個資料庫，並想要存取 ##test testdb1 中建立。 這個，請選取失敗，因為全域暫存資料表的資料庫範圍 

```tsql
SELECT * FROM ##test
---Results
Msg 208, Level 16, State 0, Line 1
Invalid object name '##test'
```

- 從目前的使用者資料庫 testdb1 定址 Azure SQL Database tempdb 中的系統物件

```tsql
SELECT * FROM tempdb.sys.objects
SELECT * FROM tempdb.sys.columns
SELECT * FROM tempdb.sys.database_files
```



## <a name="partitioned-tables"></a>分割區資料表  
 在利用 CREATE TABLE 來建立分割區資料表之前，您必須先建立一個分割區函數來指定資料表分割區的方式。 使用建立分割區函數[CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md)。 其次，您必須建立一個分割區配置來指定保留分割區函數所指示之分割區的檔案群組。 使用建立分割區配置[CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)。 您不能針對分割區資料表來指定將 PRIMARY KEY 或 UNIQUE 條件約束放在個別檔案群組中。 如需詳細資訊，請參閱 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。  
  
## <a name="primary-key-constraints"></a>PRIMARY KEY 條件約束  
  
-   一份資料表只能有一個 PRIMARY KEY 條件約束。  
  
-   PRIMARY KEY 條件約束所產生的索引，無法使資料表的索引數目超出 999 個非叢集索引和 1 個叢集索引。  
  
-   如果未指定 PRIMARY KEY 條件約束的 CLUSTERED 或 NONCLUSTERED，且未指定 UNIQUE 條件約束的叢集索引，便使用 CLUSTERED。  
  
-   PRIMARY KEY 條件約束內所定義的所有資料行，都必須定義成 NOT NULL。 如果未指定 Null 屬性，參與 PRIMARY KEY 條件約束的所有資料行，其 Null 屬性都會設成 NOT NULL。  
  
    > [!NOTE]  
    >  對於記憶體最佳化的資料表，允許 Null 索引鍵資料行。  
  
-   如果在 CLR 使用者定義的類型資料行上定義主索引鍵，類型的實作必須支援二進位排序。 如需詳細資訊，請參閱 [CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
## <a name="unique-constraints"></a>UNIQUE 條件約束  
  
-   如果未指定 UNIQUE 條件約束的 NONCLUSTERED 或 NONCLUSTERED，依預設，會使用 NONCLUSTERED。  
  
-   每個 UNIQUE 條件約束都會產生一個索引。 UNIQUE 條件約束數目無法使資料表的索引數目超出 999 個非叢集索引和 1 個叢集索引。  
  
-   如果在 CLR 使用者定義型別資料行上定義唯一條件約束，類型的實作必須支援二進位順序或以運算子為基礎的順序。 如需詳細資訊，請參閱 [CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
## <a name="foreign-key-constraints"></a>FOREIGN KEY 條件約束  
  
-   在 FOREIGN KEY 條件約束的資料行中輸入 NULL 以外的值時，值必須在參考的資料行中；否則，系統會傳回外部索引鍵違規錯誤訊息。  
  
-   除非您也指定了來源資料行，否則，FOREIGN KEY 條件約束會套用在前面的資料行。  
  
-   FOREIGN KEY 條件約束只能參考在相同伺服器之相同資料庫內的資料表。 跨資料庫參考完整性必須利用觸發程序來實作。 如需詳細資訊，請參閱 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)。  
  
-   FOREIGN KEY 條件約束可以參考相同資料表中的另一個資料行。 這稱為自我參考。  
  
-   資料行層級 FOREIGN KEY 條件約束的 REFERENCES 子句只能列出一個參考資料行。 這個資料行必須有定義了條件約束的資料行之相同資料類型。  
  
-   資料表層級 FOREIGN KEY 條件約束的 REFERENCES 子句，必須有與條件約束資料行清單中的資料行一樣多的參考資料行。 每個參考資料行的資料類型，也必須與資料行清單中的對應資料行相同。  
  
-   無法指定 CASCADE、 SET NULL 或 SET DEFAULT 如果類型的資料行**時間戳記**是外部索引鍵或被參考索引鍵的一部分。  
  
-   您可以在相互具有參考關聯性的資料表上，組合 CASCADE、SET NULL、SET DEFAULT 和 NO ACTION。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 發現 NO ACTION，它會停止和回復相關的 CASCADE、SET NULL 和 SET DEFAULT 動作。 當 DELETE 陳述式造成 CASCADE、SET NULL、SET DEFAULT 和 NO ACTION 等動作的組合時，在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 檢查任何 NO ACTION 之前，會先套用 CASCADE、SET NULL 及 SET DEFAULT 等動作。  
  
-   在資料表所能包含參考其他資料表的 FOREIGN KEY 條件約束數目，及其他資料表所擁有參考特定資料表的 FOREIGN KEY 條件約束數目上， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 並沒有預先定義的限制。  
  
     不過，FOREIGN KEY 條件約束的實際可用數目，會受到硬體組態及資料庫和應用程式設計的限制。 建議資料表所包含的 FOREIGN KEY 條件約束數目不要超出 253 個，參考資料表的 FOREIGN KEY 條件約束數目也不要超出 253 個。 有效限制多少會隨著應用程式和硬體而不同。 當您設計資料庫和應用程式時，請考量強制執行 FOREIGN KEY 條件約束的成本。  
  
-   暫存資料表不會強制執行 FOREIGN KEY 條件約束。  
  
-   FOREIGN KEY 條件約束只能參考在所參考的資料表中之 PRIMARY KEY 或 UNIQUE 條件約束中的資料行，或在所參考的資料表之 UNIQUE INDEX 中的資料行。  
  
-   如果在 CLR 使用者定義的類型資料行上定義外部索引鍵，類型的實作必須支援二進位順序。 如需詳細資訊，請參閱 [CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
-   加入外部索引鍵關聯性的資料行都必須定義相同的長度和小數位數。  
  
## <a name="default-definitions"></a>DEFAULT 定義  
  
-   資料行只能有一個 DEFAULT 定義。  
  
-   DEFAULT 定義可以包含常數值、函數、SQL 標準 niladic 函數 或 NULL。 下表顯示在 INSERT 陳述式期間，niladic 函數及它們傳回的預設值。  
  
    |SQL-92 niladic 函數|傳回的值|  
    |------------------------------|--------------------|  
    |CURRENT_TIMESTAMP|目前的日期和時間。|  
    |CURRENT_USER|執行插入的使用者名稱。|  
    |SESSION_USER|執行插入的使用者名稱。|  
    |SYSTEM_USER|執行插入的使用者名稱。|  
    |使用者|執行插入的使用者名稱。|  
  
-   *constant_expression*入預設定義無法參考另一個資料行在資料表中，或其他資料表、 檢視或預存程序。  
  
-   無法在具有資料行上建立 DEFAULT 定義**時間戳記**含 IDENTITY 屬性的資料行或資料類型。  
  
-   如果別名資料類型繫結於預設物件，您便無法針對含別名資料類型的資料行來建立 DEFAULT 定義。  
  
## <a name="check-constraints"></a>CHECK 條件約束  
  
-   資料行可以有任意數目的 CHECK 條件約束，且條件可以包括用 AND 和 OR 組合的多個邏輯運算式。 資料行的多個 CHECK 條件約束是依照建立的順序來驗證的。  
  
-   這個搜尋條件必須得出布林運算式，且不能參考其他資料表。  
  
-   資料行層級 CHECK 條件約束只能參考受條件約束限制的資料行，資料表層級的 CHECK 條件約束只能參考相同資料表中的資料行。  
  
     CHECK CONSTRAINTS 和規則會在 INSERT 和 UPDATE 陳述式期間，提供相同的資料驗證功能。  
  
-   當一個或多個資料行有規則和一個或多個 CHECK 條件約束存在時，會評估所有限制。  
  
-   CHECK 條件約束不能定義於**文字**， **ntext**，或**映像**資料行。  
  
## <a name="additional-constraint-information"></a>其他條件約束資訊  
  
-   您不能利用 DROP INDEX 來卸除建立給條件約束的索引；您必須利用 ALTER TABLE 來卸除條件約束。 為條件約束建立且供條件約束使用的索引，可以利用 ALTER INDEX...REBUILD 來重建。 如需詳細資訊，請參閱 [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
-   條件約束名稱必須遵循的規則[識別碼](../../relational-databases/databases/database-identifiers.md)，不同之處在於名稱開頭不能是數字符號 （#）。 如果*constraint_name*是未提供，將系統產生的名稱指派給條件約束。 條件約束名稱會出現在強制違規的任何錯誤訊息中。  
  
-   當在 INSERT、UPDATE 或 DELETE 陳述式中違反條件約束時，陳述式便會結束。 不過，當 SET XACT_ABORT 設為 OFF 時，如果陳述式在明確的交易中，就會繼續處理交易。 當 SET XACT_ABORT 設為 ON 時，就會回復整個交易。 您也可以使用交易定義使用 ROLLBACK TRANSACTION 陳述式，藉由檢查 @@ERROR系統函數。  
  
-   如果 ALLOW_ROW_LOCKS = ON 且 ALLOW_PAGE_LOCK = ON，當您存取索引時，允許資料列、頁面和資料表層級的鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會選擇適當的鎖定，且可以將鎖定從資料列或頁面鎖定擴大到資料表鎖定。 如果 ALLOW_ROW_LOCKS = OFF 且 ALLOW_PAGE_LOCK = OFF，當您存取索引時，只允許資料表層級的鎖定。  
  
-   如果資料表有 FOREIGN KEY 或 CHECK CONSTRAINTS 和觸發程序，就會先評估條件約束的條件，再執行觸發程序。  
  
 針對資料表及其資料行的報表，請使用**sp_help**或**sp_helpconstraint**。 若要重新命名資料表，使用**sp_rename**。 檢視和預存程序相依於資料表的報表，請使用[sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)和[sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)。  
  
## <a name="nullability-rules-within-a-table-definition"></a>資料表定義內的 Null 屬性規則  
 資料行的 Null 屬性決定了資料行的資料是否接受 NULL 值。 NULL 並不是零或空白：NULL 表示沒有任何輸入，或提供了明確的 NULL，但它通常隱含值是未知或不適用。  
  
 當您利用 CREATE TABLE 或 ALTER TABLE 來建立或變更資料表時，資料庫和工作階段設定會影響且可能會覆寫資料行定義所用之資料類型的 Null 屬性。 我們建議您對於非計算資料行，一律將資料行明確定義為 NULL 或 NOT NULL，如果您採用使用者自訂資料類型，建議您允許資料行使用資料類型的預設 Null 屬性。 疏鬆資料行必須永遠允許 NULL。  
  
 當您並未明確指定資料行 Null 屬性時，資料行 Null 屬性會遵照下表所顯示的規則。  
  
|資料行資料類型|規則|  
|----------------------|----------|  
|別名資料型別|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會使用建立資料類型時所指定的 Null 屬性。 若要判斷資料類型的預設 null 屬性，請使用**sp_help**。|  
|CLR 使用者定義型別 (CLR user-defined type)|Null 屬性取決於資料行定義。|  
|系統提供的資料類型|如果系統提供的資料類型只有一個選項，將會優先使用。 **時間戳記**資料類型必須是 NOT NULL。 當利用 SET 將任何工作階段設定設為 ON 時：<br />**ANSI_NULL_DFLT_ON** = ON，指派 NULL。  <br />**ANSI_NULL_DFLT_OFF**不 = ON，指派 NULL。<br /><br /> 當利用 ALTER DATABASE 來設定任何資料庫設定：<br />**ANSI_NULL_DEFAULT_ON** = ON，指派 NULL。  <br />**ANSI_NULL_DEFAULT_OFF**不 = ON，指派 NULL。<br /><br /> 若要檢視 ANSI_NULL_DEFAULT 的資料庫設定，請使用**sys.databases**目錄檢視|  
  
 當工作階段並未設定任何一個 ANSI_NULL_DFLT 選項，而且資料庫設為預設值 (ANSI_NULL_DEFAULT 為 OFF) 時，會指派預設值 NOT NULL。  
  
 如果資料行是計算資料行，它的 Null 屬性一律由 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 來自動決定。 若要了解這種類型的資料行的 null 屬性，使用 使用 COLUMNPROPERTY 函數**AllowsNull**屬性。  
  
> [!NOTE]  
>  SQL Server ODBC 驅動程式和 Microsoft OLE DB Provider for SQL Server 都預設為將 ANSI_NULL_DFLT_ON 設為 ON。 ODBC 和 OLE DB 使用者可以在 ODBC 資料來源中設定這個項目，也可以利用應用程式所設定的連接屬性來設定這個項目。  
  
## <a name="data-compression"></a>資料壓縮  
 系統資料表無法啟用壓縮。 當您建立資料表時，除非另外指定，否則資料壓縮會設定為 NONE。 如果您指定資料分割清單或超出範圍的資料分割，將會產生錯誤。 如需資料壓縮的詳細資訊，請參閱 [資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
 若要評估變更壓縮狀態如何影響資料表、索引或分割區，請使用 [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) 預存程序。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 CREATE TABLE 權限以及用以建立資料表之結構描述的 ALTER 權限。  
  
 如果將 CREATE TABLE 陳述式中的任何資料行定義成 CLR 使用者定義型別，就需要類型的擁有權或它的 REFERENCES 權限。  
  
 如果 CREATE TABLE 陳述式中的任何資料行有相關聯的 XML 結構描述集合，就需要 XML 結構描述集合的擁有權或它的 REFERENCES 權限。  
  
 任何使用者可以在 tempdb 中建立暫存資料表。  
  
## <a name="examples"></a>範例  
  
### <a name="a-create-a-primary-key-constraint-on-a-column"></a>A. 在資料行上建立 PRIMARY KEY 條件約束  
 下列範例會顯示 PRIMARY KEY 條件約束的資料行定義，其中 `EmployeeID` 資料表的 `Employee` 資料行上包含叢集索引。 由於未指定條件約束名稱，因此系統會提供條件約束名稱。  
  
```  
CREATE TABLE dbo.Employee (EmployeeID int  
PRIMARY KEY CLUSTERED);  
```  
  
### <a name="b-using-foreign-key-constraints"></a>B. 使用 FOREIGN KEY 條件約束  
 FOREIGN KEY 條件約束用來參考另一份資料表。 外部索引鍵可以是單一資料行，也可以是多重資料行的索引鍵。 這個範例顯示參考 `SalesOrderHeader` 資料表之 `SalesPerson` 資料表的單一資料行 FOREIGN KEY 條件約束。 單一資料行 FOREIGN KEY 條件約束只需要 REFERENCES 子句。  
  
```  
SalesPersonID int NULL  
REFERENCES SalesPerson(SalesPersonID)  
```  
  
 另外，您也可以明確地使用 FOREIGN KEY 子句，再重新指定資料行屬性。 請注意，兩份資料表中的資料行名稱不必相同。  
  
```  
FOREIGN KEY (SalesPersonID) REFERENCES SalesPerson(SalesPersonID)  
```  
  
 多重資料行索引鍵條件約束會建立成資料表條件約束。 在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中，`SpecialOfferProduct` 資料表包括一個多重資料行 PRIMARY KEY。 下列範例會顯示如何從另一份資料表參考這個索引鍵；明確的條件約束名稱是選擇性的。  
  
```  
CONSTRAINT FK_SpecialOfferProduct_SalesOrderDetail FOREIGN KEY  
 (ProductID, SpecialOfferID)  
REFERENCES SpecialOfferProduct (ProductID, SpecialOfferID)  
```  
  
### <a name="c-using-unique-constraints"></a>C. 使用 UNIQUE 條件約束  
 UNIQUE 條件約束用來強制執行非主索引鍵資料行的唯一性。 下列範例會強制執行「`Name` 資料表的 `Product` 資料行必須是唯一的」這項限制。  
  
```  
Name nvarchar(100) NOT NULL  
UNIQUE NONCLUSTERED  
```  
  
### <a name="d-using-default-definitions"></a>D. 使用 DEFAULT 定義  
 當未提供值時，預設值會提供一個值 (利用 INSERT 和 UPDATE 陳述式)。 例如，[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫可以包括一份查閱資料表，列出公司中員工能夠填入的不同作業。 在描述每項作業的資料行中，當並未明確輸入實際描述時，字元字串預設值可以提供一項描述。  
  
```  
DEFAULT 'New Position - title not formalized yet'  
```  
  
 除了常數之外，DEFAULT 定義也可以包含函數。 請利用下列範例來取得項目的目前日期。  
  
```  
DEFAULT (getdate())  
```  
  
 niladic 函數掃描也可以改進資料完整性。 若要追蹤插入資料列的使用者，請使用 USER 的 niladic 函數。 請勿用括號括住 niladic 函數。  
  
```  
DEFAULT USER  
```  
  
### <a name="e-using-check-constraints"></a>E. 使用 CHECK 條件約束  
 下列範例會顯示輸入 `CreditRating` 資料表 `Vendor` 資料行之值的限制。 這個條件約束不具名。  
  
```  
CHECK (CreditRating >= 1 and CreditRating <= 5)  
```  
  
 這個範例顯示含有在資料表資料行中輸入的字元資料之模式限制的具名條件約束。  
  
```  
CONSTRAINT CK_emp_id CHECK (emp_id LIKE   
'[A-Z][A-Z][A-Z][1-9][0-9][0-9][0-9][0-9][FM]'   
OR emp_id LIKE '[A-Z]-[A-Z][1-9][0-9][0-9][0-9][0-9][FM]')  
```  
  
 這個範例指定值必須在特定清單中，或遵照指定的模式。  
  
```  
CHECK (emp_id IN ('1389', '0736', '0877', '1622', '1756')  
OR emp_id LIKE '99[0-9][0-9]')  
```  
  
### <a name="f-showing-the-complete-table-definition"></a>F. 顯示完整的資料表定義  
 下列範例會顯示含有 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中所建立的 `PurchaseOrderDetail` 資料表之所有條件約束定義的完整資料表定義。 請注意，資料表結構描述會變更為 `dbo`，以執行範例。  
  
```  
CREATE TABLE dbo.PurchaseOrderDetail  
(  
    PurchaseOrderID int NOT NULL  
        REFERENCES Purchasing.PurchaseOrderHeader(PurchaseOrderID),  
    LineNumber smallint NOT NULL,  
    ProductID int NULL   
        REFERENCES Production.Product(ProductID),  
    UnitPrice money NULL,  
    OrderQty smallint NULL,  
    ReceivedQty float NULL,  
    RejectedQty float NULL,  
    DueDate datetime NULL,  
    rowguid uniqueidentifier ROWGUIDCOL  NOT NULL  
        CONSTRAINT DF_PurchaseOrderDetail_rowguid DEFAULT (newid()),  
    ModifiedDate datetime NOT NULL   
        CONSTRAINT DF_PurchaseOrderDetail_ModifiedDate DEFAULT (getdate()),  
    LineTotal  AS ((UnitPrice*OrderQty)),  
    StockedQty  AS ((ReceivedQty-RejectedQty)),  
    CONSTRAINT PK_PurchaseOrderDetail_PurchaseOrderID_LineNumber  
               PRIMARY KEY CLUSTERED (PurchaseOrderID, LineNumber)  
               WITH (IGNORE_DUP_KEY = OFF)  
)   
ON PRIMARY;  
```  
  
### <a name="g-creating-a-table-with-an-xml-column-typed-to-an-xml-schema-collection"></a>G. 建立內含分類到 XML 結構描述集合之 XML 資料行的資料表  
 下列範例會建立一份含有 `xml` 資料行的資料表，且該資料行的類型符合 XML 結構描述集合 `HRResumeSchemaCollection`。 `DOCUMENT`關鍵字指定的每個執行個體`xml`中的資料類型*column_name*可以只包含一個最上層元素。  
  
```  
CREATE TABLE HumanResources.EmployeeResumes   
   (LName nvarchar(25), FName nvarchar(25),   
    Resume xml( DOCUMENT HumanResources.HRResumeSchemaCollection) );  
```  
  
### <a name="h-creating-a-partitioned-table"></a>H. 建立分割區資料表  
 下列範例會建立一個資料分割函數，將資料表或索引分割成四個資料分割。 之後，此範例會建立一個分割區配置來指定分別用來保留這四份分割區的檔案群組。 最後，這個範例會建立一份使用分割區配置的資料表。 這個範例假設這些檔案群組已在資料庫中。  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES (1, 100, 1000) ;  
GO  
  
CREATE PARTITION SCHEME myRangePS1  
    AS PARTITION myRangePF1  
    TO (test1fg, test2fg, test3fg, test4fg) ;  
GO  
  
CREATE TABLE PartitionTable (col1 int, col2 char(10))  
    ON myRangePS1 (col1) ;  
GO  
```  
  
 分割區會以 `col1` 的 `PartitionTable` 資料行值為基礎而以下列方式進行指派。  
  
|檔案群組|test1fg|test2fg|test3fg|test4fg|  
|---------------|-------------|-------------|-------------|-------------|  
|**資料分割**|1|2|3|4|  
|**值**|資料行 1 \<= 1|col1 > 1 AND col1 \<= 100|col1 > 100 AND col1 \<= 1000|col1 > 1000 |  
  
### <a name="i-using-the-uniqueidentifier-data-type-in-a-column"></a>I. 在資料行中使用 uniqueidentifier 資料類型  
 下列範例會建立一份含有 `uniqueidentifier` 資料行的資料表。 這個範例會利用 PRIMARY KEY 條件約束來保護資料表，以免使用者插入重複的值，以及利用 `NEWSEQUENTIALID()` 條件約束中的 `DEFAULT` 函數來提供新資料列的值。 ROWGUIDCOL 屬性會套用到 `uniqueidentifier` 資料行，以便可以使用 $ROWGUID 關鍵字來參考它。  
  
```  
CREATE TABLE dbo.Globally_Unique_Data  
    (guid uniqueidentifier   
        CONSTRAINT Guid_Default DEFAULT   
        NEWSEQUENTIALID() ROWGUIDCOL,  
    Employee_Name varchar(60)  
    CONSTRAINT Guid_PK PRIMARY KEY (guid) );  
```  
  
### <a name="j-using-an-expression-for-a-computed-column"></a>J. 使用計算資料行的運算式  
 下列範例會顯示如何利用 (`(low + high)/2`) 運算式來計算 `myavg` 計算資料行。  
  
```  
CREATE TABLE dbo.mytable   
    ( low int, high int, myavg AS (low + high)/2 ) ;  
```  
  
### <a name="k-creating-a-computed-column-based-on-a-user-defined-type-column"></a>K. 建立以使用者定義類型資料行為基礎的計算資料行  
 下列範例會建立一份資料表，含有定義為使用者定義型別 `utf8string` 的資料行，且假設目前資料庫中已建立了這個類型的組件及這個類型本身。 第二個資料行根據定義`utf8string`，並使用方法`ToString()`的**type(class)** `utf8string`來計算資料行的值。  
  
```  
CREATE TABLE UDTypeTable   
    ( u utf8string, ustr AS u.ToString() PERSISTED ) ;  
```  
  
### <a name="l-using-the-username-function-for-a-computed-column"></a>L. 使用計算資料行的 USER_NAME 函數  
 下列範例會使用 `USER_NAME()` 資料行中的 `myuser_name` 函數。  
  
```  
CREATE TABLE dbo.mylogintable  
    ( date_in datetime, user_id int, myuser_name AS USER_NAME() ) ;  
```  
  
### <a name="m-creating-a-table-that-has-a-filestream-column"></a>M. 建立具有 FILESTREAM 資料行的資料表  
 下列範例會建立一份含有 `FILESTREAM` 資料行 `Photo` 的資料表。 如果資料表具有一個或多個 `FILESTREAM` 資料行，此資料表就必須具有一個 `ROWGUIDCOL` 資料行。  
  
```  
CREATE TABLE dbo.EmployeePhoto  
    (  
    EmployeeId int NOT NULL PRIMARY KEY,  
    ,Photo varbinary(max) FILESTREAM NULL  
    ,MyRowGuidColumn uniqueidentifier NOT NULL ROWGUIDCOL  
        UNIQUE DEFAULT NEWID()  
    );  
```  
  
### <a name="n-creating-a-table-that-uses-row-compression"></a>N. 建立使用資料列壓縮的資料表  
 下列範例會建立一份使用資料列壓縮的資料表。  
  
```  
CREATE TABLE dbo.T1   
(c1 int, c2 nvarchar(200) )  
WITH (DATA_COMPRESSION = ROW);  
```  
  
 如需其他資料壓縮範例，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
### <a name="o-creating-a-table-that-has-sparse-columns-and-a-column-set"></a>O. 建立具有疏鬆資料行與資料行集的資料表  
 下列範例會示範如何建立一份含有疏鬆資料行的資料表，以及一份含有兩個疏鬆資料行與資料行集的資料表。 此範例會使用基本語法。 如需更複雜的範例，請參閱[使用疏鬆資料行](../../relational-databases/tables/use-sparse-columns.md)和[使用資料行集](../../relational-databases/tables/use-column-sets.md)。  
  
 此範例會建立一份含有疏鬆資料行的資料表。  
  
```  
CREATE TABLE dbo.T1  
    (c1 int PRIMARY KEY,  
    c2 varchar(50) SPARSE NULL ) ;  
```  
  
 此範例會建立一份含有兩個疏鬆資料行與一個名為 `CSet` 之資料行集的資料表。  
  
```  
CREATE TABLE T1  
    (c1 int PRIMARY KEY,  
    c2 varchar(50) SPARSE NULL,  
    c3 int SPARSE NULL,  
    CSet XML COLUMN_SET FOR ALL_SPARSE_COLUMNS ) ;  
```  
  
### <a name="p-creating-a-system-versioned-disk-based-temporal-table"></a>P. 建立系統建立版本以磁碟為基礎的時態表  
   
  
**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
 下列範例顯示如何建立時態表連結到新的記錄資料表，以及如何建立連結至現有的記錄資料表的時態表。 請注意，時態表必須啟用，若要啟用系統版本設定資料表定義主索引鍵。 如需範例示範如何新增或移除系統版本設定，在現有的資料表，請參閱中的系統版本設定[範例](../../t-sql/statements/alter-table-transact-sql.md#Example_Top)。 使用案例，請參閱[時態表](../../relational-databases/tables/temporal-tables.md)。  
  
 這個範例會建立新的時態表連結到新的歷程記錄資料表。  
  
```  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)  
WITH (SYSTEM_VERSIONING = ON);  
```  
  
 這個範例會建立新的時態表連結到現有的記錄資料表。  
  
```  
  
--Existing table   
CREATE TABLE Department_History   
(  
    DepartmentNumber char(10) NOT NULL,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 NOT NULL,   
    SysEndTime datetime2 NOT NULL   
);  
--Temporal table  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID INT  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)    
)  
WITH   
    (SYSTEM_VERSIONING = ON   
        (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON )  
    );  
```  
  
### <a name="q-creating-a-system-versioned-memory-optimized-temporal-table"></a>Q. 建立系統建立版本記憶體最佳化時態表  
   
  
**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
 下列範例會示範如何建立系統建立版本記憶體最佳化的時態表連結到新的磁碟為基礎的歷程記錄資料表。  
  
 這個範例會建立新的時態表連結到新的歷程記錄資料表。  
  
```  
CREATE SCHEMA History  
GO  
CREATE TABLE dbo.Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)  
WITH   
    (  
        MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA,  
            SYSTEM_VERSIONING = ON ( HISTORY_TABLE = History.DepartmentHistory )   
    );  
```  
  
 這個範例會建立新的時態表連結到現有的記錄資料表。  
  
```  
  
--Existing table   
CREATE TABLE Department_History   
(  
    DepartmentNumber char(10) NOT NULL,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 NOT NULL,   
    SysEndTime datetime2 NOT NULL   
);  
--Temporal table  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID INT  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)    
)  
WITH   
    (SYSTEM_VERSIONING = ON   
        (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON )  
    );  
```  
  
### <a name="r-creating-a-table-with-encrypted-columns"></a>R. 建立具有加密資料行的資料表  
 下列範例會建立具有兩個加密的資料行的資料表。 如需詳細資訊，請參閱[永遠加密 &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。  
  
```  
CREATE TABLE Customers (  
    CustName nvarchar(60)   
        ENCRYPTED WITH   
            (  
             COLUMN_ENCRYPTION_KEY = MyCEK,  
             ENCRYPTION_TYPE = RANDOMIZED,  
             ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'  
            ),   
    SSN varchar(11) COLLATE  Latin1_General_BIN2  
        ENCRYPTED WITH   
            (  
             COLUMN_ENCRYPTION_KEY = MyCEK,  
             ENCRYPTION_TYPE = DETERMINISTIC ,  
             ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'  
            ),   
    Age int NULL  
);  
```

### <a name="s-create-an-inline-filtered-index"></a>S. 建立內嵌篩選的索引 
使用內嵌篩選索引中建立資料表。
  
  ```
  CREATE TABLE t1 
 (
      c1 int,
      index IX1  (c1) WHERE c1 > 0   
 )
GO
 ```
 
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [COLUMNPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DROP INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [DROP TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helpconstraint &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpconstraint-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_spaceused &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
  
  



