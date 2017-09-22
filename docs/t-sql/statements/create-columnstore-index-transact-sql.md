---
title: "建立資料行存放區索引 (TRANSACT-SQL) |Microsoft 文件"
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
- CREATE_COLUMNSTORE_INDEX_TSQL
- COLUMNSTORE INDEX
- COLUMNSTORE_INDEX_TSQL
- CREATE CLUSTERED COLUMNSTORE INDEX
- COLUMNSTORE_TSQL
- CREATE NONCLUSTERED COLUMNSTORE INDEX
- CREATE_NONCLUSTERED_COLUMNSTORE_INDEX_TSQL
- CREATE COLUMNSTORE INDEX
- CREATE_CLUSTERED_COLUMNSTORE_INDEX_TSQL
- COLUMNSTORE
dev_langs:
- TSQL
helpviewer_keywords:
- index creation [SQL Server], columnstore indexes
- columnstore index, creating
- CREATE COLUMNSTORE INDEX statement
- CREATE INDEX statement
ms.assetid: 7e1793b3-5383-4e3d-8cef-027c0c8cb5b1
caps.latest.revision: 76
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: a4e3b602b026d359c7eac492fc44480d4b1a18a9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/21/2017

---

# <a name="create-columnstore-index-transact-sql"></a>CREATE COLUMNSTORE INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

將資料列存放區資料表轉換成叢集資料行存放區索引，或建立非叢集資料行存放區索引。 有效率地對 OLTP 工作負載執行即時作業分析，或是改善資料倉儲工作負載的資料壓縮和查詢效能，請使用資料行存放區索引。  
  
> [!NOTE]  
>  從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，您可以建立資料表作為叢集資料行存放區索引。   不再需要先建立資料列存放區資料表，然後將它轉換成叢集資料行存放區索引。  
  
略過的範例：  
-   [將資料列存放區資料表轉換為資料行存放區範例](../../t-sql/statements/create-columnstore-index-transact-sql.md#convert)  
-   [非叢集資料行存放區索引的範例](../../t-sql/statements/create-columnstore-index-transact-sql.md#nonclustered)  
  
請移至案例：  
-   [資料行存放區索引進行即時作業分析](/sql-docs/docs/relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics)  
-   [資料倉儲的資料行存放區索引](/sql-docs/docs/relational-databases/indexes/columnstore-indexes-data-warehouse)  
  
深入了解：  
-   [資料行存放區索引指南](/sql-docs/docs/relational-databases/indexes/columnstore-indexes-overview)  
-   [資料行存放區索引功能摘要](/sql-docs/docs/relational-databases/indexes/columnstore-indexes-what-s-new)  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create a clustered columnstore index on disk-based table.  
CREATE CLUSTERED COLUMNSTORE INDEX index_name  
    ON [database_name. [schema_name ] . | schema_name . ] table_name  
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ]  
[ ; ]  
  
--Create a non-clustered columnstore index on a disk-based table.  
CREATE [NONCLUSTERED]  COLUMNSTORE INDEX index_name   
    ON [database_name. [schema_name ] . | schema_name . ] table_name   
        ( column  [ ,...n ] )  
    [ WHERE <filter_expression> [ AND <filter_expression> ] ]
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ]   
[ ; ]  
  
<with_option> ::=  
      DROP_EXISTING = { ON | OFF } -- default is OFF  
    | MAXDOP = max_degree_of_parallelism 
    | ONLINE = { ON | OFF } 
    | COMPRESSION_DELAY  = { 0 | delay [ Minutes ] }  
    | DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
      [ ON PARTITIONS ( { partition_number_expression | range } [ ,...n ] ) ]  
  
<on_option>::=  
      partition_scheme_name ( column_name )   
    | filegroup_name   
    | "default"   
  
