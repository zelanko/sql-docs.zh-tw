---
title: "ALTER TABLE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WAIT_AT_LOW_PRIORITY
- ABORT_AFTER_WAIT
- ABORT_AFTER_WAIT_TSQL
- ALTER_TABLE_TSQL
- ALTER TABLE
- WAIT_AT_LOW_PRIORITY_TSQL
- ALTER_COLUMN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- columns [SQL Server], resizing
- changing column size
- MAXDOP index option, ALTER TABLE statement
- table modifications [SQL Server], ALTER TABLE
- ALTER TABLE statement
- modifying tables
- partitioned tables [SQL Server], lock escalation
- resizing columns
- removing columns
- switching partitions
- reassigning partitions
- removing constraints
- triggers [SQL Server], disabling
- columns [SQL Server], adding
- LOCK_ESCALATION option of ALTER TABLE
- constraints [SQL Server], deleting
- constraints [SQL Server], disabling
- triggers [SQL Server], enabling
- re-enabling constraints
- index modifications [SQL Server]
- disabling constraints
- columns [SQL Server], removing
- max degree of parallelism option
- locking [SQL Server], tables
- ONLINE option
- disabling triggers
- constraints [SQL Server], adding
- deleting constraints
- adding constraints
- adding columns
- SWITCH partitions
- partitioned tables [SQL Server], switching
- lock escalation [SQL Server], option of ALTER TABLE
- constraints [SQL Server], enabling
- dropping constraints
- dropping columns
- table changes [SQL Server]
ms.assetid: f1745145-182d-4301-a334-18f799d361d1
caps.latest.revision: 281
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7cee79406283aa3b75d41b968370f490cb454ea5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-table-transact-sql"></a>ALTER TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  您可以利用改變、加入或卸除資料行與條件約束、重新指派和重建分割區，或是停用或啟用條件約束與觸發程序等方式來修改資料表定義。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name   
{   
    ALTER COLUMN column_name   
    {   
        [ type_schema_name. ] type_name   
            [ (   
                {   
                   precision [ , scale ]   
                 | max   
                 | xml_schema_collection   
                }   
            ) ]   
        [ COLLATE collation_name ]   
        [ NULL | NOT NULL ] [ SPARSE ]  
      | { ADD | DROP }   
          { ROWGUIDCOL | PERSISTED | NOT FOR REPLICATION | SPARSE | HIDDEN }  
      | { ADD | DROP } MASKED [ WITH ( FUNCTION = ' mask_function ') ]  
    }   
    [ WITH ( ONLINE = ON | OFF ) ]  
    | [ WITH { CHECK | NOCHECK } ]  
  
    | ADD   
    {   
        <column_definition>  
      | <computed_column_definition>  
      | <table_constraint>   
      | <column_set_definition>   
    } [ ,...n ]  
      | [ system_start_time_column_name datetime2 GENERATED ALWAYS AS ROW START   
                   [ HIDDEN ] [ NOT NULL ] [ CONSTRAINT constraint_name ] 
           DEFAULT constant_expression [WITH VALUES] ,  
            system_end_time_column_name datetime2 GENERATED ALWAYS AS ROW END   
                   [ HIDDEN ] [ NOT NULL ]  [ CONSTRAINT constraint_name ] 
           DEFAULT constant_expression [WITH VALUES] ,  
         ]  
       PERIOD FOR SYSTEM_TIME ( system_start_time_column_name, system_end_time_column_name )  
    | DROP   
     [ {  
         [ CONSTRAINT ]  [ IF EXISTS ]  
         {   
              constraint_name   
              [ WITH   
               ( <drop_clustered_constraint_option> [ ,...n ] )   
              ]   
          } [ ,...n ]  
          | COLUMN  [ IF EXISTS ]  
          {  
              column_name   
          } [ ,...n ]  
          | PERIOD FOR SYSTEM_TIME  
     } [ ,...n ]  
    | [ WITH { CHECK | NOCHECK } ] { CHECK | NOCHECK } CONSTRAINT   
        { ALL | constraint_name [ ,...n ] }   
  
    | { ENABLE | DISABLE } TRIGGER   
        { ALL | trigger_name [ ,...n ] }  
  
    | { ENABLE | DISABLE } CHANGE_TRACKING   
        [ WITH ( TRACK_COLUMNS_UPDATED = { ON | OFF } ) ]  
  
    | SWITCH [ PARTITION source_partition_number_expression ]  
        TO target_table   
        [ PARTITION target_partition_number_expression ]  
        [ WITH ( <low_lock_priority_wait> ) ]  
    | SET   
        (  
            [ FILESTREAM_ON =   
                { partition_scheme_name | filegroup | "default" | "NULL" } ]  
            | SYSTEM_VERSIONING =   
                  {   
                      OFF   
                  | ON   
                      [ ( HISTORY_TABLE = schema_name . history_table_name   
                          [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] 
                          [, HISTORY_RETENTION_PERIOD = 
                          { 
                               INFINITE | number {DAY | DAYS | WEEK | WEEKS 
                 | MONTH | MONTHS | YEAR | YEARS } 
                          } 
                          ]  
                        )  
                      ]  
                  }  
          )  
    | REBUILD   
      [ [PARTITION = ALL]  
        [ WITH ( <rebuild_option> [ ,...n ] ) ]   
      | [ PARTITION = partition_number   
           [ WITH ( <single_partition_rebuild_option> [ ,...n ] ) ]  
        ]  
      ]  
  
    | <table_option>  
  
    | <filetable_option>  
  
    | <stretch_configuration>  
  
}  
[ ; ]  
  
-- ALTER TABLE options  
  
<column_set_definition> ::=   
    column_set_name XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
  
<drop_clustered_constraint_option> ::=    
    {   
        MAXDOP = max_degree_of_parallelism  
      | ONLINE = { ON | OFF }  
      | MOVE TO   
         { partition_scheme_name ( column_name ) | filegroup | "default" }  
    }  
<table_option> ::=  
    {  
        SET ( LOCK_ESCALATION = { AUTO | TABLE | DISABLE } )  
    }  
  
<filetable_option> ::=  
    {  
       [ { ENABLE | DISABLE } FILETABLE_NAMESPACE ]  
       [ SET ( FILETABLE_DIRECTORY = directory_name ) ]  
    }  
  
<stretch_configuration> ::=  
    {  
      SET (  
        REMOTE_DATA_ARCHIVE   
        {  
            = ON (  <table_stretch_options>  )  
          | = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED )  
          | ( <table_stretch_options> [, ...n] )  
        }  
            )  
    }  
  
<table_stretch_options> ::=  
    {  
     [ FILTER_PREDICATE = { null | table_predicate_function } , ]  
       MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED }  
    }  
  
<single_partition_rebuild__option> ::=  
{  
      SORT_IN_TEMPDB = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE} }  
    | ONLINE = { ON [( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ], 
        ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )   
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER TABLE [ database_name . [schema_name ] . | schema_name. ] source_table_name   
{  
    ALTER COLUMN column_name  
        {   
            type_name [ ( precision [ , scale ] ) ]   
            [ COLLATE Windows_collation_name ]   
            [ NULL | NOT NULL ]   
        }  
    | ADD { <column_definition> | <column_constraint> FOR column_name} [ ,...n ]  
    | DROP { COLUMN column_name | [CONSTRAINT] constraint_name } [ ,...n ]  
    | REBUILD {  
            [ PARTITION = ALL [ WITH ( <rebuild_option> ) ] ] 
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_option> ] ]
      } 
    | { SPLIT | MERGE } RANGE (boundary_value)  
    | SWITCH [ PARTITION source_partition_number  
        TO target_table_name [ PARTITION target_partition_number ]  
}  
[;]  
  
<column_definition>::=  
{  
    column_name  
    type_name [ ( precision [ , scale ] ) ]   
    [ <column_constraint> ]  
    [ COLLATE Windows_collation_name ]  
    [ NULL | NOT NULL ]  
}  
  
<column_constraint>::=  
    [ CONSTRAINT constraint_name ] DEFAULT constant_expression  

<rebuild_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]   
}

