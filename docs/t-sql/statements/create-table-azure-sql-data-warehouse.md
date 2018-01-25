---
title: "建立資料表 （Azure SQL 資料倉儲） |Microsoft 文件"
ms.custom: 
ms.date: 07/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: ea21c73c-40e8-4c54-83d4-46ca36b2cf73
caps.latest.revision: "59"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f6e639bf97ed132b6ace7128b4cbe9b6f3ce474e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="create-table-azure-sql-data-warehouse"></a>建立資料表 （Azure SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  建立新的資料表中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
 
若要了解資料表和使用方式，請參閱[SQL 資料倉儲中的資料表](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-overview/)。

注意： SQL 資料倉儲，這篇文章中討論適用於 SQL 資料倉儲與 Parallel Data Warehouse 除非另有說明。 
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

<a name="Syntax"></a>   
## <a name="syntax"></a>語法  
  
```  
-- Create a new table. 
CREATE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( 
      { column_name <data_type>  [ <column_options> ] } [ ,...n ]   
    )  
    [ WITH [ <table_option> [ ,...n ] ) ]  
[;]  
   
<column_options> ::=
    [ COLLATE Windows_collation_name ]  
    [ NULL | NOT NULL ] -- default is NULL  
    [ [ CONSTRAINT constraint_name ] DEFAULT constant_expression  ]
  
<table_option> ::= 
    {   
        CLUSTERED COLUMNSTORE INDEX --default for SQL Data Warehouse 
      | HEAP --default for Parallel Data Warehouse   
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) -- default is ASC 
    }  
    { 
        DISTRIBUTION = HASH ( distribution_column_name ) 
      | DISTRIBUTION = ROUND_ROBIN -- default for SQL Data Warehouse
      | DISTRIBUTION = REPLICATE -- default for Parallel Data Warehouse
    }   
    | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] -- default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) )  
  
<data type> ::=   
      datetimeoffset [ ( n ) ]  
    | datetime2 [ ( n ) ]  
    | datetime  
    | smalldatetime  
    | date  
    | time [ ( n ) ]  
    | float [ ( n ) ]  
    | real [ ( n ) ]  
    | decimal [ ( precision [ , scale ] ) ]   
    | numeric [ ( precision [ , scale ] ) ]   
    | money  
    | smallmoney  
    | bigint  
    | int   
    | smallint  
    | tinyint  
    | bit  
    | nvarchar [ ( n | max ) ]  -- max applies only to SQL Data Warehouse 
    | nchar [ ( n ) ]  
    | varchar [ ( n | max )  ] -- max applies only to SQL Data Warehouse  
    | char [ ( n ) ]  
    | varbinary [ ( n | max ) ] -- max applies only to SQL Data Warehouse  
    | binary [ ( n ) ]  
    | uniqueidentifier  
```  

<a name="Arguments"></a>   
## <a name="arguments"></a>引數  
 *database_name*  
 將包含新資料表的資料庫名稱。 預設為目前資料庫。  
  
 *schema_name*  
 資料表的結構描述。 指定*結構描述*是選擇性的。 如果空白，則會使用預設的結構描述。  
  
 *table_name*  
 新的資料表名稱。 若要建立本機暫存資料表，資料表名前加上 #。  如需說明和暫存資料表的指引，請參閱[Azure SQL 資料倉儲中的暫存資料表](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-temporary/)。 
 
 *column_name*  
 資料表資料行的名稱。
   