<filter_expression> ::=  
      column_name IN ( constant [ ,...n ]  
    | column_name { IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !< } constant  
  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE CLUSTERED COLUMNSTORE INDEX index_name   
    ON [ database_name . [ schema_name ] . | schema_name . ] table_name  
    [ WITH ( DROP_EXISTING = { ON | OFF } ) ] --default is OFF  
[;]  
```  
  
## <a name="arguments"></a>引數  
CREATE CLUSTERED COLUMNSTORE INDEX  
建立叢集資料行存放區索引中的所有資料壓縮，然後儲存的資料行。 索引會包括資料表中的所有資料行，而且將儲存整個資料表。 如果現有的資料表是堆積或叢集的索引，資料表會轉換成叢集資料行存放區索引。 如果資料表已儲存為叢集資料行存放區索引中，現有的索引會卸除及重建。  
  
*index_name*  
指定新索引的名稱。  
  
如果資料表有叢集資料行存放區索引，您可以指定相同的名稱為現有的索引，或您可以使用 DROP EXISTING 選項來指定新名稱。  
  
ON [*database_name*。 [*schema_name* ]。 | *schema_name* 。 ] *table_name*  
   指定要儲存為叢集資料行存放區索引之資料表的單部分、兩部分或三部分名稱。 如果資料表是堆積或叢集的索引的資料表會從資料列存放區轉換為資料行存放區。 如果資料表已經是資料行存放區，此陳述式會重建叢集資料行存放區索引。  
  
取代所有提及的  
DROP_EXISTING = [關閉] |ON  
   DROP_EXISTING = ON 指定要卸除現有的叢集資料行存放區索引，並建立新的資料行存放區索引。  

   預設值時，DROP_EXISTING = OFF 必須要有 索引名稱會與現有名稱相同。 為指定的索引名稱已存在時，發生錯誤。  
  
MAXDOP = *max_degree_of_parallelism*  
   在索引作業期間，覆寫現有的「平行處理原則的最大程度」伺服器組態。 請利用 MAXDOP 來限制執行平行計畫所用的處理器數目。 最大值是 64 個處理器。  
  
   *max_degree_of_parallelism*值可以是：  
   - 1 - 隱藏平行計畫的產生。  
   - \>1-限制為指定的數目或更少根據目前的系統工作負載將平行索引作業所用的處理器數目上限。 例如，當 MAXDOP = 4，使用的處理器數目是 4 或更少。  
   - 0 (預設值) - 根據目前的系統工作負載來使用實際數目的處理器或比實際數目更少的處理器。  
  
   如需詳細資訊，請參閱[設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)，和[設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
 
COMPRESSION_DELAY = **0** | *延遲*[分鐘]  
   適用於：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。

   針對以磁碟為基礎的資料表，*延遲*指定 SQL Server 可以壓縮到壓縮的資料列群組之前差異資料列群組中的最小分鐘的時間必須保持在關閉狀態的差異 rowgroup 數目。 因為磁碟基礎的資料表不會追蹤插入和更新時間在個別的資料列，SQL Server 適用於延遲差異資料列群組處於已關閉狀態。  
   預設值是 0 分鐘。  
   如需何時使用 COMPRESSION_DELAY，建議，請參閱[開始使用資料行存放區進行即時作業分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)。  
  
DATA_COMPRESSION = 資料行存放區 |COLUMNSTORE_ARCHIVE  
   適用於：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
針對指定的資料表、分割區編號或分割區範圍指定資料壓縮選項。 選項如下：   
COLUMNSTORE  
   資料行存放區是預設值，並指定要壓縮的大部分的高效能資料行存放區壓縮。 這是典型的選擇。  
  
COLUMNSTORE_ARCHIVE  
   進一步 COLUMNSTORE_ARCHIVE 壓縮資料表或資料分割成較小的大小。 使用此選項的情況下，例如封存，需要較小的儲存體大小，而且可負擔更多時間來儲存和擷取。  
  
   如需有關壓縮的詳細資訊，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  

ON  
   使用 ON 選項可讓您指定資料存放區選項，例如資料分割配置、特定的檔案群組或預設檔案群組。 如果未指定 ON 選項，則索引會使用現有的資料表設定資料分割或檔案群組設定。  
  
   *partition_scheme_name* **(** *column_name* **)**  
   指定資料表的資料分割配置。 資料分割配置必須已存在於資料庫中。 若要建立資料分割配置，請參閱[CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)。  
 
   *column_name*指定針對資料分割的索引的分割區的資料行。 此資料行必須符合資料類型、 長度和有效位數引數的資料分割函式， *partition_scheme_name*使用。  

   *filegroup_name*  
   指定用以儲存叢集資料行存放區索引的檔案群組。 如果未指定位置，且資料表未分割，則索引會使用與基礎資料表或檢視相同的檔案群組。 此檔案群組必須已存在。  

   **「**預設**"**  
   若要在預設檔案群組上建立索引，使用 「 預設 」 或 [default]。  
  
   如果指定了 "default"，目前工作階段的 QUOTED_IDENTIFIER 選項就必須是 ON。 QUOTED_IDENTIFIER 的預設值是 ON。 如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
建立 [非叢集] 資料行存放區索引  
資料列存放區資料表上建立記憶體中非叢集資料行存放區索引儲存為堆積或叢集的索引。 可以有一個篩選的條件並不需要包含基礎資料表的資料行的所有索引。 資料行存放區索引，需要足夠的空間來儲存一份資料。 它是可更新，而且會更新為基礎的資料表已變更。 叢集索引的非叢集資料行存放區索引進行即時分析。  
  
*index_name*  
   指定索引的名稱。 *index_name*必須是唯一在資料表中，但並沒有資料庫內是唯一的。 索引名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。  
  
 **(** *資料行*[ **，**...*n* ] **)**  
    指定要存放的資料行。 非叢集資料行存放區索引僅限於 1024 個資料行。  
   每個資料行必須是資料行存放區索引支援的資料類型。 請參閱[限制事項](../../t-sql/statements/create-columnstore-index-transact-sql.md#LimitRest)如需支援的資料類型的清單。  

ON [*database_name*。 [*schema_name* ]。 | *schema_name* 。 ] *table_name*  
   指定一段、 兩個或三部分名稱，包含索引的資料表。  

WITH DROP_EXISTING = [關閉] |ON  
   DROP_EXISTING = 的 ON 卸除及重建現有的索引。 所指定的索引名稱必須與目前現有的索引相同；不過，索引定義可以修改。 例如，您可以指定不同的資料行或索引選項。
  
   DROP_EXISTING = 的 OFF，如果指定的索引名稱已經存在，會顯示錯誤。 您無法利用 DROP_EXISTING 來變更索引類型。 在與舊版本相容的語法中，WITH DROP_EXISTING 相當於 WITH DROP_EXISTING = ON。  

MAXDOP = *max_degree_of_parallelism*  
   覆寫[設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)索引作業期間的組態選項。 請利用 MAXDOP 來限制執行平行計畫所用的處理器數目。 最大值是 64 個處理器。  
  
   *max_degree_of_parallelism*值可以是：  
   - 1 - 隱藏平行計畫的產生。  
   - \>1-限制為指定的數目或更少根據目前的系統工作負載將平行索引作業所用的處理器數目上限。 例如，當 MAXDOP = 4，使用的處理器數目是 4 或更少。  
   - 0 (預設值) - 根據目前的系統工作負載來使用實際數目的處理器或比實際數目更少的處理器。  
  
   如需詳細資訊，請參閱 [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
> [!NOTE]  
>  並非每個版本都可使用平行索引作業[!INCLUDE[msC](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2016 版本和支援的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
ONLINE = [ON |關閉]   
   適用於： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]，只有非叢集資料行存放區索引中。
在指定的非叢集資料行存放區索引會保持線上狀態，並可用於索引的新複本正在建置。

   關閉指定的索引不是可供使用時正在建立新的複本。 因為這是一個非叢集索引，基底資料表維持可用的狀態，只有非叢集資料行存放區索引不會用來滿足查詢，直到新的索引已完成。 

COMPRESSION_DELAY = **0** | \<延遲 > [分鐘]  
   適用於：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
  
   指定時間長度的資料列應該放在差異資料列群組壓縮資料列群組的移轉之前的下限。 例如，客戶可以說，是否資料列是不變 120 分鐘，讓它符合資格壓縮成單欄式儲存體格式。 磁碟基礎的資料表上的資料行存放區索引，我們不會追蹤的時間，資料列插入或更新，當我們改用差異 rowgroup 關閉時間做為 proxy 的資料列。 預設持續時間是從 0 分鐘。 資料列移轉至單欄式儲存體中，當 1 百萬個資料列已經累積的差異資料列群組，而且它已標示為已關閉。  
  
DATA_COMPRESSION  
   針對指定的資料表、分割區編號或分割區範圍指定資料壓縮選項。 選項如下：  
COLUMNSTORE  
   適用於：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 只適用於資料行存放區索引，包括非叢集資料行存放區索引和叢集資料行存放區索引。 資料行存放區是預設值，並指定要壓縮的大部分的高效能資料行存放區壓縮。 這是典型的選擇。  
  
COLUMNSTORE_ARCHIVE  
   適用於：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
只適用於資料行存放區索引，包括非叢集資料行存放區索引和叢集資料行存放區索引。 進一步 COLUMNSTORE_ARCHIVE 壓縮資料表或資料分割成較小的大小。 這可用於封存，或是其他需要較小儲存體，而且可負擔更多時間來儲存和擷取的狀況。  
  
 如需有關壓縮的詳細資訊，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
其中\<filter_expression > [AND \<filter_expression >] 適用於：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
  
   這稱為篩選器述詞，會指定要在索引中包含的資料列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在篩選索引中的資料列上建立篩選的統計資料。  
  
   篩選器述詞使用簡單比較邏輯。 比較運算子不允許使用 NULL 常值的比較。 請改用 IS NULL 和 IS NOT NULL 運算子。  
  
   下面是一些 `Production.BillOfMaterials` 資料表之篩選述詞的範例：  
   `WHERE StartDate > '20000101' AND EndDate <= '20000630'`    
   `WHERE ComponentID IN (533, 324, 753)`  
   `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
   
   如需篩選的索引上的指引，請參閱[Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)。  
  
ON  
   這些選項會指定建立索引的檔案群組。  
  
*partition_scheme_name* **(** *column_name* **)**  
   指定定義資料分割索引的資料分割會對應到其中的檔案群組的資料分割配置。 資料分割配置必須存在於資料庫中藉由執行[CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)。 
   *column_name*指定針對資料分割的索引的分割區的資料行。 此資料行必須符合資料類型、 長度和有效位數引數的資料分割函式， *partition_scheme_name*使用。 *column_name*未限制為索引定義中的資料行。 對資料行存放區索引進行分割時，如果未指定分割區資料行，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將它新增為索引的資料行。  
   如果*partition_scheme_name*或*檔案群組*未指定和資料表資料分割，此索引會放在相同的資料分割配置，使用相同的分割資料行，做為基礎的資料表。  
   分割資料表的資料行存放區索引必須保持分割區對齊。  
   如需有關資料分割索引的詳細資訊，請參閱[Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。  

*filegroup_name*  
   指定索引建立所在的檔案群組名稱。 如果*filegroup_name*未指定和資料表未分割，則索引會與基礎資料表使用相同的檔案群組。 此檔案群組必須已存在。  
 
**「**預設**"**  
在預設的檔案群組上建立指定的索引。  
  
在這個內容中，default 這個字不是關鍵字。 它是預設檔案群組的識別碼，必須加以分隔，如 ON **"**預設**"**或 ON **[**預設**]**。 如果指定了 "default"，目前工作階段的 QUOTED_IDENTIFIER 選項就必須是 ON。 這是預設值。 如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
##  <a name="Permissions"></a> Permissions  
 需要資料表的 ALTER 權限。  
  
##  <a name="GenRemarks"></a>一般備註  
 在暫存資料表上建立資料行存放區索引。 當資料表卸除或工作階段結束時，也會卸除索引。  
 
## <a name="filtered-indexes"></a>篩選的索引  
已篩選的索引是最佳化的非叢集索引，適用於從資料表選取小型資料列百分比的查詢使用。 它會使用篩選述詞，針對資料表中的部分資料建立索引。 設計良好的已篩選索引可以提升查詢效能、降低儲存成本，並減少維護成本。  
  
### <a name="required-set-options-for-filtered-indexes"></a>需要已篩選之索引的 SET 選項  
每當發生下列任何一個狀況時，都需要必要值資料行中的 SET 選項：  
- 建立已篩選的索引。  
- INSERT、UPDATE、DELETE 或 MERGE 作業修改已篩選之索引中的資料。  
- 篩選的索引用於查詢最佳化工具產生查詢計劃。  
  
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
  
##  <a name="LimitRest"></a> 限制事項  

**資料行存放區索引中的每個資料行必須是下列的一般商務資料類型的其中一個：** 
-   datetimeoffset [( * n * )]  
-   datetime2 [( * n * )]  
-   datetime  
-   smalldatetime  
-   date  
-   時間 [( * n * )]  
-   float [( * n * )]  
-   實際 [( * n * )]  
-   小數 [(*精確度*[ *，標尺*] **)** ]
-   數字 [(*精確度*[ *，標尺*] **)** ]    
-   money  
-   smallmoney  
-   bigint  
-   int  
-   smallint  
-   tinyint  
-   bit  
-   nvarchar [( * n * )] 
-   nvarchar （max) (適用於[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]和 Azure SQL Database premium 定價層，僅限叢集資料行存放區索引中)   
-   nchar [( * n * )]  
-   varchar [( * n * )]  
-   varchar （max) (適用於[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]和 Azure SQL Database premium 定價層，僅限叢集資料行存放區索引中)
-   char [( * n * )]  
-   varbinary [( * n * )] 
-   varbinary (max) (適用於[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]和 Azure SQL Database premium 定價層，僅限叢集資料行存放區索引中)
-   二進位 [( * n * )]  
-   uniqueidentifier (適用於[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]和更新版本)
  