<single_partition_rebuild_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
}  
```    

   
## <a name="arguments"></a>引數  
 *database_name*  
 這是建立資料表的資料庫名稱。  
  
 *schema_name*  
 這是資料表所屬的結構描述名稱。  
  
 *table_name*  
 這是要變更的資料表名稱。 如果資料表不在目前資料庫中，或未包含在目前使用者擁有的結構描述內，則必須明確指定該資料庫和結構描述。  
  
 ALTER COLUMN  
 指定將要變更或改變的具名資料行。  
  
 修改過的資料行不得為下列任何一項：  
  
-   具有的資料行**時間戳記**資料型別。  
  
-   資料表的 ROWGUIDCOL。  
  
-   計算資料行，或用於計算資料行。  
  
-   除非資料行是由 CREATE STATISTICS 陳述式所產生的統計資料中使用**varchar**， **nvarchar**，或**varbinary**資料類型，未變更的資料類型，以及新的大小是等於或大於舊大小，或如果資料行已從非 null 變為 null。 首先，利用 DROP STATISTICS 陳述式移除統計資料。 ALTER COLUMN 會自動卸除查詢最佳化工具自動產生的統計資料。  
  
-   在 PRIMARY KEY 或 [FOREIGN KEY] REFERENCES 條件約束中使用。  
  
-   在 CHECK 或 UNIQUE 條件約束中使用。 不過，允許變更用於 CHECK 或 UNIQUE 條件約束的可變長度資料行的長度。  
  
-   與預設定義相關聯。 不過，如果資料類型沒有變更，則會變更資料行的長度、有效位數或小數位數。  
  
資料型別**文字**， **ntext**和**映像**可以變更資料行，只會以下列方式：  
  
    -   **文字**至**varchar （max)**， **nvarchar （max)**，或**xml**  
  
    -   **ntext**至**varchar （max)**， **nvarchar （max)**，或**xml**  
  
    -   **映像**至**varbinary （max)**  
  
某些資料類型變更可能會使資料變更。 例如，變更**nchar**或**nvarchar**資料行**char**或**varchar**可能會造成擴充字元的轉換。 如需詳細資訊，請參閱 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)。 減少資料行的有效位數或小數位數，可能會使資料截斷。  
  
     The data type of a column of a partitioned table cannot be changed.  
  
 無法變更索引中包含的資料行的資料類型，除非資料行是**varchar**， **nvarchar**，或**varbinary**資料型別，且新大小等於或大於比舊的大小。  
  
 無法變更主索引鍵條件約束中包含的資料行**NOT NULL**至**NULL**。  
  
 如果要修改資料行已加密加密搭配使用，您可以變更資料類型相容的資料類型 （例如 BIGINT 至 INT)，但是您無法變更任何加密設定。  
  
 *column_name*  
 要改變、加入或卸除的資料欄名稱。 *column_name*最多可有 128 個字元。 新資料行， *column_name*以建立資料行可以省略**時間戳記**資料型別。 名稱**時間戳記**如果沒有則會使用*column_name*指定**時間戳記**資料類型資料行。  
  
 [ *type_schema_name***。** ] *type_name*  
 所改變之資料行的新資料類型，或是所加入之資料行的資料類型。 *type_name*不能指定為資料分割資料表的現有資料行。 *type_name*可以是下列其中一個：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型。  
  
-   基於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型的別名資料類型。 別名資料類型是利用 CREATE TYPE 陳述式建立的，在這之後才能在資料表定義中使用它們。  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 使用者定義型別及其所屬的結構描述。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 使用者定義型別必須先以 CREATE TYPE 陳述式加以建立，才可在資料表定義中使用。  
  
以下是準則*type_name*的改變資料行：  
  
-   前一個資料類型必須可隱含轉換至新資料類型。  
  
-   *type_name*不可**時間戳記**。  
  
-   ALTER COLUMN 的 ANSI_NULL 預設值一律開啟；如果未指定，資料行可為 Null。  
  
-   ALTER COLUMN 的 ANSI_PADDING 填補一律為 ON。  
  
-   如果已修改的資料行是識別資料行， *new_data_type*必須是可支援 identity 屬性的資料類型。  
  
-   SET ARITHABORT 的目前設定會被忽略。 如果 ARITHABORT 設為 ON，ALTER TABLE 就會執行作業。  
  
> [!NOTE]  
>  如果未指定 COLLATE 子句，變更資料行的資料類型會使資料庫的預設定序發生定序變更。  
  
 *有效位數*  
 這是指定之資料類型的有效位數。 如需有關有效位數值的詳細資訊，請參閱[有效位數、 小數位數及長度 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 *scale*  
 這是指定資料類型的小數位數。 如需有關有效小數位數值的詳細資訊，請參閱[有效位數、 小數位數及長度 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 **最大值**  
 僅適用於**varchar**， **nvarchar**，和**varbinary**資料類型來儲存 2 ^31-1 位元組的字元、 二進位資料，及 Unicode 資料。  
  
 *xml_schema_collection*  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 僅適用於**xml**將 XML 結構描述與型別產生關聯的資料類型。 之前輸入**xml**結構描述集合的資料行，結構描述集合必須先建立資料庫中使用[CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)。  
  
COLLATE \< *sys.databases* > 指定改變資料行的新定序。 若未指定，就會將資料庫的預設定序指派給資料行。 定序名稱可以是 Windows 定序名稱或 SQL 定序名稱。 如需清單和詳細資訊，請參閱[Windows 定序名稱 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)和[SQL Server 定序名稱 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 COLLATE 子句可以用來變更的資料行的定序**char**， **varchar**， **nchar**，和**nvarchar**資料型別。 若要變更使用者定義之別名資料類型資料行的定序，您必須執行個別的 ALTER TABLE 陳述式，將資料行變更為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型，並變更它的定序，然後再將資料行改回別名資料類型。  
  
 如果存在下列一個或多個條件，ALTER COLUMN 不能有定序變更：  
  
-   如果 CHECK 條件約束、FOREIGN KEY 條件約束或計算資料行參考變更的資料行。  
  
-   如果在資料行上建立任何索引、統計資料或全文檢索索引。 如果資料行定序變更了，在變更的資料行上自動建立的統計資料就會卸除。  
  
-   如果結構描述繫結檢視或函數參考資料行。  
  
 如需詳細資訊，請參閱 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)。  
  
NULL | NOT NULL  
 指定資料行是否接受 Null 值。 只有在不允許 Null 值的資料行指定了預設值，或資料表是空的情況下，才能利用 ALTER TABLE 新增這些資料行。 只有在也指定了 PERSISTED 時，計算資料行才能指定 NOT NULL。 如果新資料行允許 Null 值，且未指定預設值，資料表每個資料列的新資料行都會包含 Null 值。 如果新資料行允許 Null 值，且加入了預設定義，就可以利用 WITH VALUES，將預設值儲存在資料表每個現有資料列的新資料行中。  
  
 如果新資料行不允許 Null 值，且資料表不是空的，則必須利用新資料行新增 DEFAULT 定義，則新資料行會自動將預設值載入每個現有資料列中的新資料行。  
  
 您可以在 ALTER COLUMN 中指定 NULL，來強制 NOT NULL 資料行允許 NULL 值 (但不包括 PRIMARY KEY 條件約束中的資料行)。 只有在資料行沒有包含 Null 值的情況下，才能在 ALTER COLUMN 中指定 NOT NULL。 必須先將 Null 值更新為某些值，才能允許 ALTER COLUMN NOT NULL，例如：  
  
```  
UPDATE MyTable SET NullCol = N'some_value' WHERE NullCol IS NULL;  
ALTER TABLE MyTable ALTER COLUMN NullCOl NVARCHAR(20) NOT NULL;  
```  
  
 當您建立或改變一份含有 CREATE TABLE 或 ALTER TABLE 陳述式的資料表時，資料庫和工作階段設定會影響且可能會覆寫資料行定義中使用之資料類型的 Null 屬性。 我們建議您一定要針對非計算資料行，明確將資料行定義為 NULL 或 NOT NULL。  
  
 如果您加入一個具有使用者定義資料類型的資料行，我們建議您最好使用與此使用者定義資料類型相同的 Null 屬性來定義此資料行，並為此資料行指定預設值。 如需詳細資訊，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)。  
  
> [!NOTE]  
>  如果 NULL 或 NOT NULL 指定改變資料行*new_data_type* [(*精確度*[，*標尺*])] 也必須指定。 如果資料類型、有效位數及小數位數沒有變更，請指定目前的資料行值。  
  
 [ {ADD | DROP} ROWGUIDCOL ]  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定將 ROWGUIDCOL 屬性加入至指定的資料行，或從指定的資料行卸除該屬性。 ROWGUIDCOL 指出資料行是資料列 GUID 資料行。 只有一個**uniqueidentifier**每個資料表的資料行可以指定為 ROWGUIDCOL 資料行，而且您可以只指派 ROWGUIDCOL 屬性**uniqueidentifier**資料行。 不能將 ROWGUIDCOL 指派給使用者定義資料類型的資料行。  
  
 ROWGUIDCOL 不強制使用儲存在資料行中之值的唯一性，且不針對插入資料表中的新資料列自動產生值。 若要產生每個資料行的唯一值，請在 INSERT 陳述式上使用 NEWID 函數，或將 NEWID 函數指定為資料行的預設值。  
  
 [ {ADD | DROP} PERSISTED ]  
 指定將 PERSISTED 屬性加入至指定的資料行，或從指定的資料行卸除該屬性。 該資料行必須是一個利用具決定性運算式定義的計算資料行。 就指定為 PERSISTED 的資料行而言，當計算資料行相依的任何其他資料行更新時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 實際上會將計算值儲存在資料表並將值更新。 將計算資料行標示為 PERSISTED，就可以在定義於具決定性 (但不是精確) 運算式上的計算資料行上建立索引。 如需詳細資訊，請參閱 [計算資料行的索引](../../relational-databases/indexes/indexes-on-computed-columns.md)。  
  
 當做分割區資料表之分割區資料行的任何計算資料行，都必須明確標示為 PERSISTED。  
  
 DROP NOT FOR REPLICATION  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定當複寫代理程式執行插入作業時，識別欄位中的值會累加。 可以指定這個子句，只有當*column_name*是識別資料行。  
  
 SPARSE  
 指出此資料行是疏鬆資料行。 疏鬆資料行的儲存體會針對 Null 值最佳化。 疏鬆資料行無法指定為 NOT NULL。 將資料行從疏鬆轉換成非疏鬆 (或相反) 會在命令執行期間疏鬆鎖定資料表。 您可能必須使用 REBUILD 子句來回收任何節省的空間。 如需其他限制和疏鬆資料行的詳細資訊，請參閱[使用疏鬆資料行](../../relational-databases/tables/use-sparse-columns.md)。  
  
 新增遮罩與 (函式 = ' *mask_function* ')  
 **適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定動態資料遮罩。 *mask_function*的遮罩函數，以適當的參數名稱。 有三個函式：  
  
-   default （)  
-   email()  
-   partial()  
-   random()  
  
 若要卸除遮罩，請使用`DROP MASKED`。 函式參數，請參閱[動態資料遮罩](../../relational-databases/security/dynamic-data-masking.md)。  
  
使用 (ONLINE = ON |OFF)\<適用於改變資料行 >  
 **適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 資料表仍可使用時，允許執行多個改變資料行動作。 預設是 OFF。 可線上針對資料類型、資料行長度或有效位數、Null 屬性、疏鬆度和定序來改變資料行。  
  
 線上改變資料行可讓使用者建立和自動統計資料於 ALTER COLUMN 作業期間參考變更資料行。 這可讓查詢如往常般執行。 在作業結束時會卸除參考資料行的自動統計，使用者建立的統計資料亦同時失效。 作業完成之後，使用者必須手動更新使用者產生的統計資料。 如果資料行是任何統計資料或索引的篩選運算式的一部分，您無法執行改變資料行作業。  
  
-   雖然線上改變資料行的作業正在執行，但可能與資料行有相依性之所有作業(索引、檢視等)會因適當的錯誤訊息而封鎖或失敗。 這確保線上改變資料行不會因作業執行時導入的相依性之故而失敗。  
  
-   當非叢集索引參考資料行時，便不支援改變資料行以線上作業形式從 NOT NULL 變為 NULL。  
  
-   當檢查條件約束參考資料行，以及改變作業限制資料行的有效位數 (數值或日期時間) 時，便不支援線上改變。  
  
-   **Low_priority_lock_wait**選項不能與線上改變資料行。  
  
-   改變資料行... ADD/DROP PERSISTED 不支援線上改變資料行。  
  
-   改變資料行... 加入/卸除 ROWGUIDCOL/不針對複寫不會受到線上改變資料行。  
  
-   已啟用變更追蹤，或是屬於合併式複寫發行者之線上改變資料行不支援改變資料表。  
  
-   線上改變資料行不支援改變自或改變成 CLR 資料類型。  
  
-   線上改變資料行不支援改變成具有不同於目前結構描述集合的 XML 資料類型。  
  
-   線上改變資料行不會減少針對何時可以更改資料行之限制。 索引及統計等之參考資料可能會導致改變失敗。  
  
-   線上改變資料行不支援同時修改多個資料行。  
  
-   線上改變資料行已系統版本設定時態表時沒有作用。 無論針對 ONLINE 選項指定何值，皆不會將 ALTER 資料行執行為線上。  
  
線上改變資料行具有與線上索引重建類似的需求、限制和功能。 這包括：  
  
-   當資料表包含舊版的 LOB 或 filestream 資料行或資料表具有資料行存放區索引時，不支援線上索引重建。 相同的限制適用於線上改變資料行。  
  
-   與原始資料行和新建立的隱藏資料行相比較，要改變現有的資料行需要兩倍的空間配置。  
  
-   改變資料行線上作業期間的鎖定策略是遵循用於線上索引建立相同的鎖定模式。  
  
WITH CHECK | WITH NOCHECK  
 指定是否要依照新加入或重新啟用的 FOREIGN KEY 或 CHECK 條件約束來驗證資料表中的資料。 如果未指定，則假設 WITH CHECK 為新條件約束，並假設 WITH NOCHECK 為重新啟用的條件約束。  
  
 如果您不要依照現有的資料來確認新的 CHECK 或 FOREIGN KEY 條件約束，請使用 WITH NOCHECK。 除了極少數的狀況外，我們建議您不要這麼做。 在以後的所有資料更新中將會評估新條件約束。 新增條件約束時，如果 WITH NOCHECK 抑制任何強制違規，當未來的更新作業更新含有不符合該條件約束的資料列時，這些強制違規可能會使這些更新作業失敗。  
  
 查詢最佳化工具不考量定義為 WITH NOCHECK 的條件約束。 這類條件約束將予忽略，直到使用 `ALTER TABLE table WITH CHECK CHECK CONSTRAINT ALL` 重新啟用為止。  
  
 ADD  
 指定，會新增一或多個資料行定義、 計算資料行定義或資料表條件約束，或系統將會使用系統版本設定的資料行。  
  
 PERIOD FOR SYSTEM_TIME （system_start_time_column_name、 system_end_time_column_name）  
 **適用於**:[!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定的名稱，系統會記錄的有效期間使用的資料行。 您可以指定現有的資料行，或建立新的資料行，導致 ADD PERIOD FOR SYSTEM_TIME 引數的一部分。 資料行必須使用 datetime2 的資料類型，而且必須定義為 NOT NULL。 如果 period 資料行定義為 NULL 時，會擲回錯誤。 您可以定義[column_constraint &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-table-column-constraint-transact-sql.md)及/或[指定預設資料行值](../../relational-databases/tables/specify-default-values-for-columns.md)system_start_time 和 system_end_time 資料行。 請參閱範例 A 中的[系統版本設定](#system_versioning)範例示範如何使用預設值為 system_end_time 資料行下方。  
  
 設定 SYSTEM_VERSIONING 引數搭配使用這個引數，若要啟用現有的資料表上的系統版本設定。 如需詳細資訊，請參閱[時態表](../../relational-databases/tables/temporal-tables.md)和[開始使用 Azure SQL Database 中的時態表](https://azure.microsoft.com/documentation/articles/sql-database-temporal-tables/)。  
  
 從[!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)]，使用者將無法使用的一或兩個期間資料行標記**隱藏**隱含地隱藏這些資料行的旗標，**選取\*FROM**  *\<資料表 >*不會傳回這些資料行的值。 根據預設，將不會隱藏期間資料行。 才能加以使用，隱藏的資料行必須明確包含在所有查詢直接參考時態表中。  
  
 DROP  
 指定，則會卸除一個或多個資料行定義、 計算資料行定義或資料表條件約束，或卸除，系統會使用對系統版本設定的資料行規格。  
  
 條件約束*constraint_name*  
 指定*constraint_name*從資料表中移除。 可以列出多個條件約束。  
  
 使用者定義或系統提供的名稱條件約束可由查詢**sys.check_constraint**， **sys.default_constraints**， **sys.key_constraints**，和**sys.foreign_keys**目錄檢視。  
  
 如果 XML 索引存在於資料表上，則不能卸除 PRIMARY KEY 條件約束。  
  
 資料行*column_name*  
 指定*constraint_name*或*column_name*從資料表中移除。 可以列出多個資料行。  
  
 當資料行符合下列條件時，則無法將它卸除：  
  
-   用於索引。  
  
-   用於 CHECK、FOREIGN KEY、UNIQUE 或 PRIMARY KEY 條件約束。  
  
-   與利用 DEFAULT 關鍵字定義的預設值相關聯，或者繫結到預設物件。  
  
-   繫結至規則。  
  
> [!NOTE]  
>  卸除資料行不會回收資料行的磁碟空間。 當資料表的資料列大小接近或已超出限制時，您可能需要回收卸除之資料行的磁碟空間。 在資料表上建立叢集的索引，或藉由重建現有的叢集的索引來回收空間[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)。 如需影響的卸除 LOB 資料類型的資訊，請參閱此[CSS 部落格文章](http://blogs.msdn.com/b/psssql/archive/2012/12/03/how-it-works-gotcha-varchar-max-caused-my-queries-to-be-slower.aspx)。  
  
 導致 PERIOD FOR SYSTEM_TIME  
 **適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 卸除，系統會使用對系統版本設定的資料行規格。  
  
 與\<drop_clustered_constraint_option >  
 指定設定一個或多個卸除叢集條件約束選項。  
  
 MAXDOP = *max_degree_of_parallelism*  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 覆寫**的最大平行處理原則程度**組態選項，只會針對作業持續時間。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。  
  
 請利用 MAXDOP 選項來限制執行平行計畫所用的處理器數目。 最大值是 64 個處理器。  
  
 *max_degree_of_parallelism*可以是下列值之一：  
  
 1  
 隱藏平行計畫的產生。  
  
 \>1  
 將平行索引作業所用的最大處理器數目限制為指定的數目。  
  
 0 (預設值)  
 根據目前的系統工作負載，使用實際數目或比實際數目更少的處理器。  
  
 如需詳細資訊，請參閱 [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有版本都無法使用平行索引作業。 如需詳細資訊，請參閱[版本和支援 SQL Server 2016 的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 線上 **=**  {ON |**OFF** }\<在套用至 drop_clustered_constraint_option >  
 指定在索引作業期間，查詢和資料修改是否能夠使用基礎資料表和相關聯的索引。 預設值為 OFF。 REBUILD 可以執行為 ONLINE 作業。  
  
 ON  
 索引作業持續期間不會保留長期資料表鎖定。 在索引作業的主要階段期間，來源資料表上只保留意圖共用 (IS) 鎖定。 這使得基礎資料表和索引的查詢或更新能夠繼續運作。 在作業開始時，只會在一段很短的時間內，保留來源物件的共用 (S) 鎖定。 在作業結束時，如果建立非叢集索引的話，便會短時間取得來源的 S (共用) 鎖定；在線上建立或卸除叢集索引時，以及重建叢集或非叢集索引時，會取得 SCH-M (結構描述修改) 鎖定。 建立本機暫存資料表的索引時，ONLINE 不可設為 ON。 只可使用單一執行緒的堆積重建作業。  
  
 若要執行的 DDL**交換器**或線上索引重建，所有使用中封鎖特定資料表上執行的交易必須完成。 執行時，**交換器**或重建作業會阻止新交易啟動可能會大幅影響工作負載輸送量並暫時延遲對基礎資料表的存取。  
  
 OFF  
 在索引作業期間會套用資料表鎖定。 建立、重建或卸除叢集索引的離線索引作業，或重建或卸除非叢集索引的離線索引作業，會取得資料表的結構描述修改 (Sch-M) 鎖定。 這可防止所有使用者在作業持續期間存取基礎資料表。 建立非叢集索引的離線索引作業會取得資料表的共用 (S) 鎖定。 這可避免對基礎資料表進行更新，但仍可執行讀取作業，如 SELECT 陳述式。 允許多執行緒的堆積重建作業。  
  
 如需詳細資訊，請參閱[線上索引作業的運作方式](../../relational-databases/indexes/how-online-index-operations-work.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的所有版本都無法使用線上索引作業。 如需詳細資訊，請參閱[版本和支援 SQL Server 2016 的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 MOVE TO { *partition_scheme_name***(***column_name* [1**，** ... *n* ] **)** | *檔案群組* | **"**預設**"** }  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定目前在叢集索引分葉層級中之資料列所要移往的位置。 資料表會移至新位置。 此選項只適用於建立叢集索引的條件約束。  
  
> [!NOTE]  
>  在此內容中，default 不是關鍵字。 它是預設檔案群組的識別碼，必須加以分隔，如 MOVE TO **"**預設**"**或 MOVE TO **[**預設**]**。 如果**"**預設**"**指定，將 QUOTED_IDENTIFIER 選項必須是 ON，目前工作階段。 這是預設值。 如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
 { CHECK | NOCHECK } CONSTRAINT  
 指定*constraint_name*為啟用或停用。 這個選項只能搭配 FOREIGN KEY 和 CHECK 條件約束使用。 當指定 NOCHECK 時，會停用條件約束，且不會依照條件約束條件來驗證未來資料行的插入或更新作業。 不能停用 DEFAULT、PRIMARY KEY 及 UNIQUE 條件約束。  
  
 ALL  
 指定利用 NOCHECK 選項停用所有條件約束，或利用 CHECK 選項啟用所有條件約束。  
  
 { ENABLE | DISABLE } TRIGGER  
 指定*trigger_name*為啟用或停用。 當停用觸發程序時，仍會針對資料表定義觸發程序；不過，當依照資料表執行 INSERT、UPDATE 或 DELETE 陳述式時，在重新啟用觸發程序之前，並不會執行觸發程序中的動作。  
  
 ALL  
 指定資料表中的所有觸發程序為已啟用或已停用。  
  
 *trigger_name*  
 指定要停用或啟用的觸發程序名稱。  
  
 { ENABLE | DISABLE } CHANGE_TRACKING  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定資料表是要啟用還是停用變更追蹤。 預設會停用變更追蹤。  
  
 只有當資料庫啟用了變更追蹤時，才能使用此選項。 如需詳細資訊，請參閱 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。  
  
 若要啟用變更追蹤，資料表必須具有主索引鍵。  
  
 與**(** TRACK_COLUMNS_UPDATED  **=**  {ON |**OFF** } **)**  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 是否追蹤哪些啟用變更追蹤的資料行已更新。 預設值是 OFF。  
  
 切換 [PARTITION *source_partition_number_expression* ] TO [ *schema_name***。** ] *target_table* [資料分割*target_partition_number_expression* ]  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 利用下列其中一種方式切換資料區塊：  
  
-   將資料表的所有資料當做分割區重新指派給已存在的分割區資料表。  
  
-   將分割區從某一分割區資料表切換到另一分割區資料表。  
  
-   將分割區資料表之一個分割區中的所有資料，重新指派給現有的非分割區資料表。  
  
如果*資料表*是資料分割的資料表， *source_partition_number_expression*必須指定。 如果*target_table*已分割， *target_partition_number_expression*必須指定。 如果將做為分割區之資料表的資料重新指派給已存在的分割區資料表，或將分割區從某一分割區資料表切換到另一分割區資料表，則目標分割區必須存在，且它必須是空的。  
  
 如果重新指派一個分割區的資料來形成單一資料表，則目標資料表必須已經建立，且它必須是空的。 來源資料表或分割區和目標資料表或分割區必須位於相同的檔案群組。 相對應的索引或索引分割區區也必須位於相同的檔案群組。 切換分割區還有許多其他限制。 *資料表*和*target_table*不能相同。 *target_table*可以是多重部分識別碼。  
  
 *source_partition_number_expression*和*target_partition_number_expression*是可以參考變數和函數的常數運算式。 其中包括使用者定義型別變數與使用者定義函數。 其不可參考 [!INCLUDE[tsql](../../includes/tsql-md.md)] 運算式。  
  
 資料分割的資料表與索引藉行為類似資料分割堆積：  
  
-   主索引鍵必須包含資料分割索引鍵。  
  
-   唯一的索引必須包含資料分割索引鍵。  請注意，包括現有的唯一索引的資料分割索引鍵可以變更唯一性。  
  
-   若要切換資料分割，所有的非叢集索引必須包含資料分割索引鍵。  
  
如**交換器**限制時使用複寫，請參閱[複寫 Partitioned Tables and Indexes](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。  
  
 非叢集資料行存放區索引的內建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 ctp1 而言，和 SQL database V12 版是唯讀的格式之前。 可以執行任何資料分割作業之前，必須重建非叢集資料行存放區索引成目前的格式 （這是可更新）。  
  
 設定**(** FILESTREAM_ON = { *partition_scheme_name* | *filestream_filegroup_name* |         **"**預設**"** | **"**NULL**"** }**)**  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 |  
  
 指定 FILESTREAM 資料存放的位置。  
  
 具有 SET FILESTREAM_ON 子句的 ALTER TABLE 只有在資料表沒有任何 FILESTREAM 資料行時才會成功。 您可以使用第二個 ALTER TABLE 陳述式來加入 FILESTREAM 資料行。  
  
 如果*partition_scheme_name*指定的規則[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)套用。 資料表應該已經針對資料列資料進行分割區，且其分割區配置所使用的分割區函數和資料行必須與 FILESTREAM 分割區配置相同。  
  
 *filestream_filegroup_name*指定 FILESTREAM 檔案群組的名稱。 此檔案群組必須有一個定義檔案的檔案群組使用[CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md)或[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)陳述式或發生錯誤，就會引發。  
  
 **「**預設**"** DEFAULT 屬性集指定 FILESTREAM 檔案群組。 如果沒有任何 FILESTREAM 檔案群組，就會引發錯誤。  
  
 **「**NULL**"**指定資料表的 FILESTREAM 檔案群組的所有參考將被都移除。 首先必須卸除所有的 FILESTREAM 資料行。 您必須使用 SET FILESTREAM_ON**="**NULL**"**刪除所有與資料表相關聯的 FILESTREAM 資料。  
  
 設定**(** SYSTEM_VERSIONING  **=**  {OFF |在 [(HISTORY_TABLE = schema_name。 名稱 [，DATA_CONSISTENCY_CHECK = { **ON** |關閉}]）]} **)**  
 **適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 請停用資料表的系統版本設定，或啟用系統版本設定的資料表。 若要啟用系統版本設定的資料表，系統會確認符合資料類型、 null 屬性條件約束，並對系統版本設定的主索引鍵條件約束需求。 如果未使用 HISTORY_TABLE 引數，系統會產生新的記錄資料表，比對目前的資料表中，兩個資料表之間建立連結的結構描述，並可以讓系統記錄每一筆記錄歷程記錄資料表中目前的資料表中。 此歷程記錄資料表的名稱會是`MSSQL_TemporalHistoryFor<primary_table_object_id>`。 如果 HISTORY_TABLE 引數用來建立的連結，並使用現有的記錄資料表，是目前的資料表和指定的資料表之間建立連結。 建立現有記錄資料表的連結時，您可以選擇執行資料一致性檢查。 這項資料一致性檢查可確保現有的記錄沒有重疊。 預設執行資料一致性檢查。 如需相關資訊，請參閱 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)。  
  
HISTORY_RETENTION_PERIOD = {**無限**| 數目 {日 |天 |週 | 週 |月 |月 |年份 |年}}**適用於**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  

時態表中指定有限或 infinte 保留歷程記錄資料。 如果省略，則會假設無限期保留。
  
 設定**(** LOCK_ESCALATION = {自動 |資料表 |停用} **)**  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定資料表鎖定擴大的允許方法。  
  
 AUTO  
 此選項允許 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 選取適用於資料表結構描述的鎖定擴大資料粒度。  
  
-   如果資料表是分割區資料表，將允許鎖定擴大進行分割區。 當鎖定擴大為分割區層級後，就無法進一步擴大為 TABLE 資料粒度。  
  
-   如果資料表不是分割區，則會對 TABLE 資料粒度執行鎖定擴大。  
  
TABLE  
 不論資料表是否為分割區資料表，鎖定擴大將在資料表層級的資料粒度上完成。 TABLE 為預設值。  
  
 DISABLE  
 在大多數情況下都避免使用鎖定擴大， 但並非完全不允許資料表層級的鎖定。 例如，當您在可序列化隔離層級下掃描沒有任何叢集索引的資料表時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 必須採用資料表鎖定以保護資料的完整性。  
  
 REBUILD  
 REBUILD WITH 語法可用來重建整個資料表，包括已分割區之資料表中的所有分割區。 如果資料表有叢集索引，則 REBUILD 選項會重建叢集索引。 REBUILD 可以執行為 ONLINE 作業。  
  
 REBUILD PARTITION 語法可用來重建已分割區之資料表中的單一分割區。  
  
 PARTITION = ALL  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 在變更分割區壓縮設定時重建所有分割區。  
  
 REBUILD WITH ( \<rebuild_option >)  
 所有選項都適用於具有叢集索引的資料表。 如果資料表沒有叢集索引，則只有其中一些選項會影響堆積結構。  
  
 當特定壓縮設定並非使用 REBUILD 作業來指定時，就會使用分割區的目前壓縮設定。 若要傳回的目前設定，請查詢**data_compression**中的資料行**sys.partitions**目錄檢視。  
  
 如需重建選項的完整描述，請參閱[index_option &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-table-index-option-transact-sql.md).  
  
 DATA_COMPRESSION  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 針對指定的資料表、分割區編號或分割區範圍指定資料壓縮選項。 選項如下：  
  
 無  
 不壓縮資料表或指定的分割區。 這不適用於資料行存放區資料表。  
  
 ROW  
 使用資料列壓縮來壓縮資料表或指定的分割區。 這不適用於資料行存放區資料表。  
  
 PAGE  
 使用頁面壓縮來壓縮資料表或指定的分割區。 這不適用於資料行存放區資料表。  
  
 COLUMNSTORE  
 **適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 只適用於資料行存放區資料表。 COLUMNSTORE 指定解壓縮之前以 COLUMNSTORE_ARCHIVE 選項壓縮的分割區。 當還原資料時，資料將會繼續以用於所有資料行存放區資料表的資料行存放區壓縮來壓縮。  
  
 COLUMNSTORE_ARCHIVE  
 **適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 只適用於資料行存放區資料表，這些資料表會與叢集資料行存放區索引一起儲存。 COLUMNSTORE_ARCHIVE 將進一步將指定的分割區壓縮成較小的大小。 這可用於封存，或是其他需要較少儲存體，而且可負擔更多時間來儲存和擷取的狀況  
  
 若要同時重建多個資料分割，請參閱[index_option &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-table-index-option-transact-sql.md). 如果資料表沒有叢集索引，變更資料壓縮將會重建堆積和非叢集索引。 如需有關壓縮的詳細資訊，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
 線上 **=**  {ON |**OFF** }\<在套用至 single_partition_rebuild_option >  
 指定在索引作業期間，查詢和資料修改是否能夠使用基礎資料表的單一分割區和相關聯的索引。 預設值為 OFF。 REBUILD 可以執行為 ONLINE 作業。  
  
 ON  
 索引作業持續期間不會保留長期資料表鎖定。 在索引重建開始時，資料表上需要 S 鎖定，而在線上索引重建結束時，資料表上需要 Sch-M 鎖定。 雖然這兩個鎖定是短暫的中繼資料鎖定，尤其是 Sch-M 鎖定必須等候所有封鎖交易完成。 在等候期間，Sch-M 鎖定會在存取相同資料表時，封鎖等待在這個鎖定之後的所有其他交易。  
  
> [!NOTE]  
>  線上索引重建可設定*low_priority_lock_wait*本節稍後說明的選項。  
  
 OFF  
 在索引作業期間會套用資料表鎖定。 這可防止所有使用者在作業持續期間存取基礎資料表。  
  
 *create* XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 這是資料行集的名稱。 資料行集是不具類型的 XML 表示，可將資料表的所有疏鬆資料行結合到結構化輸出中。 如果資料表已包含疏鬆資料行，資料行集無法加入該資料表中。 如需資料行集的詳細資訊，請參閱 [使用資料行集](../../relational-databases/tables/use-column-sets.md)。  
  
 { ENABLE | DISABLE } FILETABLE_NAMESPACE  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 啟用或停用 FileTable 的系統定義條件約束。 只能用於 FileTable。  
  
 設定 (FILETABLE_DIRECTORY = *directory_name* )  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定 Windows 相容的 FileTable 目錄名稱。 在資料庫的所有 FileTable 目錄名稱之間，此名稱必須是唯一的。 不論 SQL 定序設定為何，唯一性比較不區分大小寫。 只能用於 FileTable。  
```    
 SET (  
        REMOTE_DATA_ARCHIVE   
        {  
            = ON (  <table_stretch_options> )  
          | = OFF_WITHOUT_DATA_RECOVERY  
          ( MIGRATION_STATE = PAUSED ) | ( <table_stretch_options> [, ...n] )  
        } )  