### <a name="ColumnOptions"></a>資料行選項

 `COLLATE` *Windows_collation_name*  
 指定運算式的定序。 定序必須是所支援的 Windows 定序之一[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需所支援的 Windows 定序的清單[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱[Windows 定序名稱 (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms188046\(v=sql11\)/)。  
  
 `NULL` | `NOT NULL`  
 指定是否`NULL`資料行中允許的值。 預設值為 `NULL`。  
  
 [ `CONSTRAINT` *constraint_name* ] `DEFAULT` *constant_expression*  
 指定預設資料行值。  
  
 | 引數 | 說明 |
 | -------- | ----------- |
 | *constraint_name* | 選擇性的條件約束名稱。 條件約束名稱是在資料庫內唯一的。 名稱可以是其他資料庫中重複使用。 |
 | *constant_expression* | 資料行的預設值。 運算式必須是常值或常數。 允許這些常數的運算式，例如： `'CA'`， `4`。 這些不允許： `2+3`， `CURRENT_TIMESTAMP`。 |
  

### <a name="TableOptions"></a>資料表結構選項
如需選擇資料表類型的指引，請參閱[編製索引的資料表中 Azure SQL 資料倉儲](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-index/)。
  
 `CLUSTERED COLUMNSTORE INDEX`  
將資料表儲存為叢集資料行存放區索引。 叢集資料行存放區索引適用於所有的資料表資料。 這是預設值[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。   
 
 `HEAP`   
  將資料表儲存為堆積。 這是預設值[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
 `CLUSTERED INDEX` ( *index_column_name* [ ,...*n* ] )  
 將資料表儲存為叢集索引與一個或多個索引鍵資料行。 這是由資料列所儲存的資料。 使用*index_column_name*索引中指定的一或多個索引鍵資料行名稱。  如需詳細資訊，請參閱 < 一般備註中的資料列存放區資料表。
 
 `LOCATION = USER_DB`   
 此選項已被取代。 它會在語法上被接受，但不再需要，並不會再影響行為。   
  
### <a name="TableDistributionOptions"></a>資料表分佈選項
若要了解如何選擇最佳散發方法，並使用分散式的資料表，請參閱[散發 Azure SQL 資料倉儲中的資料表](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-distribute/)。

`DISTRIBUTION = HASH` ( *distribution_column_name* )   
指派給一個發佈的每個資料列，雜湊值儲存在所*distribution_column_name*。 這表示永遠雜湊到相同發佈相同的值，此演算法為具決定性。  散發資料行應定義為 NOT NULL，因為 NULL 會指派給相同的通訊群組的所有資料列。

`DISTRIBUTION = ROUND_ROBIN`   
將資料列平均分散到循環配置資源方式中的所有分佈。 這是預設值[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。

`DISTRIBUTION = REPLICATE`    
每個計算節點上儲存一份資料表。 如[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]資料表儲存在散發資料庫上的每個計算節點上。 如[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，資料表儲存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]跨越計算節點的檔案群組。 這是預設值[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。
  
### <a name="TablePartitionOptions"></a>資料表資料分割選項
如需使用資料表資料分割的指引，請參閱[SQL 資料倉儲中的資料表資料分割](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/)。

 `PARTITION` ( *partition_column_name* `RANGE` [ `LEFT` | `RIGHT` ] `FOR VALUES` ( [ *boundary_value* [,...*n*] ] ))   
建立一或多個資料表資料分割。 這些是水平資料表配量可讓您執行的資料列，不論是否儲存為堆積、 叢集的索引或叢集資料行存放區索引的資料表子集的作業。 與散發 資料行不同的是資料表資料分割不會決定每個資料列所在的散發。 相反地，資料表資料分割所決定的資料列群組和儲存在每個發佈的方式。  
 
| 引數 | 說明 |
| -------- | ----------- |
|*partition_column_name*| 指定的資料行，[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]將分割的資料列。 此資料行可以是任何資料類型。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]資料分割資料行值，以遞增順序排序。 從低到高順序下移`LEFT`至`RIGHT`的用途的`RANGE`規格。 |  
| `RANGE LEFT` | 指定的界限值屬於左 （較低的值） 上的磁碟分割。 預設值為 LEFT。 |
| `RANGE RIGHT` | 指定的界限值屬於資料分割上的權限 （更高的值）。 | 
| `FOR VALUES` ( *boundary_value* [,...*n*] ) | 指定資料分割的界限值。 *boundary_value*是常數運算式。 它不能是 NULL。 它必須符合或可隱含轉換成的資料型別*partition_column_name*。 它無法截斷隱含轉換期間，這樣的大小和小數位數的值不相符的資料型別*partition_column_name*<br></br><br></br>如果您指定`PARTITION`子句，但未指定界限值，[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]將一個資料分割使用建立分割區的資料表。 如果適用的話，您分割成兩個資料分割在稍後的資料表。<br></br><br></br>如果您指定一個界限值，產生的資料表有兩個磁碟分割。其中一個值低於界限值，另一個用於高於界限值的值。 請注意，是否您將資料分割移到非資料分割的資料表時，非資料分割的資料表會接收資料，但不是會有資料分割界限中它的中繼資料。| 
 
 請參閱[建立分割區的資料表](#PartitionedTable)範例 > 一節中。

### <a name="DataTypes"></a>資料類型
[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]支援最常使用的資料類型。 以下是支援的資料類型，以及它們的詳細資料和儲存體位元組的清單。 若要進一步了解資料類型和使用方式，請參閱[SQL 資料倉儲中的資料表的資料型別](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-data-types)。

資料類型轉換表，請參閱的隱含轉換 區段中， [CAST 和 CONVERT (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms187928/)。

`datetimeoffset` [ ( *n* ) ]  
 預設值為 *n* 為 7。  
  
 `datetime2` [ ( *n* ) ]  
與相同`datetime`，不過，您可以指定小數秒數。 預設值為 *n* 是`7`。  
  
|*n*值|有效位數|小數位數|  
|--:|--:|-:|  
|`0`|19|0|  
|`1`|21|1|  
|`2`|22|2|  
|`3`|23|3|  
|`4`|24|4|  
|`5`|25|5|  
|`6`|26|6|  
|`7`|27|7|  
  
 `datetime`  
 儲存與根據西曆的 19 到 23 個字元的一天的日期和時間。 日期可以包含年、 月和日。 時間包含小時、 分和秒。選項，您可以顯示三位數小數秒數。 儲存體大小是 8 位元組。  
  
 `smalldatetime`  
 儲存日期和時間。 儲存體大小是 4 個位元組。  
  
 `date`  
 儲存使用最多 10 個字元的年、 月和日根據西曆日期。 儲存體大小是 3 個位元組。 日期會儲存為整數。  
  
 `time` [ ( *n* ) ]  
 預設值為 *n* 是`7`。  
  
 `float` [ ( *n* ) ]  
 大約的數字資料類型用於浮點數資料。 浮點數資料是近似值，這表示資料型別範圍內不是所有值都可以正確都表示。 *n*指定用來儲存的尾數的位元數`float`科學記號標記法。 因此，  *n* 規定的有效位數和儲存體大小。 如果 *n* 指定，則它必須是介於`1`和`53`。 預設值 *n* 是`53`。  
  
| *n*值 | 有效位數 | 儲存體大小 |  
| --------: | --------: | -----------: |  
| 1-24   | 7 位數  | 4 個位元組      |  
| 25-53  | 15 位數 | 8 個位元組      |  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]會將 *n* 做為其中一個兩個可能值。 如果`1` <=   *n*   <=  `24`，  *n* 會被視為`24`。 如果`25`  <=   *n*   <=  `53`，  *n* 會被視為`53`。  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] `float`資料型別符合 ISO 標準的所有值 *n* 從`1`透過`53`。 雙精確度的同義字是`float(53)`。  
  
 `real` [ ( *n* ) ]  
 實際的定義是浮點數相同。 `real` 的 ISO 同義字是 `float(24)`。  
  
 `decimal`[(*精確度*[ *，標尺*])] |`numeric` [(*精確度*[ *，標尺*])]  
 固定有效位數和小數位數的數字的存放區。  
  
 *有效位數*  
 可儲存的最大十進位數總數，小數點左右兩側都包括在內。 有效位數必須介於`1`透過最大有效位數`38`。 預設有效位數是`18`。  
  
 *scale*  
 小數點右側所能儲存的最大十進位數。 *標尺*必須是介於`0`透過*精確度*。 您只能指定*標尺*如果*精確度*指定。 預設小數位數是`0`; 因此， `0`  <= *標尺* <= *精確度*。 最大儲存體大小會隨著有效位數而不同。  
  
| 有效位數 | 儲存體位元組  |  
| ---------: |-------------: |  
|  1-9       |             5 |  
| 10-19      |             9 |  
| 20-28      |            13 |  
| 29-38      |            17 |  
  
 `money` | `smallmoney`  
 代表貨幣值的資料類型。  
  
| 資料類型 | 儲存體位元組 |  
| --------- | ------------: |  
| `money`|8|  
| `smallmoney` |4|  
  
 `bigint` | `int` | `smallint` | `tinyint`  
 使用整數資料的 Exact-number 資料類型。 儲存體 下表所示。  
  
| 資料類型 | 儲存體位元組 |  
| --------- | ------------: |  
| `bigint`|8|  
| `int` |4|  
| `smallint` |2|  
| `tinyint` |1|  
  
 `bit`  
 整數資料類型可接受的值`1`， `0`，或 ' 為 NULL。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]儲存體最佳化的位元資料行。 如果資料表中有 8 或更少的位元資料行，資料行儲存為 1 個位元組。 如果有 9 到 16 位元資料行，資料行儲存成 2 位元組，並以此類推。  
  
 `nvarchar`[(  *n*   |  `max` )]-`max`僅適用於[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
 可變長度的 Unicode 字元資料。 *n*可以是 1 到 4000 之間的值。 `max` 表示儲存體大小上限是 2^31-1 個位元組 (2 GB)。 以位元組為單位的儲存體大小是輸入字元加上 2 位元組的數目兩倍。 輸入的資料長度可以是 0 個字元。  
  
 `nchar` [ ( *n* ) ]  
 固定長度 Unicode 字元資料的長度為 *n* 字元。 *n*必須是介於`1`透過`4000`。 儲存體大小是兩次 *n* 位元組。  
  
 `varchar`[(  *n*    |  `max` )]-`max`僅適用於[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。   
 可變長度非 Unicode 字元資料的長度為 *n* 位元組。 *n*必須是介於`1`至`8000`。 `max`表示儲存體大小上限是 2 ^31-1 位元組 (2 GB)。儲存體大小是輸入資料的實際長度再加上 2 個位元組。  
  
 `char` [ ( *n* ) ]  
 固定長度非 Unicode 字元資料的長度為 *n* 位元組。 *n*必須是介於`1`至`8000`。 儲存體大小是 *n* 位元組。 預設值為 *n* 是`1`。  
  
 `varbinary`[(  *n*    |  `max` )]-`max`僅適用於[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
 可變長度的二進位資料。 *n*可以是值`1`至`8000`。 `max` 表示儲存體大小上限是 2^31-1 個位元組 (2 GB)。 儲存體大小是輸入資料的實際長度再加上 2 位元組。 預設值為 *n* 為 7。  
  
 `binary` [ ( *n* ) ]  
 固定長度二進位資料的長度為 *n* 位元組。 *n*可以是值`1`至`8000`。 儲存體大小是 *n* 位元組。 預設值為 *n* 是`7`。  
  
 `uniqueidentifier`  
 這是 16 位元組的 GUID。  
   
<a name="Permissions"></a>  
## <a name="permissions"></a>Permissions  
 建立資料表需要的權限`db_ddladmin`固定資料庫角色或：
 - `CREATE TABLE`資料庫的權限
 - `ALTER SCHEMA`將包含資料表的結構描述上的權限。 

建立資料分割的資料表，需要權限`db_ddladmin`固定資料庫角色，或

- `ALTER ANY DATASPACE`權限
  
 建立本機暫存資料表的登入接收`CONTROL`， `INSERT`， `SELECT`，和`UPDATE`資料表的權限。  
 
<a name="GeneralRemarks"></a>  
## <a name="general-remarks"></a>一般備註  
 
最小和最大限制，請參閱[SQL 資料倉儲容量限制](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-service-capacity-limits/)。 
 
### <a name="determining-the-number-of-table-partitions"></a>決定資料表資料分割數目
每個使用者定義資料表分成多個較小的資料表儲存在個別呼叫發佈的位置中。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]會使用 60 分佈。 在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，分佈的數目取決於計算節點的數目。
 
每個通訊群組包含所有資料表資料分割。 例如，如果有 60 的分佈和四個資料表資料分割，會有 320 資料分割。 如果資料表是叢集資料行存放區索引，會有一個資料行存放區索引，每個資料分割，這表示您的資料行存放區索引是 320。

我們建議使用較少的資料表資料分割，以確保每個資料行存放區索引具備足夠的資料列，以充分利用的資料行存放區索引的優點。 如需進一步的指引，請參閱[SQL 資料倉儲中的資料表資料分割](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/)和[編製索引的 SQL 資料倉儲中的資料表](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-tables-index/)  

  
 ### <a name="rowstore-table-heap-or-clustered-index"></a>資料列存放區資料表 （堆積或叢集的索引）  
 資料列存放區資料表是儲存在資料列的資料列順序中的資料表。 它是堆積或叢集的索引。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]所有資料列存放區資料表建立具有頁面壓縮。這不是使用者可設定。   
 
 ### <a name="columnstore-table-columnstore-index"></a>資料行存放區資料表 （資料行存放區索引）
資料行存放區資料表是儲存在資料行的資料行順序中的資料表。 資料行存放區索引是管理資料儲存在資料行存放區資料表中的技術。  叢集資料行存放區索引不會影響散發資料的方式;它會影響資料儲存在每個發佈的方式。

若要變更資料行存放區資料表的資料列存放區資料表，卸除所有現有的索引資料表，並建立非叢集資料行存放區索引。 如需範例，請參閱[CREATE COLUMNSTORE INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md).

如需詳細資訊，請參閱下列文章：
- [資料行存放區索引建立版本功能摘要](https://msdn.microsoft.com/library/dn934994/)
- [索引在 SQL 資料倉儲中的資料表](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-tables-index/)
- [資料行存放區索引指南](~/relational-databases/indexes/columnstore-indexes-overview.md) 
 
<a name="LimitationsRestrictions"></a>  
## <a name="limitations-and-restrictions"></a>限制事項  
 您無法定義散發資料行的預設條件約束。  
  
 ### <a name="partitions"></a>資料分割
 當使用資料分割，分割區資料行不能有僅限 Unicode 的定序。 例如，下列陳述式會失敗。  
  
 `CREATE TABLE t1 ( c1 varchar(20) COLLATE Divehi_90_CI_AS_KS_WS) WITH (PARTITION (c1 RANGE FOR VALUES (N'')))`  
 
 如果*boundary_value*是常值必須能夠隱含地轉換成資料類型中*partition_column_name*，就會發生不一致的情形。 常值會顯示透過[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]系統檢視表的轉換的值來進行[!INCLUDE[tsql](../../includes/tsql-md.md)]作業。 
 
  
 ### <a name="temporary-tables"></a>暫存資料表
 全域暫存資料表開頭為 # # 不支援。  
  
 本機暫存資料表具有下列限制事項：  
  
-   它們是只對目前的工作階段為可見。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]卸除它們會自動在工作階段的結尾。 若要卸除它們 explicitlt，請使用 DROP TABLE 陳述式。   
-   它們不能重新命名。 
-   它們不能有資料分割或檢視表。  
-   無法變更其權限。 `GRANT``DENY`，和`REVOKE`陳述式不能與本機暫存資料表。   
-   暫存資料表會被鎖定資料庫主控台命令。   
-   如果批次內使用多個本機暫存資料表，則每一個都必須是唯一的名稱。 如果多個工作階段會執行相同的批次並且建立了相同的本機暫存資料表，[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]在內部將數值後置詞附加到本機暫存資料表名稱，以維護每個本機暫存資料表的唯一名稱。  
    
<a name="LockingBehavior"></a>   
## <a name="locking-behavior"></a>鎖定行為  
 在資料表上採用獨佔鎖定。 資料庫、 結構描述，以及 SCHEMARESOLUTION 物件上採用共用的鎖定。  
 

<a name="ExamplesColumn"></a>   
## <a name="examples-for-columns"></a>資料行的範例

### <a name="ColumnCollation"></a> A. 指定資料行定序 
 在下列範例中，資料表`MyTable`建立具有兩個不同的資料行定序。 根據預設，資料行，`mycolumn1`的預設定序 Latin1_General_100_CI_AS_KS_WS。 資料行， `mycolumn2` Frisian_100_CS_AS 定序。  
  
```  
CREATE TABLE MyTable   
  (  
    mycolumnnn1 nvarchar,  
    mycolumn2 nvarchar COLLATE Frisian_100_CS_AS )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
  
```  
  
### <a name="DefaultConstraint"></a> B. 指定資料行的 DEFAULT 條件約束  
 下列範例顯示指定資料行的預設值的語法。 ColA 資料行有預設條件約束命名為 constraint_colA 和預設值為 0。  
  
```  
  
CREATE TABLE MyTable   
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS   
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
```  

<a name="ExamplesTemporaryTables"></a> 
## <a name="examples-for-temporary-tables"></a>暫存資料表的範例

### <a name="TemporaryTable"></a> C. 建立本機暫存資料表  
 下列範例會建立名為 #myTable 本機暫存資料表。 指定的資料表是利用 3 部分名稱。 暫存資料表名稱開頭為 #。   
  
```  
CREATE TABLE AdventureWorks.dbo.#myTable   
  (  
   id int NOT NULL,  
   lastName varchar(20),  
   zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id),  
    CLUSTERED COLUMNSTORE INDEX   
  )  
;  
```

<a name="ExTableStructure"></a>  
## <a name="examples-for-table-structure"></a>資料表結構的範例

### <a name="ClusteredColumnstoreIndex"></a> D. 建立具有叢集資料行存放區索引的資料表  
 下列範例會建立分散式的資料表具有叢集資料行存放區索引。 每個發佈將會儲存為資料行存放區中。  
  
 叢集資料行存放區索引不會影響如何散發資料。資料列永遠已發佈資料。 叢集資料行存放區索引會影響資料儲存在每個發佈的方式。  
  
```  
  
CREATE TABLE MyTable   
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS   
  )  
WITH   
  (   
    DISTRIBUTION = HASH ( colB ),  
    CLUSTERED COLUMNSTORE INDEX   
  )  
;  
```  
 
<a name="ExTableDistribution"></a> 
## <a name="examples-for-table-distribution"></a>資料表發佈的範例

### <a name="RoundRobin"></a> E. 建立 ROUND_ROBIN 資料表  
 下列範例會建立三個資料行與資料分割不 ROUND_ROBIN 資料表。 資料則會分散到所有分佈。 有了叢集資料行存放區索引，可提供較佳的效能和資料壓縮比堆積或資料列存放區叢集索引被建立資料表。  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );  
```  
  
### <a name="HashDistributed"></a> F. 建立雜湊分散式資料表  
 下列範例會建立與上一個範例相同的資料表。 不過，針對這個資料表，資料列散發 (上`id`資料行) 而不是隨機分佈資料表這類的 ROUND_ROBIN。 有了叢集資料行存放區索引，可提供較佳的效能和資料壓縮比堆積或資料列存放區叢集索引被建立資料表。  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id),   
    CLUSTERED COLUMNSTORE INDEX  
  );  
```  
  
### <a name="Replicated"></a> G. 建立複寫的資料表  
 下列範例會建立複寫的資料表類似於先前的範例。 複寫的資料表中完整複製到每個計算節點。 使用此版每個計算節點上時，資料移動會降低查詢。 這個範例會建立具有叢集索引，這可提供更好的資料壓縮比堆積，而且不能包含足夠的資料列，以達成良好的叢集資料行存放區索引壓縮。  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = REPLICATE,   
    CLUSTERED INDEX (lastName)  
  );  
```  

<a name="ExTablePartitions"></a> 
## <a name="examples-for-table-partitions"></a>資料表資料分割的範例

###  <a name="PartitionedTable"></a> H. 建立分割區的資料表  
 下列範例會建立在同一個資料表，加上的 RANGE LEFT 資料分割上的範例 A 中所示`id`資料行。 它會指定四個資料分割的界限值，結果會在五個資料分割。  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH   
  (   
  
    PARTITION ( id RANGE LEFT FOR VALUES (10, 20, 30, 40 )),  
    CLUSTERED COLUMNSTORE INDEX      
  )  
;  
```  
  
 在此範例中，資料的排序至下列分割區：  
  
-   資料分割 1： 資料行 < = 10   
-   資料分割 2: 10 < 資料行 < = 20   
-   資料分割 3: 20 < 資料行 < = 30   
-   資料分割 4: 30 < 資料行 < = 40   
-   分割區 5: 40 < 資料行  
  
 如果這個相同的資料表已分割 RANGE RIGHT，而不是 RANGE LEFT （預設值），資料將會排序成下列分割區：  
  
-   資料分割 1： 資料行 < 10  
-   資料分割 2: 10 < = 資料行 < 20   
-   資料分割 3: 20 < = 資料行 < 30    
-   資料分割 4: 30 < = 資料行 < 40   
-   分割區 5: 40 < = 資料行  
  
### <a name="OnePartition"></a> I. 建立一個磁碟分割的資料分割的資料表  
 下列範例會建立一個磁碟分割的資料分割的資料表。 它並未指定任何界限的值，結果會在一個資料分割。  
  
```  
CREATE TABLE myTable (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH   
    (   
      PARTITION ( id RANGE LEFT FOR VALUES ( )),  
      CLUSTERED COLUMNSTORE INDEX  
    )  
;  
```  
  
### <a name="DatePartition"></a> J. 建立具有日期資料分割的資料表  
 下列範例會建立新的資料表，名為`myTable`中的資料分割上`date`資料行。 藉由使用 RANGE RIGHT 及日期的界限值，它會將一個月的資料放在每個資料分割。  
  
```  
CREATE TABLE myTable (  
    l_orderkey      bigint,       
    l_partkey       bigint,                                             
    l_suppkey       bigint,                                           
    l_linenumber    bigint,        
    l_quantity      decimal(15,2),  
    l_extendedprice decimal(15,2),  
    l_discount      decimal(15,2),  
    l_tax           decimal(15,2),  
    l_returnflag    char(1),  
    l_linestatus    char(1),  
    l_shipdate      date,  
    l_commitdate    date,  
    l_receiptdate   date,  
    l_shipinstruct  char(25),  
    l_shipmode      char(10),  
    l_comment       varchar(44))  
WITH   
  (   
    DISTRIBUTION = HASH (l_orderkey),  
    CLUSTERED COLUMNSTORE INDEX,  
    PARTITION ( l_shipdate  RANGE RIGHT FOR VALUES   
      (  
        '1992-01-01','1992-02-01','1992-03-01','1992-04-01','1992-05-01',
        '1992-06-01','1992-07-01','1992-08-01','1992-09-01','1992-10-01',
        '1992-11-01','1992-12-01','1993-01-01','1993-02-01','1993-03-01',
        '1993-04-01','1993-05-01','1993-06-01','1993-07-01','1993-08-01',
        '1993-09-01','1993-10-01','1993-11-01','1993-12-01','1994-01-01',
        '1994-02-01','1994-03-01','1994-04-01','1994-05-01','1994-06-01',
        '1994-07-01','1994-08-01','1994-09-01','1994-10-01','1994-11-01',
        '1994-12-01'  
      ))
  );  
```  
  
<a name="SeeAlso"></a>    
## <a name="see-also"></a>另請參閱 
 
 [建立 TABLE AS SELECT &#40;Azure SQL 資料倉儲 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