如果基礎資料表的資料行存放區索引不支援資料類型的資料行，必須省略該資料行從非叢集資料行存放區索引。  
  
**使用任何下列資料類型的資料行不能包含在資料行存放區索引：**
-   ntext、text 和 image  
-   nvarchar （max）、 varchar （max） 和 varbinary （max） (適用於[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]和先前版本和非叢集資料行存放區索引) 
-   rowversion (和 timestamp)  
-   sql_variant  
-   CLR 類型 (hierarchyid 和空間類型)  
-   xml  
-   uniqueidentifier (適用於[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])  

**非叢集資料行存放區索引：**
-   不能有 1024 個以上的資料行。  
-   具有非叢集資料行存放區索引的資料表可以有唯一條件約束、主索引鍵條件約束或外部索引鍵條件約束，但是條件約束不得包含在非叢集資料行存放區索引內。  
-   無法在檢視表或索引檢視表上建立。  
-   不能包含疏鬆資料行。  
-   無法變更使用**ALTER INDEX**陳述式。 若要變更非叢集索引，您必須先卸除再重新建立資料行存放區索引。 您可以使用**ALTER INDEX**停用並重建資料行存放區索引。  
-   無法建立使用**INCLUDE**關鍵字。  
-   不能包含**ASC**或**DESC**關鍵字排序索引。 資料行存放區索引是依據壓縮演算法來排序。 遞增或遞減排序會取消許多效能優點。  
-   不能在非叢集資料行存放區索引包含大型物件 (LOB) 資料行類型 nvarchar （max）、 varchar （max），和 varbinary （max）。 只有叢集資料行存放區索引支援 LOB 類型，從[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]版本和 Azure SQL Database 在 premium 定價層設定。 請注意，先前的版本不支援叢集和非叢集資料行存放區索引中的 LOB 類型。


 **資料行存放區索引無法結合下列功能：**  