```    
**適用於**： [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 啟用或停用 Stretch Database 資料表。 如需詳細資訊，請參閱 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)。  
  
 **為資料表啟用 Stretch Database**  
  
 當您啟用 Stretch 的資料表指定`ON`，您也必須指定`MIGRATION_STATE = OUTBOUND`開始移轉資料的立即或`MIGRATION_STATE = PAUSED`延後資料移轉。 預設值是`MIGRATION_STATE = OUTBOUND`。 如需啟用 Stretch 的資料表的詳細資訊，請參閱[針對資料表啟用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)。  
  
 **必要條件**。 為資料表啟用 「 延展 」 之前，您必須在伺服器和資料庫上啟用 Stretch。 如需詳細資訊，請參閱 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)。  
  
 **權限**。 啟用 Stretch 的資料庫或資料表需要 db_owner 權限。 啟用 Stretch 的資料表也需要資料表的 ALTER 權限。  
  
 **針對資料表停用 Stretch Database**  
  
 當您停用資料表的延展功能時，您會有兩個選項的已移轉至 Azure 的遠端資料。 如需詳細資訊，請參閱 [停用 Stretch Database 並帶回遠端資料](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)。  
  
-   若要針對資料表停用 Stretch，並將資料表的遠端資料從 Azure複製回 SQL Server，請執行下列命令。 無法取消此命令。  
  
    ```tsql  