-   計算資料行。 從 SQL Server 2017，非叢集資料行存放區索引可以包含非保存的計算資料行。 不過，在 SQL Server 2017，叢集資料行存放區索引不能包含保存的計算資料行，而且您不能在計算資料行上的建立非叢集的索引。 
-   Page 和 row 壓縮和**vardecimal**儲存格式 （資料行存放區索引壓縮格式不同。）  
-   複寫  
-   檔案資料流

您無法使用具有叢集資料行存放區索引的資料表上的資料指標或觸發程序。 這項限制不適用於非叢集資料行存放區索引。您可以在具有非叢集資料行存放區索引的資料表上使用資料指標和觸發程序。

**SQL Server 2014 特定限制**  
這些限制僅適用於 SQL Server 2014。 在此版本中，我們引進了可更新的叢集資料行存放區索引。 非叢集資料行存放區索引是仍是唯讀。  

-   變更追蹤。 您無法使用變更追蹤與非叢集資料行存放區索引 (NCCI)，因為它們是唯讀狀態。 它使用叢集資料行存放區索引 (CCI)。  
-   異動資料擷取。 您無法使用的變更資料擷取的非叢集資料行存放區索引 (NCCI)，因為它們是唯讀狀態。 它使用叢集資料行存放區索引 (CCI)。  
-   可讀取的次要複本。 您無法存取叢集的叢集資料行存放區索引 (CCI) 從可讀取次要資料庫一律 OnReadable 可用性群組。  您可以存取的非叢集資料行存放區索引 (NCCI) 從可讀取的次要複本。  
-   Multiple Active Result Sets (MARS)。 SQL Server 2014 使用 MARS 的唯讀連接具有資料行存放區索引的資料表。    不過，SQL Server 2014 不支援 MARS 的資料行存放區索引的資料表上的並行資料操作語言 (DML) 作業。 當發生這種情況時，SQL Server 會終止連線，並中止交易。  
  
 如需的效能優點與限制資料行存放區索引的資訊，請參閱[資料行存放區索引概觀](../../relational-databases/indexes/columnstore-indexes-overview.md)。
  