ALTER TABLE \<table name>
       SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ;  
    ```  
  
     此作業會產生資料傳輸成本，且無法取消。 如需詳細資訊，請參閱 [資料傳輸定價詳細資料](https://azure.microsoft.com/en-us/pricing/details/data-transfers/)。  
  
     將所有遠端資料從 Azure 複製回 SQL Server 後，即會針對資料表停用 Stretch。  
  
-   若要針對資料表停用 Stretch 並放棄遠端資料，請執行下列命令。  
  
    ```tsql  
ALTER TABLE \<table_name>
       SET ( REMOTE_DATA_ARCHIVE = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED ) ) ;  
    ```  
  
 針對資料表停用 Stretch Database 後，即會停止執行資料移轉作業，且查詢結果不再包含來自遠端資料表的結果。  
  
 停用 Stretch，並不會移除遠端資料表。 若您想要刪除遠端資料表，則必須使用 Azure 管理入口網站將其卸除。  
  
[FILTER_PREDICATE = {null |*述詞*}]  
 **適用於**： [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 （選擇性） 指定篩選述詞來選取要移轉包含歷史和目前資料的資料表資料列。 此述詞必須呼叫決定性內嵌資料表值函式。 如需詳細資訊，請參閱[針對資料表啟用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)和[選取要使用篩選函數 &#40; 遷移資料列Stretch Database &#41;](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).   
  
> [!IMPORTANT]  
>  若您提供執行狀況不佳的篩選器述詞，資料移轉也無法順利執行。 Stretch Database 使用 CROSS APPLY 運算子，將篩選器述詞套用至資料表。  
  
 若您未指定篩選器述詞，則會遷移整個資料表。  
  
 當您指定篩選器述詞時，您也必須指定*MIGRATION_STATE*。  
  
 MIGRATION_STATE = {輸出 | 輸入 |暫停}  
 **適用於**： [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
-   指定`OUTBOUND`將資料從 SQL Server 移轉至 Azure。  
  
-   指定`INBOUND`複製遠端從 Azure 資料表的資料會備份到 SQL Server，以及針對資料表停用 Stretch。 如需詳細資訊，請參閱 [停用 Stretch Database 並帶回遠端資料](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)。  
  
     此作業會產生資料傳輸成本，且無法取消。  
  
-   指定`PAUSED`暫停或延後資料移轉。 如需詳細資訊，請參閱[暫停和繼續資料移轉 &#40;Stretch Database &#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
WAIT_AT_LOW_PRIORITY  
 **適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 線上索引重建必須等候這個資料表的封鎖作業。 **WAIT_AT_LOW_PRIORITY**表示線上索引重建作業將會等候低優先權鎖定，讓其他作業，線上索引建立作業等候時繼續進行。 省略**WAIT AT LOW PRIORITY**選項相當於 WA`IT_AT_LOW_PRIORITY ( MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`。  
  
 MAX_DURATION =*時間*[**分鐘**]  
 **適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 等候時間 （以分鐘為單位的整數值），**交換器**或執行 DDL 命令時，線上索引重建鎖定將會以低優先順序等候。 如果操作已遭到封鎖**MAX_DURATION**時間的其中一個**ABORT_AFTER_WAIT**會在執行動作。 **MAX_DURATION**時間永遠是以分鐘和 word**分鐘**可以省略。  
  
 ABORT_AFTER_WAIT = [**NONE** | **自助** | **封鎖**}]  
 **適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 無  
 繼續等候一般 (標準) 優先權的鎖定。  
  
 SELF  
 結束**交換器**或線上索引重建 DDL 作業目前正在執行而不採取任何動作。  
  
 BLOCKERS  
 刪除所有目前封鎖的使用者交易**交換器**或線上索引重建 DDL 作業，讓作業可以繼續。  
  
 需要**ALTER ANY CONNECTION**權限。  
  
如果存在  
 **適用於**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[新版](http://go.microsoft.com/fwlink/p/?LinkId=299658)) 和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 有條件地卸除資料行或條件約束已經存在。  
  
## <a name="remarks"></a>備註  
 若要加入新的資料列，使用[插入](../../t-sql/statements/insert-transact-sql.md)。 若要移除的資料列，請使用[刪除](../../t-sql/statements/delete-transact-sql.md)或[TRUNCATE TABLE](../../t-sql/statements/truncate-table-transact-sql.md)。 若要變更現有的資料列中的值，請使用[更新](../../t-sql/queries/update-transact-sql.md)。  
  
 如果參考資料表的程序快取中有任何執行計畫，ALTER TABLE 會加以標示，以便在下一次執行時重新編譯。  
  
## <a name="changing-the-size-of-a-column"></a>變更資料行的大小  
 您可以在 ALTER COLUMN 子句中指定資料行資料類型的新大小，以變更資料行的長度、有效位數或小數位數。 如果資料行中有資料存在，則新大小不得小於資料的最大大小。 此外，資料行不能定義在索引中，除非資料行是**varchar**， **nvarchar**，或**varbinary**資料類型，且索引不是主索引鍵的結果條件約束。 請參閱範例 P。  
  
## <a name="locks-and-alter-table"></a>鎖定和 ALTER TABLE  
 ALTER TABLE 中指定的變更會立即實作。 如果變更作業需要修改資料表中的資料列，ALTER TABLE 會更新資料列。 ALTER TABLE 會取得資料表上的結構描述修改 (SCH-M) 鎖定，以確定下列事項：在變更期間，除了在結束時需要非常短暫的 SCH-M 鎖定之線上索引作業以外，沒有其他連接會參考資料表的中繼資料。 在 ALTER TABLE…SWITCH 作業中，不論在來源資料表或目標資料表上都會取得鎖定。 對資料表所做的修改會記錄下來，且完全可復原。 影響每份極大型資料表中之所有資料列的變更 (例如，卸除資料行或在某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本上加入含有預設值的 NOT NULL 資料行) 可能需要很長的時間才能完成及產生多個記錄。 執行這些 ALTER TABLE 陳述式時，要像執行任何影響多個資料列的 INSERT、UPDATE 或 DELETE 陳述式時一樣地小心。  
  
### <a name="adding-not-null-columns-as-an-online-operation"></a>以線上作業的方式加入 NOT NULL 資料行  
 從開始[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Enterprise 版本中，新增的預設值時，預設值的 NOT NULL 資料行就是線上作業*執行階段常數*。 這表示，不論資料表中的資料列數目為何，此作業幾乎會立即完成。 這是因為資料表中的現有資料列不會在作業期間更新。而是，預設值只會儲存在資料表的中繼資料內，而且存取這些資料列的查詢會視需要查閱此值。 這種行為是自動的。不需要任何額外的語法，即可實作超越 ADD COLUMN 語法的線上作業。 執行階段常數是一種運算式，它會在執行階段針對資料表中的每個資料列產生相同的值，不論其決定性為何。 例如，常數運算式 "My temporary data" 或系統函數 GETUTCDATETIME() 都是執行階段常數。 相較之下，NEWID() 或 NEWSEQUENTIALID() 函數不是執行階段常數，因為它們會針對資料表中的每個資料列產生唯一值。 加入含有非執行階段常數之預設值的 NOT NULL 資料行一律以離線方式執行，而且系統會在作業期間取得獨佔 (SCH-M) 鎖定。  
  
 當現有的資料列參考中繼資料內儲存的值時，如果已插入任何新資料列但並未針對資料行指定另一個值，預設值就會儲存在資料列上。 當您更新資料列 (即使沒有在 UPDATE 陳述式中指定實際的資料行) 或是重建資料表或叢集索引時，中繼資料內儲存的預設值會移至現有的資料列。  
  
 類型的資料行**varchar （max)**， **nvarchar （max)**， **varbinary （max)**， **xml**，**文字**， **ntext**，**映像**， **hierarchyid**，**幾何**， **geography**，或無法 CLR UDT加入一項線上作業。 您無法線上加入資料行，如果這樣做，就會導致最大可能的資料列大小超過 8,060 位元組限制。 在此情況中，資料行會以離線作業的方式加入。  
  
## <a name="parallel-plan-execution"></a>平行計畫執行  
 在[!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)]和處理器的數目愈高，用來執行單一 ALTER TABLE ADD （索引為依據） CONSTRAINT 或 DROP （叢集索引） CONSTRAINT 陳述式由**的最大平行處理原則程度**組態選項和目前的工作負載。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 偵測到系統在忙碌中，則在開始執行陳述式之前，會先自動降低作業平行原則的程度。 您可以指定 MAXDOP 選項，手動設定用來執行陳述式的處理器數目。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。  
  
## <a name="partitioned-tables"></a>分割區資料表  
 除了執行涉及分割區資料表的 SWITCH 作業以外，ALTER TABLE 還可用來變更分割區資料表之資料行、條件約束及觸發程序的狀態，就像它是用於非分割區資料表一樣。 不過，這個陳述式不可用來變更資料表本身的分割區方式。 若要重新分割資料分割的資料表，使用[ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md)和[ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md)。 此外，您也不能變更分割區資料表的資料行資料類型。  
  
## <a name="restrictions-on-tables-with-schema-bound-views"></a>含有結構描述繫結檢視表之資料表的限制  
 適用於含有結構描述繫結檢視之資料表上的 ALTER TABLE 陳述式的限制，跟修改含有簡式索引之資料表時目前所適用的限制一樣。 允許加入資料行。 不過，不允許移除或變更參與任何結構描述繫結檢視表的資料行。 如果 ALTER TABLE 陳述式需要變更結構描述繫結檢視中使用的資料行，ALTER TABLE 會失敗，且 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會引發錯誤訊息。 如需有關結構描述繫結和索引檢視表的詳細資訊，請參閱[CREATE VIEW &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
 建立參考資料表的結構描述繫結檢視，不會影響基底資料表上之觸發程序的新增或移除。  
  
## <a name="indexes-and-alter-table"></a>索引和 ALTER TABLE  
 當條件約束卸除時，建立為條件約束之一部分的索引也會卸除。 必須利用 DROP INDEX 來卸除利用 CREATE INDEX 建立的索引。 ALTER INDEX 陳述式可用來重建條件約束定義中索引的部分；不必卸除條件約束，然後又利用 ALTER TABLE 新增條件約束。  
  
 若要移除某資料行，必須先移除以該資料行為基礎的所有索引和條件約束。  
  
 刪除建立叢集索引的條件約束時，儲存在叢集索引分葉層級中的資料列會儲存在非叢集資料表中。 您可以卸除叢集索引，再藉由指定 MOVE TO 選項，於單一交易中將結果資料表移到另一個檔案群組或分割區配置。 MOVE TO 選項有下列限制：  
  
-   MOVE TO 對於索引檢視表或非叢集索引無效。  
  
-   分割區配置或檔案群組必須已經存在。  
  
-   如果未指定 MOVE TO，資料表會放在針對叢集索引定義的相同分割區配置或檔案群組中。  
  
當您卸除叢集的索引時，您可以指定 ONLINE  **=**  ON 選項，使 DROP INDEX 交易不會封鎖查詢和修改基礎資料和相關聯的非叢集的索引。  
  
 線上 **=**  ON 有下列限制：  
  
-   線上 **=**  ON 不適用於也會停用的叢集索引。 停用的索引必須利用 ONLINE 來卸除 **=**  OFF。  
  
-   一次只能卸除一個索引。  
  
-   線上 **=**  ON 不適用於索引的檢視、 非叢集索引或本機暫存資料表上的索引。  
  
-   線上 **=**  ON 不適用於資料行存放區索引。  
  
卸除叢集索引時，需要一個大小等於現有叢集索引的暫存磁碟空間。 作業完成時，會立即釋放此額外空間。  
  
> [!NOTE]  
>  底下列出的選項 *\<drop_clustered_constraint_option >*套用至資料表的叢集索引，但不可套用至檢視上的叢集的索引或非叢集的索引。  
  
## <a name="replicating-schema-changes"></a>複寫結構描述變更  
 根據預設，當您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者的已發行資料表上執行 ALTER TABLE 時，該項變更就會傳播到所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。 這項功能具有某些限制，而且可停用。 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
## <a name="data-compression"></a>資料壓縮  
 系統資料表無法啟用壓縮。 如果資料表是堆積，ONLINE 模式的重建作業將會是單一執行緒。 請針對多執行緒的堆積重建作業使用 OFFLINE 模式。 如需資料壓縮的詳細資訊，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
 若要評估變更壓縮狀態如何影響資料表、索引或分割區，請使用 [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) 預存程序。  
  
 下列限制適用於分割區資料表：  
  
-   您無法在資料表具有非對齊索引時變更單一分割區的壓縮設定。  
  
-   ALTER TABLE\<資料表 > REBUILD PARTITION...語法會重建指定的資料分割。  
  
-   ALTER TABLE\<資料表 > REBUILD WITH...語法會重建所有分割區。  
  
## <a name="dropping-ntext-columns"></a>卸除 NTEXT 資料行  
 卸除 NTEXT 資料行時，已刪除資料的清除作業會在所有資料列上的序列化作業執行時發生。 這可能需要相當長的時間。 卸除包含大量資料列的資料表中的 NTEXT 資料行時，請先將 NTEXT 更新為 NULL 值，再卸除該資料行。 這可透過平行作業執行，而且速度加快許多。  
  
## <a name="online-index-rebuild"></a>線上索引重建  
 為了執行線上索引重建的 DDL 陳述式，特定資料表上執行的所有使用中封鎖交易都必須完成。 當線上索引重建執行時，它會封鎖這個資料表上準備開始執行的所有新交易。 雖然線上索引重建的鎖定期間很短，但是等候特定資料表上所有未完成的交易完成並封鎖要開始的新交易，可能會大幅影響輸送量，導致工作負載速度變慢或逾時，並且大幅限制對基礎資料表的存取。 **WAIT_AT_LOW_PRIORITY**選項可讓 DBA 管理線上索引重建，並允許它們選取 3 個選項的其中一個所需的 S 鎖定和 SCH-M 鎖定。 在這 3 個案例中，如果在等候期間 (`(MAX_DURATION =n [minutes])`) 沒有封鎖活動，線上索引重建會立即執行而不等候，並 DDL 陳述式會完成。  
  
## <a name="compatibility-support"></a>相容性支援  
 ALTER TABLE 陳述式只允許兩部分 (schema.object) 資料表名稱。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，使用下列格式來指定資料表名稱會在編譯階段失敗，並顯示錯誤 117。  
  
-   server.database.schema.table  
  
-   .database.schema.table  
  
-   ..schema.table  
  
在舊版中，指定 server.database.schema.table 格式會傳回錯誤 4902。 不過，指定 .database.schema.table 格式或 ..schema.table 格式會成功。  
  
 若要解決此問題，請移除 4 部分前置詞的用法。  
  
## <a name="permissions"></a>Permissions  
 需要資料表的 ALTER 權限。  
  
 ALTER TABLE 權限可套用至涉及 ALTER TABLE SWITCH 陳述式的兩種資料表。 所切換的任何資料，都會繼承目標資料表的安全性。  
  
 如果將 ALTER TABLE 陳述式中的任何資料行定義為屬於 Common Language Runtime (CLR) 使用者定義類型或別名資料類型，則需要對該類型具有 REFERENCES 權限。  
  
 若要加入的資料行，會更新資料表的資料列必須**更新**資料表的權限。 例如，加入**NOT NULL**與預設值或不是空的資料表時加入識別欄位的資料行。  
  
##  <a name="Example_Top"></a> 範例  
  
|類別目錄|代表性語法元素|  
|--------------|------------------------------|  
|[加入資料行和條件約束](#add)|ADD • 含索引選項的 PRIMARY KEY • 疏鬆資料行和資料行集 •|  
|[卸除資料行和條件約束](#Drop)|DROP|  
|[修改資料行定義](#alter_column)|變更資料類型 • 變更資料行大小 • 定序|  
|[修改資料表定義](#alter_table)|DATA_COMPRESSION • SWITCH PARTITION • LOCK ESCALATION • 變更追蹤|  
|[停用和啟用條件約束和觸發程序](#disable_enable)|CHECK • NO CHECK • ENABLE TRIGGER • DISABLE TRIGGER|  
  
###  <a name="add"></a>加入資料行和條件約束  
 本節中的範例示範如何將資料行和條件約束加入至資料表。  
  
#### <a name="a-adding-a-new-column"></a>A. 加入新資料行  
 下列範例會加入一個資料行，該資料行允許 Null 值，且不含利用 DEFAULT 定義提供的值。 在這個新資料行中，每一個資料列都會有 `NULL`。  
  
```  
CREATE TABLE dbo.doc_exa (column_a INT) ;  
GO  
ALTER TABLE dbo.doc_exa ADD column_b VARCHAR(20) NULL ;  
GO  
  
```  
  
#### <a name="b-adding-a-column-with-a-constraint"></a>B. 加入含有條件約束的資料行  
 下列範例會加入一個含有 `UNIQUE` 條件約束的新資料行。  
  
```  
CREATE TABLE dbo.doc_exc (column_a INT) ;  
GO  
ALTER TABLE dbo.doc_exc ADD column_b VARCHAR(20) NULL   
    CONSTRAINT exb_unique UNIQUE ;  
GO  
EXEC sp_help doc_exc ;  
GO  
DROP TABLE dbo.doc_exc ;  
GO  
```  
  
#### <a name="c-adding-an-unverified-check-constraint-to-an-existing-column"></a>C. 將未確認的 CHECK 條件約束加入現有的資料行  
 下列範例將條件約束加入至資料表中的現有資料行。 該資料行含有違反該條件約束的值。 因此，`WITH NOCHECK` 可用來防止根據現有的資料列來驗證條件約束，並允許加入條件約束。  
  
```  
CREATE TABLE dbo.doc_exd ( column_a INT) ;  
GO  
INSERT INTO dbo.doc_exd VALUES (-1) ;  
GO  
ALTER TABLE dbo.doc_exd WITH NOCHECK   
ADD CONSTRAINT exd_check CHECK (column_a > 1) ;  
GO  
EXEC sp_help doc_exd ;  
GO  
DROP TABLE dbo.doc_exd ;  
GO  
```  
  
#### <a name="d-adding-a-default-constraint-to-an-existing-column"></a>D. 將 DEFAULT 條件約束加入現有的資料行  
 下列範例會建立一份含有兩個資料行的資料表、在第一個資料行插入值，並讓另一個資料行保持 NULL。 然後再將 `DEFAULT` 條件約束加入至第二個資料行。 若要確認已套用預設值，請在第一個資料行中插入其他值，然後查詢資料表。  
  
```  
CREATE TABLE dbo.doc_exz ( column_a INT, column_b INT) ;  
GO  
INSERT INTO dbo.doc_exz (column_a)VALUES ( 7 ) ;  
GO  
ALTER TABLE dbo.doc_exz  
ADD CONSTRAINT col_b_def  
DEFAULT 50 FOR column_b ;  
GO  
INSERT INTO dbo.doc_exz (column_a) VALUES ( 10 ) ;  
GO  
SELECT * FROM dbo.doc_exz ;  
GO  
DROP TABLE dbo.doc_exz ;  
GO  
```  
  
#### <a name="e-adding-several-columns-with-constraints"></a>E. 加入數個含有條件約束的資料行  
 下列範例會加入數個資料行，這些資料行含有利用新資料行定義的條件約束。 第一個新資料行有 `IDENTITY` 屬性。 資料表中的每一個資料列在識別欄位中都有新的累加值。  
  
```  
CREATE TABLE dbo.doc_exe ( column_a INT CONSTRAINT column_a_un UNIQUE) ;  
GO  
ALTER TABLE dbo.doc_exe ADD   
  
-- Add a PRIMARY KEY identity column.  
column_b INT IDENTITY  
CONSTRAINT column_b_pk PRIMARY KEY,   
  
-- Add a column that references another column in the same table.  
column_c INT NULL    
CONSTRAINT column_c_fk   
REFERENCES doc_exe(column_a),  
  
-- Add a column with a constraint to enforce that   
-- nonnull data is in a valid telephone number format.  
column_d VARCHAR(16) NULL   
CONSTRAINT column_d_chk  
CHECK   
(column_d LIKE '[0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]' OR  
column_d LIKE  
'([0-9][0-9][0-9]) [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]'),  
  
-- Add a nonnull column with a default.  
column_e DECIMAL(3,3)  
CONSTRAINT column_e_default  
DEFAULT .081 ;  
GO  
EXEC sp_help doc_exe ;  
GO  
DROP TABLE dbo.doc_exe ;  
GO  
```  
  
#### <a name="f-adding-a-nullable-column-with-default-values"></a>F. 加入含有預設值並可為 Null 的資料行  
 下列範例會加入含有 `DEFAULT` 定義且可為 Null 的資料行，並利用 `WITH VALUES` 為資料表中的每一個現有資料列提供值。 如果沒有使用 WITH VALUES，每一個資料列的新資料行中都會有 NULL 值。  
  
```  
  
CREATE TABLE dbo.doc_exf ( column_a INT) ;  
GO  
INSERT INTO dbo.doc_exf VALUES (1) ;  
GO  
ALTER TABLE dbo.doc_exf   
ADD AddDate smalldatetime NULL  
CONSTRAINT AddDateDflt  
DEFAULT GETDATE() WITH VALUES ;  
GO  
DROP TABLE dbo.doc_exf ;  
GO  
```  
  
#### <a name="g-creating-a-primary-key-constraint-with-index-options"></a>G. 建立含有索引選項的 PRIMARY KEY 條件約束  
 下列範例會建立 PRIMARY KEY 條件約束 `PK_TransactionHistoryArchive_TransactionID`，並設定選項 `FILLFACTOR`、`ONLINE` 及 `PAD_INDEX`。 產生的叢集索引將與條件約束同名。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```  
USE AdventureWorks2012;  
GO  
ALTER TABLE Production.TransactionHistoryArchive WITH NOCHECK   
ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)  
WITH (FILLFACTOR = 75, ONLINE = ON, PAD_INDEX = ON);  
GO  
```  
  
#### <a name="h-adding-a-sparse-column"></a>H. 加入疏鬆資料行  
 下列範例示範如何在資料表 T1 中加入及修改疏鬆資料行。 建立資料表 `T1` 的程式碼如下。  
  
```  
CREATE TABLE T1  
(C1 int PRIMARY KEY,  
C2 varchar(50) SPARSE NULL,  
C3 int SPARSE NULL,  
C4 int ) ;  
GO  
```  
  
 若要加入其他的疏鬆資料行 `C5`，請執行下列陳述式。  
  
```  
ALTER TABLE T1  
ADD C5 char(100) SPARSE NULL ;  
GO  
```  
  
 若要將 `C4` 非疏鬆資料行轉換成疏鬆資料行，請執行下列陳述式。  
  
```  
ALTER TABLE T1  
ALTER COLUMN C4 ADD SPARSE ;  
GO  
```  
  
 要轉換`C4`疏鬆資料行，為疏鬆資料行中，執行下列陳述式。  
  
```  
ALTER TABLE T1  
ALTER COLUMN C4 DROP SPARSE;  
GO  
```  
  
#### <a name="i-adding-a-column-set"></a>I. 加入資料行集  
 下列範例示範如何將資料行加入至資料表 `T2`。 如果資料表已包含疏鬆資料行，就無法在該資料表中加入資料行集。 建立資料表 `T2` 的程式碼如下。  
  
```  
CREATE TABLE T2  
(C1 int PRIMARY KEY,  
C2 varchar(50) NULL,  
C3 int NULL,  
C4 int ) ;  
GO  
```  
  
 下列三個陳述式會加入名為 `CS` 的資料行集，然後將資料行 `C2` 和 `C3` 修改為 `SPARSE`。  
  
```  
ALTER TABLE T2  
ADD CS XML COLUMN_SET FOR ALL_SPARSE_COLUMNS ;  
GO  
  
ALTER TABLE T2  
ALTER COLUMN C2 ADD SPARSE ;   
GO  
  
ALTER TABLE T2  
ALTER COLUMN C3 ADD SPARSE ;  
GO  
```  
  
#### <a name="j-adding-an-encrypted-column"></a>J. 加入加密的資料行  
 下列陳述式會將加密的資料行，名為`PromotionCode`。  
  
```  
ALTER TABLE Customers ADD  
    PromotionCode nvarchar(100)   
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = MyCEK,  
    ENCRYPTION_TYPE = RANDOMIZED,  
    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') ;  
```  
  
###  <a name="Drop"></a>卸除資料行和條件約束  
 本節中的範例示範如何卸除資料行和條件約束。  
  
#### <a name="a-dropping-a-column-or-columns"></a>A. 卸除資料行  
 第一個範例會修改資料表來移除資料行。 第二個範例會移除多個資料行。  
  
```  
CREATE TABLE dbo.doc_exb   
    (column_a INT  
     ,column_b VARCHAR(20) NULL  
     ,column_c datetime  
     ,column_d int) ;  
GO  
-- Remove a single column.  
ALTER TABLE dbo.doc_exb DROP COLUMN column_b ;  
GO  
-- Remove multiple columns.  
ALTER TABLE dbo.doc_exb DROP COLUMN column_c, column_d;  
  