##  <a name="Metadata"></a> 中繼資料  
 資料行存放區索引中的所有資料行都將儲存於中繼資料內成為內含資料行。 資料行存放區索引沒有索引鍵資料行。 這些系統檢視表提供有關資料行存放區索引的資訊。  
  
-   [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
-   [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
-   [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)  
-   [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
-   [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  

##  <a name="convert"></a>將資料列存放區資料表轉換為資料行存放區範例  
  
### <a name="a-convert-a-heap-to-a-clustered-columnstore-index"></a>A. 將堆積轉換成叢集資料行存放區索引  
 此範例會建立資料表做為堆積，然後將它轉換成名為 cci_Simple 的叢集資料行存放區索引。 這會將整個資料表的儲存體從資料列存放區變更為資料行存放區。  
  
```  
CREATE TABLE SimpleTable(  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_Simple ON SimpleTable;  
GO  
```  
  
### <a name="b-convert-a-clustered-index-to-a-clustered-columnstore-index-with-the-same-name"></a>B. 將叢集索引轉換成具有相同名稱的叢集資料行存放區索引。  
 此範例會建立一個具有叢集索引的資料表，然後示範將叢集索引轉換成叢集資料行存放區索引的語法。 這會將整個資料表的儲存體從資料列存放區變更為資料行存放區。  
  
```  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED INDEX cl_simple ON SimpleTable (ProductKey);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cl_simple ON SimpleTable  
WITH (DROP_EXISTING = ON);  
GO  
```  
  
### <a name="c-handle-nonclustered-indexes-when-converting-a-rowstore-table-to-a-columnstore-index"></a>C. 將資料列存放區資料表轉換成資料行存放區索引時，請處理非叢集索引。  
 這個範例示範如何處理時將資料列存放區資料表轉換為資料行存放區索引的非叢集索引。 實際上，開頭[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]任何特殊的動作是必要項;[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自動定義並重建非叢集索引，針對新的叢集資料行存放區索引。  
  
 如果您想要卸除叢集索引，使用之前建立的資料行存放區索引的 DROP INDEX 陳述式。 卸除現有的選項只會卸除叢集的索引正在轉換。 它不會卸除的非叢集索引。  
  
 在[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，您無法在資料行存放區索引上建立非叢集索引。 這個範例會示範如何在舊版中您需要建立資料行存放區索引之前，請先卸除的非叢集索引。  
  
```  
  
--Create the table for use with this example.  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
  
--Create two nonclustered indexes for use with this example  
CREATE INDEX nc1_simple ON SimpleTable (OrderDateKey);  
CREATE INDEX nc2_simple ON SimpleTable (DueDateKey);   
GO  
  
--SQL Server 2012 and SQL Server 2014: you need to drop the nonclustered indexes  
--in order to create the columnstore index.   
  
DROP INDEX SimpleTable.nc1_simple;  
DROP INDEX SimpleTable.nc2_simple;  
  
--Convert the rowstore table to a columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_simple ON SimpleTable;   
GO  
  
```  
  
### <a name="d-convert-a-large-fact-table-from-rowstore-to-columnstore"></a>D. 將大型事實資料表從資料列存放區轉換成資料行存放區  
 此範例說明如何將大型事實資料表從資料列存放區資料表轉換成資料行存放區資料表。  
  
 若要將資料列存放區資料表轉換成資料行存放區資料表。  
  
1.  首先，建立一個小型資料表以供此範例使用。  
  
    ```  
    --Create a rowstore table with a clustered index and a non-clustered index.  
    CREATE TABLE MyFactTable (  
        ProductKey [int] NOT NULL,  
        OrderDateKey [int] NOT NULL,  
         DueDateKey [int] NOT NULL,  
         ShipDateKey [int] NOT NULL )  
    )  
    WITH (  
        CLUSTERED INDEX ( ProductKey )  
    );  
  
    --Add a non-clustered index.  
    CREATE INDEX my_index ON MyFactTable ( ProductKey, OrderDateKey );  
    ```  
  
2.  卸除資料列存放區資料表中所有的非叢集索引。  
  
    ```  
    --Drop all non-clustered indexes  
    DROP INDEX my_index ON MyFactTable;  
    ```  
  
3.  卸除叢集索引。  
  
    -   只有在您將索引轉換成叢集資料行存放區索引的過程中，想要為索引指定新名稱時才這樣做。 如果無法卸除叢集的索引，新的叢集資料行存放區索引具有相同的名稱。  
  
        > [!NOTE]  
        >  如果您使用自己的索引名稱，可能較容易記住。 所有資料列存放區叢集索引會使用預設名稱，也就是 ' ClusteredIndex_\<GUID >'。  
  
    ```  
    --Process for dropping a clustered index.  
    --First, look up the name of the clustered rowstore index.  
    --Clustered rowstore indexes always use the DEFAULT name ‘ClusteredIndex_<GUID>’.  
    SELECT i.name   
    FROM sys.indexes i   
    JOIN sys.tables t  
    ON ( i.type_desc = 'CLUSTERED' ) WHERE t.name = 'MyFactTable';  
  
    --Drop the clustered rowstore index.  
    DROP INDEX ClusteredIndex_d473567f7ea04d7aafcac5364c241e09 ON MyDimTable;  
    ```  
  
4.  將資料列存放區資料表轉換成具有叢集資料行存放區索引的資料行存放區資料表。  
  
    ```  
    --Option 1: Convert to columnstore and name the new clustered columnstore index MyCCI.  
    CREATE CLUSTERED COLUMNSTORE INDEX MyCCI ON MyFactTable;  
  
    --Option 2: Convert to columnstore and use the rowstore clustered   
    --index name for the columnstore clustered index name.  
    --First, look up the name of the clustered rowstore index.  
    SELECT i.name   
    FROM sys.indexes i  
    JOIN sys.tables t   
    ON ( i.type_desc = 'CLUSTERED' )  
    WHERE t.name = 'MyFactTable';  
  
    --Second, create the clustered columnstore index and   
    --Replace ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
    --with the name of your clustered index.  
    CREATE CLUSTERED COLUMNSTORE INDEX   
    ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
     ON MyFactTable  
    WITH DROP_EXISTING = ON;  
    ```  
  
### <a name="e-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>E. 將資料行存放區資料表轉換成具有叢集索引的資料列存放區資料表。  
 若要將資料行存放區資料表轉換成具有叢集索引的資料列存放區資料表，請使用 CREATE INDEX 陳述式搭配 DROP_EXISTING 選項。  
  
```  
CREATE CLUSTERED INDEX ci_MyTable   
ON MyFactTable  
WITH ( DROP EXISTING = ON );  
```  
  
### <a name="f-convert-a-columnstore-table-to-a-rowstore-heap"></a>F. 將資料行存放區資料表轉換成資料列存放區堆積  
 若要將資料行存放區資料表轉換成資料列存放區堆積，只要卸除叢集資料行存放區索引即可。  
  
```  
DROP INDEX MyCCI   
ON MyFactTable;  
```  
  

### <a name="g-defragment-by-rebuilding-the-entire-clustered-columnstore-index"></a>G. 重建整個叢集資料行存放區索引重組  
   適用於： SQL Server 2014  
  
 有兩種方式可重建完整的叢集資料行存放區索引。 您可以使用 CREATE CLUSTERED COLUMNSTORE INDEX 或[ALTER INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-index-transact-sql.md)和 REBUILD 選項。 這兩種方法會獲得相同的結果。  
  
> [!NOTE]  
>  從 SQL Server 2016 開始，使用 ALTER INDEX REORGANIZE 而不會重建與在此範例中所述的方法。  
  
```  
--Determine the Clustered Columnstore Index name of MyDimTable.  
SELECT i.object_id, i.name, t.object_id, t.name   
FROM sys.indexes i   
JOIN sys.tables t  
ON (i.type_desc = 'CLUSTERED COLUMNSTORE')  
WHERE t.name = 'RowstoreDimTable';  
  
--Rebuild the entire index by using CREATE CLUSTERED INDEX.  
CREATE CLUSTERED COLUMNSTORE INDEX my_CCI   
ON MyFactTable  
WITH ( DROP_EXISTING = ON );  
  
--Rebuild the entire index by using ALTER INDEX and the REBUILD option.  
ALTER INDEX my_CCI  
ON MyFactTable  
REBUILD PARTITION = ALL  
WITH ( DROP_EXISTING = ON );  
  
```  
  
##  <a name="nonclustered"></a>非叢集資料行存放區索引的範例  
  
### <a name="a-create-a-columnstore-index-as-a-secondary-index-on-a-rowstore-table"></a>A. 為次要索引資料列存放區資料表上建立資料行存放區索引  
 此範例會建立非叢集資料行存放區索引的資料列存放區資料表上。 在此情況下，可以建立一個資料行存放區索引。 資料行存放區索引會需要額外的儲存體，因為它包含的資料列存放區資料表中的資料複本。 本範例會建立簡單的資料表和叢集的索引，然後示範建立非叢集資料行存放區索引的語法。  
  
```  
CREATE TABLE SimpleTable  
(ProductKey [int] NOT NULL,   
OrderDateKey [int] NOT NULL,   
DueDateKey [int] NOT NULL,   
ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED INDEX cl_simple ON SimpleTable (ProductKey);  
GO  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey);  
GO  
```  
  
### <a name="b-create-a-simple-nonclustered-columnstore-index-using-all-options"></a>B. 建立簡單的非叢集資料行存放區索引，使用所有選項  
 下列範例示範利用所有選項建立非叢集資料行存放區索引的語法。  
  
```  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey)  
WITH (DROP_EXISTING =  ON,   
    MAXDOP = 2)  
ON "default"  
GO  
```  
  
 如需使用資料分割的資料表更複雜的範例，請參閱[資料行存放區索引概觀](../../relational-databases/indexes/columnstore-indexes-overview.md)。  
  
### <a name="c-create-a-nonclustered-columnstore-index-with-a-filtered-predicate"></a>C. 以篩選述詞建立非叢集資料行存放區索引  
 下列範例會建立已篩選的非叢集資料行存放區索引中的 Production.BillOfMaterials 資料表[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]資料庫。 篩選述詞可以包含在已篩選之索引中不是索引鍵資料行的資料行。 此範例中的述詞只會選取 EndDate 不是 NULL 的資料列。  
  
```  
IF EXISTS (SELECT name FROM sys.indexes  
    WHERE name = N'FIBillOfMaterialsWithEndDate'   
    AND object_id = OBJECT_ID(N'Production.BillOfMaterials'))  
DROP INDEX FIBillOfMaterialsWithEndDate  
    ON Production.BillOfMaterials;  
GO  
CREATE NONCLUSTERED COLUMNSTORE INDEX "FIBillOfMaterialsWithEndDate"  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL;  
  
```  
  
###  <a name="ncDML"></a> D. 變更非叢集資料行存放區索引中的資料  
   適用於：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。
  
 一旦您在資料表上建立非叢集資料行存放區索引，就無法直接修改該資料表中的資料。 使用 INSERT、 UPDATE、 DELETE 或 MERGE 的查詢會失敗，並傳回錯誤訊息。 若要加入或修改資料表中的資料，您可以執行下列其中一項操作：  
  
-   停用或卸除資料行存放區索引。 然後您就可以更新資料表中的資料。 如果您停用資料行存放區索引，您可以在完成更新資料時重建資料行存放區索引。 例如，  
  
    ```  
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;  
    -- update mytable --  
    ALTER INDEX mycolumnstoreindex on mytable REBUILD  
    ```  
  
-   將資料載入未包含資料行存放區索引的暫存資料表。 在暫存資料表上建立資料行存放區索引。 將暫存資料表切換至主資料表的空白分割區。  
  
-   從具有資料行存放區索引的資料表分割區切換至空白的暫存資料表。 如果暫存資料表上有資料行存放區索引，請停用資料行存放區索引。 執行所有更新。 建立 (或重建) 資料行存放區索引。 將暫存資料表切換回 (現在為空白的) 主資料表分割區。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-change-a-clustered-index-to-a-clustered-columnstore-index"></a>A. 將叢集的索引變更為非叢集資料行存放區索引  
 使用 CREATE CLUSTERED COLUMNSTORE INDEX 陳述式 with DROP_EXISTING = ON，您可以：  
  
-   變更叢集的索引插入叢集資料行存放區索引。  
  
-   重建叢集資料行存放區索引。  
  
 本範例會將 xDimProduct 資料表建立資料列存放區資料表具有叢集索引，並再用於建立叢集資料行存放區索引將資料表從資料列存放區資料表變更資料行存放區資料表。  
  
```  
-- Uses AdventureWorks  
  
IF EXISTS (SELECT name FROM sys.tables  
    WHERE name = N'xDimProduct'  
    AND object_id = OBJECT_ID (N'xDimProduct'))  
DROP TABLE xDimProduct;  
  
--Create a distributed table with a clustered index.  
CREATE TABLE xDimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey)  
WITH ( DISTRIBUTION = HASH(ProductKey),  
    CLUSTERED INDEX (ProductKey) )  
AS SELECT ProductKey, ProductAlternateKey, ProductSubcategoryKey FROM DimProduct;  
  
--Change the existing clustered index   
--to a clustered columnstore index with the same name.  
--Look up the name of the index before running this statement.  
CREATE CLUSTERED COLUMNSTORE INDEX <index_name>   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="b-rebuild-a-clustered-columnstore-index"></a>B. 重建叢集資料行存放區索引  
 建置在前面的範例，此範例可以使用 CREATE CLUSTERED COLUMNSTORE INDEX 來重建現有的叢集資料行存放區索引，稱為 cci_xDimProduct。  
  
```  
--Rebuild the existing clustered columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_xDimProduct   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="c-change-the-name-of-a-clustered-columnstore-index"></a>C. 變更叢集資料行存放區索引的名稱  
 若要變更非叢集資料行存放區索引的名稱，請卸除現有的叢集資料行存放區索引，並再重新建立具有新名稱的索引。  
  
 我們建議您只有在這項作業與小型的資料表或空的資料表上執行動作。 它會卸除大型叢集資料行存放區索引和重建使用不同的名稱很長的時間。  
  
 本範例使用 cci_xDimProduct 叢集資料行存放區索引，從先前的範例，卸除 cci_xDimProduct 叢集資料行存放區索引，然後重新建立叢集資料行存放區索引與名稱 mycci_xDimProduct。  
  
```  
--For illustration purposes, drop the clustered columnstore index.   
--The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xDimProduct;  
  
--Create a clustered index with a new name, mycci_xDimProduct.  
CREATE CLUSTERED COLUMNSTORE INDEX mycci_xDimProduct  
ON xdimProduct  
WITH ( DROP_EXISTING = OFF );  
```  
  
### <a name="d-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>D. 將資料行存放區資料表轉換成具有叢集索引的資料列存放區資料表。  
 可能的情況下，您要卸除叢集資料行存放區索引並建立叢集的索引。 這是以資料列存放區格式儲存資料表。 這個範例會將資料行存放區資料表轉換成具有叢集索引具有相同名稱的資料列存放區資料表。 所有資料都會遺失。 所有的資料會移到資料列存放區資料表，並列出的資料行成為叢集索引中的索引鍵資料行。  
  
```  
--Drop the clustered columnstore index and create a clustered rowstore index.   
--All of the columns are stored in the rowstore clustered index.   
--The columns listed are the included columns in the index.  
CREATE CLUSTERED INDEX cci_xDimProduct    
ON xdimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey, WeightUnitMeasureCode)  
WITH ( DROP_EXISTING = ON);  
  
```  
  
### <a name="e-convert-a-columnstore-table-back-to-a-rowstore-heap"></a>E. 將資料行存放區資料表轉換回資料列存放區堆積  
 使用[DROP INDEX (SQL Server PDW)](http://msdn.microsoft.com/en-us/f59cab43-9f40-41b4-bfdb-d90e80e9bf32)卸除叢集資料行存放區索引，並將資料表轉換成資料列存放區堆積。 這個範例會將 cci_xDimProduct 資料表轉換成資料列存放區堆積。 資料表會繼續散發，但是儲存為堆積。  
  
```  
--Drop the clustered columnstore index. The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xdimProduct;  
```  