```  
  
#### <a name="b-dropping-constraints-and-columns"></a>B. 卸除條件約束和資料行  
 第一個範例會從資料表中移除 `UNIQUE` 條件約束。 第二個範例會移除兩個條件約束與單一資料行。  
  
```  
CREATE TABLE dbo.doc_exc ( column_a int NOT NULL CONSTRAINT my_constraint UNIQUE) ;  
GO  
  
-- Example 1. Remove a single constraint.  
ALTER TABLE dbo.doc_exc DROP my_constraint ;  
GO  
  
DROP TABLE dbo.doc_exc;  
GO  
  
CREATE TABLE dbo.doc_exc ( column_a int    
                          NOT NULL CONSTRAINT my_constraint UNIQUE  
                          ,column_b int   
                          NOT NULL CONSTRAINT my_pk_constraint PRIMARY KEY) ;  
GO  
  
-- Example 2. Remove two constraints and one column  
-- The keyword CONSTRAINT is optional. The keyword COLUMN is required.  
ALTER TABLE dbo.doc_exc   
  
    DROP CONSTRAINT CONSTRAINT my_constraint, my_pk_constraint, COLUMN column_b ;  
GO  
  
```  
  
#### <a name="c-dropping-a-primary-key-constraint-in-the-online-mode"></a>C. 在 ONLINE 模式中卸除 PRIMARY KEY 條件約束  
 下列範例會刪除 PRIMARY KEY 條件約束，並將 `ONLINE` 選項設為 `ON`。  
  
```  
  
ALTER TABLE Production.TransactionHistoryArchive  
DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID  
WITH (ONLINE = ON);  
GO  
```  
  
#### <a name="d-adding-and-dropping-a-foreign-key-constraint"></a>D. 加入或卸除 FOREIGN KEY 條件約束  
 下列範例會建立資料表 `ContactBackup`，然後改變該資料表，方式是先加入一個參考 `FOREIGN KEY` 資料表的 `Person.Person` 條件約束，再卸除 `FOREIGN KEY` 條件約束。  
  
```  
CREATE TABLE Person.ContactBackup  
    (ContactID int) ;  
GO  
  
ALTER TABLE Person.ContactBackup  
ADD CONSTRAINT FK_ContactBacup_Contact FOREIGN KEY (ContactID)  
    REFERENCES Person.Person (BusinessEntityID) ;  
GO  
  
ALTER TABLE Person.ContactBackup  
DROP CONSTRAINT FK_ContactBacup_Contact ;  
GO  
  
DROP TABLE Person.ContactBackup ;  
```  
  
 ![搭配回到頁首連結使用的箭號圖示](../../analysis-services/instances/media/uparrow16x16.gif "搭配回到頁首連結使用的箭號圖示")[範例](#Example_Top)  
  
###  <a name="alter_column"></a>修改資料行定義  
  
#### <a name="a-changing-the-data-type-of-a-column"></a>A. 變更資料行的資料類型  
 下列範例會將資料表的資料行從 `INT` 變更為 `DECIMAL`。  
  
```  
CREATE TABLE dbo.doc_exy (column_a INT ) ;  
GO  
INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
GO  
ALTER TABLE dbo.doc_exy ALTER COLUMN column_a DECIMAL (5, 2) ;  
GO  
DROP TABLE dbo.doc_exy ;  
GO  
```  
  
#### <a name="b-changing-the-size-of-a-column"></a>B. 變更資料欄的大小  
 下列範例會增加大小**varchar**資料行的有效位數和小數位數**十進位**資料行。 因為資料行包含資料，所以資料行大小只能增加。 另請注意，`col_a` 會定義於唯一索引中。 大小`col_a`仍可增加，因為資料類型是**varchar**而且索引不是 PRIMARY KEY 條件約束的結果。  
  
```  
-- Create a two-column table with a unique index on the varchar column.  
CREATE TABLE dbo.doc_exy ( col_a varchar(5) UNIQUE NOT NULL, col_b decimal (4,2));  
GO  
INSERT INTO dbo.doc_exy VALUES ('Test', 99.99);  
GO  
-- Verify the current column size.  
SELECT name, TYPE_NAME(system_type_id), max_length, precision, scale  
FROM sys.columns WHERE object_id = OBJECT_ID(N'dbo.doc_exy');  
GO  
-- Increase the size of the varchar column.  
ALTER TABLE dbo.doc_exy ALTER COLUMN col_a varchar(25);  
GO  
-- Increase the scale and precision of the decimal column.  
ALTER TABLE dbo.doc_exy ALTER COLUMN col_b decimal (10,4);  
GO  
-- Insert a new row.  
INSERT INTO dbo.doc_exy VALUES ('MyNewColumnSize', 99999.9999) ;  
GO  
-- Verify the current column size.  
SELECT name, TYPE_NAME(system_type_id), max_length, precision, scale  
FROM sys.columns WHERE object_id = OBJECT_ID(N'dbo.doc_exy');  
```  
  
#### <a name="c-changing-column-collation"></a>C. 變更資料行定序  
 下列範例將示範如何變更資料行的定序。 首先，資料表是包含預設使用者定序的已建立資料表。  
  
```  
CREATE TABLE T3  
(C1 int PRIMARY KEY,  
C2 varchar(50) NULL,  
C3 int NULL,  
C4 int ) ;  
GO  
```  
  
 接著，將資料行 `C2` 定序變更為 Latin1_General_BIN。 請注意，資料類型即使不會變更，但卻是必要的。  
  
```  
ALTER TABLE T3  
ALTER COLUMN C2 varchar(50) COLLATE Latin1_General_BIN;  
GO  
  
```  

  
###  <a name="alter_table"></a>修改資料表定義  
 本節中的範例示範如何修改資料表的定義。  
  
#### <a name="a-modifying-a-table-to-change-the-compression"></a>A. 修改資料表以變更壓縮  
 下列範例會變更非分割區資料表的壓縮。 堆積或叢集索引將會重建。 如果資料表為堆積，則所有非叢集索引將會重建。  
  
```  
ALTER TABLE T1   
REBUILD WITH (DATA_COMPRESSION = PAGE);  
```  
  
 下列範例會變更分割區資料表的壓縮。 `REBUILD PARTITION = 1` 語法只會造成分割區號碼 `1` 的重建。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  NONE) ;  
GO  
```  
  
使用下列替代語法的相同作業會造成資料表內所有分割區的重建。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = ALL   
WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(1) ) ;  
```  
  
 如需其他資料壓縮範例，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
#### <a name="b-modifying-a-columnstore-table-to-change-archival-compression"></a>B. 修改資料行存放區資料表來變更封存壓縮  
 下列範例藉由套用其他壓縮演算法來進一步壓縮資料行存放區資料表的分割區。 這樣會縮小資料表，但是也會增加儲存和擷取所需的時間。 這對於封存，或是需要較少空間而且可負擔更多時間來儲存和擷取的狀況很實用。  
  
**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
GO  
```  
  
以下範例會將之前以 COLUMNSTORE_ARCHIVE 選項壓縮的資料行存放區資料表分割區解壓縮。 當還原資料時，資料將會繼續以用於所有資料行存放區資料表的資料行存放區壓縮來壓縮。  
  
**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
GO  
```  
  
#### <a name="c-switching-partitions-between-tables"></a>C. 在資料表之間切換分割區  
 下列範例會建立分割區資料表，並假設資料庫中已經建立分割區配置 `myRangePS1`。 接著會建立一個非分割區資料表，其結構與分割區資料表相同，並且與資料表 `PARTITION 2` 的 `PartitionTable` 位於相同的檔案群組上。 然後，資料表 `PARTITION 2` 之 `PartitionTable` 的資料就會切換到資料表 `NonPartitionTable` 中。  
  
```  
CREATE TABLE PartitionTable (col1 int, col2 char(10))  
ON myRangePS1 (col1) ;  
GO  
CREATE TABLE NonPartitionTable (col1 int, col2 char(10))  
ON test2fg ;  
GO  
ALTER TABLE PartitionTable SWITCH PARTITION 2 TO NonPartitionTable ;  
GO  
```  
  
#### <a name="d-allowing-lock-escalation-on-partitioned-tables"></a>D. 允許對分割區擴大鎖定  
 下列範例會在分割區資料表上啟用分割區層級的鎖定擴大。 如果資料表不是分割區資料表，則鎖定擴大會在 TABLE 層級設定。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```  
ALTER TABLE dbo.T1 SET (LOCK_ESCALATION = AUTO);  
GO  
```  
  
#### <a name="e-configuring-change-tracking-on-a-table"></a>E. 設定資料表的變更追蹤  
 下列範例會啟用 `Person.Person` 資料表上的變更追蹤。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```  
USE AdventureWorks2012;  
ALTER TABLE Person.Person  
ENABLE CHANGE_TRACKING;  
```  
  
下列範例會啟用變更追蹤，並為變更期間更新的資料行啟用追蹤。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
USE AdventureWorks2012;  
GO  
ALTER TABLE Person.Person  
ENABLE CHANGE_TRACKING  
WITH (TRACK_COLUMNS_UPDATED = ON)  
```  
  
下列範例會停用 `Person.Person` 資料表上的變更追蹤。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```  
USE AdventureWorks2012;  
Go  
ALTER TABLE Person.Person  
DISABLE CHANGE_TRACKING;  
```  

  
###  <a name="disable_enable"></a>停用和啟用條件約束和觸發程序  
  
#### <a name="a-disabling-and-re-enabling-a-constraint"></a>A. 停用及重新啟用條件約束  
 下列範例會停用限制資料中所接受之薪資的條件約束。 `NOCHECK CONSTRAINT` 若與 `ALTER TABLE` 搭配使用，可以停用條件約束，並允許插入通常會違反條件約束的值。 `CHECK CONSTRAINT` 可重新啟用條件約束。  
  
```  
CREATE TABLE dbo.cnst_example   
(id INT NOT NULL,  
 name VARCHAR(10) NOT NULL,  
 salary MONEY NOT NULL  
    CONSTRAINT salary_cap CHECK (salary < 100000)  
);  
  
-- Valid inserts  
INSERT INTO dbo.cnst_example VALUES (1,'Joe Brown',65000);  
INSERT INTO dbo.cnst_example VALUES (2,'Mary Smith',75000);  
  
-- This insert violates the constraint.  
INSERT INTO dbo.cnst_example VALUES (3,'Pat Jones',105000);  
  
-- Disable the constraint and try again.  
ALTER TABLE dbo.cnst_example NOCHECK CONSTRAINT salary_cap;  
INSERT INTO dbo.cnst_example VALUES (3,'Pat Jones',105000);  
  
-- Re-enable the constraint and try another insert; this will fail.  
ALTER TABLE dbo.cnst_example CHECK CONSTRAINT salary_cap;  
INSERT INTO dbo.cnst_example VALUES (4,'Eric James',110000) ;  
```  
  
#### <a name="b-disabling-and-re-enabling-a-trigger"></a>B. 停用及重新啟用觸發程序  
 下列範例會使用 `DISABLE TRIGGER` 的 `ALTER TABLE` 選項停用觸發程序，並允許通常會違反此觸發程序規定的插入作業。 接著會再使用 `ENABLE TRIGGER` 重新啟用此觸發程序。  
  
```  
CREATE TABLE dbo.trig_example   
(id INT,   
name VARCHAR(12),  
salary MONEY) ;  
GO  
-- Create the trigger.  
CREATE TRIGGER dbo.trig1 ON dbo.trig_example FOR INSERT  
AS  
IF (SELECT COUNT(*) FROM INSERTED  
WHERE salary > 100000) > 0  
BEGIN  
    print 'TRIG1 Error: you attempted to insert a salary > $100,000'  
    ROLLBACK TRANSACTION  
END ;  
GO  
-- Try an insert that violates the trigger.  
INSERT INTO dbo.trig_example VALUES (1,'Pat Smith',100001) ;  
GO  
-- Disable the trigger.  
ALTER TABLE dbo.trig_example DISABLE TRIGGER trig1 ;  
GO  
-- Try an insert that would typically violate the trigger.  
INSERT INTO dbo.trig_example VALUES (2,'Chuck Jones',100001) ;  
GO  
-- Re-enable the trigger.  
ALTER TABLE dbo.trig_example ENABLE TRIGGER trig1 ;  
GO  
-- Try an insert that violates the trigger.  
INSERT INTO dbo.trig_example VALUES (3,'Mary Booth',100001) ;  
GO  
```  
 
  
### <a name="online-operations"></a>線上作業  
  
#### <a name="a-online-index-rebuild-using-low-priority-wait-options"></a>A. 使用低優先順序等候選項的線上索引重建  
 下列範例示範如何執行指定低優先順序等候選項的線上索引重建。  
  
**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```  
ALTER TABLE T1   
REBUILD WITH   
(  
    PAD_INDEX = ON,  
    ONLINE = ON ( WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 4 MINUTES, 
                                         ABORT_AFTER_WAIT = BLOCKERS ) )  
)  
;  
```  
  
#### <a name="b-online-alter-column"></a>B. Online Alter Column  
 下列範例示範如何使用 ONLINE 選項執行變更資料行作業。  
  
**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```  
CREATE TABLE dbo.doc_exy (column_a INT ) ;  
GO  
INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
GO  
ALTER TABLE dbo.doc_exy   
    ALTER COLUMN column_a DECIMAL (5, 2) WITH (ONLINE = ON);  
GO  
sp_help doc_exy;  
DROP TABLE dbo.doc_exy ;  
GO  
```  
  
##  <a name="system_versioning"></a>系統版本設定  
 下列四個範例將協助您熟悉使用系統版本設定的語法。 如需其他協助，請參閱[開始使用系統版本設定時態表](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)。  
  
**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
### <a name="a-add-system-versioning-to-existing-tables"></a>A. 將系統版本設定加入現有的資料表  
 下列範例會示範如何將系統版本設定加入現有的資料表，並建立未來的歷程記錄資料表。 這個範例假設沒有現有的資料表呼叫`InsurancePolicy`與定義的主索引鍵。 此範例中會填入新建立的期間資料行對系統版本設定使用的開始和結束時間的預設值，因為這些值不能是 null。 此範例會使用 HIDDEN 子句，以確保不會影響到現有的應用程式與目前的資料表進行互動。  它也會使用位於的 HISTORY_RETENTION_PERIOD[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]只。 
  
```  
--Alter non-temporal table to define periods for system versioning  
ALTER TABLE InsurancePolicy  
ADD PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime),   
SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL 
    DEFAULT GETUTCDATE(),   
SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL 
    DEFAULT CONVERT(DATETIME2, '9999-12-31 23:59:59.99999999');  
--Enable system versioning with 1 year retention for historical data
ALTER TABLE InsurancePolicy 
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 1 YEAR));  
```  
  
### <a name="b-migrate-an-existing-solution-to-use-system-versioning"></a>B. 移轉現有的方案使用系統版本設定  
 下列範例會示範如何從使用觸發程序來模擬暫時支援的解決方案移轉至系統版本設定。 這個範例假設沒有現有的方案使用`ProjectTaskCurrent`資料表和`ProjectTaskHistory`適用於資料表其現有的解決方案，會使用 變更日期和修改日期資料行其長一段時間，這些期間資料行，並未採用 datetime2 資料類型而且`ProjectTaskCurrent`資料表有定義的主索引鍵。  
  
```  
-- Drop existing trigger  
DROP TRIGGER ProjectTaskCurrent_Trigger;  
-- Adjust the schema for current and history table  
-- Change data types for existing period columns  
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [Changed Date] datetime2 NOT NULL;  
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [Revised Date] datetime2 NOT NULL;  
  
ALTER TABLE ProjectTaskHistory ALTER COLUMN [Changed Date] datetime2 NOT NULL;  
ALTER TABLE ProjectTaskHistory ALTER COLUMN [Revised Date] datetime2 NOT NULL;  
  
-- Add SYSTEM_TIME period and set system versioning with linking two existing tables  
-- (a certain set of data checks happen in the background)  
ALTER TABLE ProjectTaskCurrent  
ADD PERIOD FOR SYSTEM_TIME ([Changed Date], [Revised Date])  
  
ALTER TABLE ProjectTaskCurrent  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProjectTaskHistory, DATA_CONSISTENCY_CHECK = ON))  
```  
  
### <a name="c-disabling-and-re-enabling-system-versioning-to-change-table-schema"></a>C. 停用並重新啟用系統版本設定來變更資料表結構描述  
 這個範例示範如何停用上的系統版本設定`Department`資料表、 加入資料行，並重新啟用系統版本設定。 停用系統版本設定，才能修改資料表結構描述。 執行這些步驟，以防止這兩個資料表的更新，更新資料表結構描述，這可讓 DBA 略過資料一致性檢查時重新啟用系統版本設定，並取得效能獲益時在交易內。 請注意工作，例如建立統計資料、 切換資料分割或壓縮套用到一或兩個資料表不需要停用系統版本設定。  
  
```  
BEGIN TRAN  
/* Takes schema lock on both tables */  
ALTER TABLE Department  
    SET (SYSTEM_VERSIONING = OFF);  
/* expand table schema for temporal table */  
ALTER TABLE Department  
     ADD Col5 int NOT NULL DEFAULT 0;  
/* Expand table schema for history table */  
ALTER TABLE DepartmentHistory  
    ADD Col5 int NOT NULL DEFAULT 0;  
/* Re-establish versioning again  */
ALTER TABLE Department  
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE=dbo.DepartmentHistory, 
                                 DATA_CONSISTENCY_CHECK = OFF));  
COMMIT   
```  
  
### <a name="d-removing-system-versioning"></a>D. 移除系統版本設定  
 這個範例示範如何從 Department 資料表和 drop 中完全移除系統版本設定`DepartmentHistory`資料表。 （選擇性） 您可能也要卸除系統用來記錄系統版本設定資訊的期間資料行。 請注意，您無法卸除 `Department`或`DepartmentHistory`資料表啟用系統版本設定時。  
  
```  
ALTER TABLE Department  
    SET (SYSTEM_VERSIONING = OFF);  
ALTER TABLE Department  
DROP PEROD FOR SYSTEM_TIME;  
DROP TABLE DepartmentHistory;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例 A 到 C 使用中的，FactResellerSales 資料表[!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]資料庫。  
  
### <a name="e-determining-if-a-table-is-partitioned"></a>E. 判斷是否已分割資料表  
 下列查詢會在資料表 `FactResellerSales` 已分割時，傳回一個或多個資料列。 如果資料表未分割，則不會傳回任何資料列。  
  
```  
SELECT * FROM sys.partitions AS p  
JOIN sys.tables AS t  
    ON  p.object_id = t.object_id  
WHERE p.partition_id IS NOT NULL  
    AND t.name = 'FactResellerSales';  
```  
  
### <a name="f-determining-boundary-values-for-a-partitioned-table"></a>F. 決定資料分割資料表的界限值  
 下列查詢會針對 `FactResellerSales` 資料表中的每一個分割區傳回界限值。  
  
```  
SELECT t.name AS TableName, i.name AS IndexName, p.partition_number, 
    p.partition_id, i.data_space_id, f.function_id, f.type_desc, 
    r.boundary_id, r.value AS BoundaryValue   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.partitions AS p  
    ON i.object_id = p.object_id AND i.index_id = p.index_id   
JOIN  sys.partition_schemes AS s   
    ON i.data_space_id = s.data_space_id  
JOIN sys.partition_functions AS f   
    ON s.function_id = f.function_id  
LEFT JOIN sys.partition_range_values AS r   
    ON f.function_id = r.function_id and r.boundary_id = p.partition_number  
WHERE t.name = 'FactResellerSales' AND i.type <= 1  
ORDER BY p.partition_number;  
```  
  
### <a name="g-determining-the-partition-column-for-a-partitioned-table"></a>G. 決定資料分割資料表的資料分割資料行  
 下列查詢會傳回資料表之分割區資料行的名稱。 `FactResellerSales`。  
  
```  
SELECT t.object_id AS Object_ID, t.name AS TableName, 
    ic.column_id as PartitioningColumnID, c.name AS PartitioningColumnName   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.columns AS c  
    ON t.object_id = c.object_id  
JOIN sys.partition_schemes AS ps  
    ON ps.data_space_id = i.data_space_id  
JOIN sys.index_columns AS ic  
    ON ic.object_id = i.object_id 
    AND ic.index_id = i.index_id AND ic.partition_ordinal > 0  
WHERE t.name = 'FactResellerSales'  
AND i.type <= 1  
AND c.column_id = ic.column_id;  
```  
  
### <a name="h-merging-two-partitions"></a>H. 合併兩個資料分割  
 下列範例會合併兩個資料分割的資料表上。  
  
 `Customer`資料表具有下列定義：  
  
```  
CREATE TABLE Customer (  
    id int NOT NULL,  
    lastName varchar(20),  
    orderCount int,  
    orderDate date)  
WITH   
    ( DISTRIBUTION = HASH(id),  
    PARTITION ( orderCount RANGE LEFT  
    FOR VALUES (1, 5, 10, 25, 50, 100)));  
```  
  
 下列命令會結合 10 到 25 的資料分割界限。  
  
```  
ALTER TABLE Customer MERGE RANGE (10);  
```  
  
 新的 DDL 資料表為：  
  
```  
CREATE TABLE Customer (  
    id int NOT NULL,  
    lastName varchar(20),  
    orderCount int,  
    orderDate date)  
WITH   
    ( DISTRIBUTION = HASH(id),  
    PARTITION ( orderCount RANGE LEFT  
    FOR VALUES (1, 5, 25, 50, 100)));  
```  
  
### <a name="i-splitting-a-partition"></a>I. 分割資料分割  
 下列範例會分割資料表上的磁碟分割。  
  
 `Customer`資料表有下列 DDL:  
  
```  
DROP TABLE Customer;  
  
CREATE TABLE Customer (  
    id int NOT NULL,  
    lastName varchar(20),  
    orderCount int,  
    orderDate date)  
WITH   
    ( DISTRIBUTION = HASH(id),  
    PARTITION ( orderCount RANGE LEFT  
    FOR VALUES (1, 5, 10, 25, 50, 100 )));  
```  
  
 下列命令會建立新的資料分割所 50 與 100 之間的值 75，繫結。  
  
```  
ALTER TABLE Customer SPLIT RANGE (75);  
```  
  
 新的 DDL 資料表為：  
  
```  
CREATE TABLE Customer (  
   id int NOT NULL,  
   lastName varchar(20),  
   orderCount int,  
   orderDate date)  
   WITH DISTRIBUTION = HASH(id),  
   PARTITION ( orderCount (RANGE LEFT  
      FOR VALUES (1, 5, 10, 25, 50, 75, 100 )));  
```  
  
### <a name="j-using-switch-to-move-a-partition-to-a-history-table"></a>J. 使用參數將資料分割移至記錄資料表  
 下列範例會將資料移動的資料分割中`Orders`資料表中的分割區`OrdersHistory`資料表。  
  
 `Orders`資料表有下列 DDL:  
  
```  
CREATE TABLE Orders (  
    id INT,  
    city VARCHAR (25),  
    lastUpdateDate DATE,  
    orderDate DATE )  
WITH   
    (DISTRIBUTION = HASH ( id ),  
    PARTITION ( orderDate RANGE RIGHT   
    FOR VALUES ('2004-01-01', '2005-01-01', '2006-01-01', '2007-01-01' )));  
```  
  
 在此範例中，`Orders`資料表具有下列資料分割。 每個資料分割包含的資料。  
  
|資料分割|具有資料嗎？|界限的範圍|  
|---------------|---------------|--------------------|  
|1|是|OrderDate < ' 2004年-01-01'|  
|2|是|'2004年-01-01' < = OrderDate <' 2005年-01-01'|  
|3|是|'2005年-01-01' < = OrderDate <' 2006年-01-01'|  
|4|是|'2006年-01-01'< = OrderDate <' 2007年-01-01'|  
|5|是|' 2007年-01-01' < = OrderDate|  
  
-   資料分割 1 （沒有資料）： OrderDate < ' 2004年-01-01'  
-   資料分割 2 （有資料）: '2004年-01-01' < = OrderDate <' 2005年-01-01'  
-   分割區 3 （具有資料）: '2005年-01-01' < = OrderDate <' 2006年-01-01'  
-   資料分割 4 （具有資料）: '2006年-01-01'< = OrderDate <' 2007年-01-01'  
-   分割區 5 （具有資料）: ' 2007年-01-01' < = OrderDate  
  
`OrdersHistory`資料表有下列 DDL，具有相同的資料行和資料行名稱做為`Orders`資料表。 兩者都是雜湊分佈在`id`資料行。  
  
```  
CREATE TABLE OrdersHistory (  
   id INT,  
   city VARCHAR (25),  
   lastUpdateDate DATE,  
   orderDate DATE )  
WITH   
    (DISTRIBUTION = HASH ( id ),  
    PARTITION ( orderDate RANGE RIGHT   
    FOR VALUES ( '2004-01-01' )));  
```  
  
 資料行和資料行名稱必須相同，雖然不需要相同資料分割界限。 在此範例中，`OrdersHistory`資料表具有下列兩個資料分割和兩個資料分割是空的：  
  
-   資料分割 1 （無資料）： OrderDate < ' 2004年-01-01'  
-   資料分割 2 （空白）: ' 2004年-01-01' < = OrderDate  
  
如先前的兩個資料表，下列命令會將所有資料列`OrderDate < '2004-01-01'`從`Orders`資料表`OrdersHistory`資料表。  
  
```  
ALTER TABLE Orders SWITCH PARTITION 1 TO OrdersHistory PARTITION 1;  
```  
  
 如此一來，第一個資料分割中`Orders`是空白且第一個資料分割中的`OrdersHistory`包含資料。 資料表現在會出現，如下所示：  
  
 `Orders`資料表  
  
-   資料分割 1 （空白）： OrderDate < ' 2004年-01-01'  
-   資料分割 2 （有資料）: '2004年-01-01' < = OrderDate <' 2005年-01-01'  
-   分割區 3 （具有資料）: '2005年-01-01' < = OrderDate <' 2006年-01-01'  
-   資料分割 4 （具有資料）: '2006年-01-01'< = OrderDate <' 2007年-01-01'  
-   分割區 5 （具有資料）: ' 2007年-01-01' < = OrderDate  
  
 `OrdersHistory`資料表  
  
-   資料分割 1 （沒有資料）： OrderDate < ' 2004年-01-01'  
-   資料分割 2 （空白）: ' 2004年-01-01' < = OrderDate  
  
若要清除`Orders`資料表中，您可以移除空的資料分割合併資料分割 1 和 2，如下所示：  
  
```  
ALTER TABLE Orders MERGE RANGE ('2004-01-01');  
```  
  
 在合併之後`Orders`資料表具有下列資料分割：  
  
 `Orders`資料表  
  
-   資料分割 1 （沒有資料）： OrderDate < ' 2005年-01-01'  
-   資料分割 2 （有資料）: '2005年-01-01' < = OrderDate <' 2006年-01-01'  
-   分割區 3 （具有資料）: '2006年-01-01'< = OrderDate <' 2007年-01-01'  
-   資料分割 4 （具有資料）: ' 2007年-01-01' < = OrderDate  
  
假設傳遞其他年份，並準備好封存 2005 年。 您可以將空的分割區配置中 2005 年`OrdersHistory`資料表分割空的分割區，如下所示：  
  
```  
ALTER TABLE OrdersHistory SPLIT RANGE ('2005-01-01');  
```  
  
 在分割之後，`OrdersHistory`資料表具有下列資料分割：  
  
 `OrdersHistory`資料表  
  
-   資料分割 1 （沒有資料）： OrderDate < ' 2004年-01-01'  
-   資料分割 2 （空白）: '2004年-01-01' <' 2005年-01-01'  
-   分割區 3 （空白）: ' 2005年-01-01' < = OrderDate  
  
## <a name="see-also"></a>另請參閱  
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [ALTER PARTITION SCHEME &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  


