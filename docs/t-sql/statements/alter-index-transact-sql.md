---
title: "ALTER INDEX (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER INDEX
- ALTER_INDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- indexes [SQL Server], reorganizing
- ALTER INDEX statement
- indexes [SQL Server], disabling
- online index operations
- index reorganization [SQL Server]
- ALLOW_ROW_LOCKS option
- ALL keyword
- reorganizing indexes
- constraints [SQL Server], indexes
- row locks [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- locking [SQL Server], indexes
- partitioned indexes [SQL Server], rebuilding
- defragmenting indexes
- disabling indexes
- XML indexes [SQL Server], modifying
- index modifications [SQL Server]
- indexes [SQL Server], modifying
- index options [SQL Server]
- modifying indexes
- index disabling [SQL Server]
- MAXDOP index option, ALTER INDEX statement
- spatial indexes [SQL Server], modifying
- indexes [SQL Server], options
- ALLOW_PAGE_LOCKS option
- page locks [SQL Server]
ms.assetid: b796c829-ef3a-405c-a784-48286d4fb2b9
caps.latest.revision: 222
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: f61b6469e40ba303cbff14db9bde15161b225ca7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="alter-index-transact-sql"></a>ALTER INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  藉由停用、重建或重新組織索引或設定索引選項，修改現有的資料表或檢視表索引 (關聯式或 XML)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and SQL Database
  
ALTER INDEX { index_name | ALL } ON <object>  
{  
      REBUILD {  
            [ PARTITION = ALL ] [ WITH ( <rebuild_index_option> [ ,...n ] ) ]   
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> ) [ ,...n ] ]  
      }  
    | DISABLE  
    | REORGANIZE  [ PARTITION = partition_number ] [ WITH ( <reorganize_option>  ) ]  
    | SET ( <set_index_option> [ ,...n ] )   
    | RESUME [WITH (<resumable_index_options>,[…n])]
    | PAUSE
    | ABORT
}  
[ ; ]  
  
<object> ::=   
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
  
<rebuild_index_option > ::=  
{  
      PAD_INDEX = { ON | OFF }  
    | FILLFACTOR = fillfactor   
    | SORT_IN_TEMPDB = { ON | OFF }  
    | IGNORE_DUP_KEY = { ON | OFF }  
    | STATISTICS_NORECOMPUTE = { ON | OFF }  
    | STATISTICS_INCREMENTAL = { ON | OFF }  
    | ONLINE = {   
          ON [ ( <low_priority_lock_wait> ) ]   
        | OFF } 
    | RESUMABLE = { ON | OFF } 
    | MAX_DURATION = <time> [MINUTES}     
    | ALLOW_ROW_LOCKS = { ON | OFF }  
    | ALLOW_PAGE_LOCKS = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | COMPRESSION_DELAY = {0 | delay [Minutes]}  
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }   
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]  
}  
  
<single_partition_rebuild_index_option> ::=  
{  
      SORT_IN_TEMPDB = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | RESUMABLE = { ON | OFF } 
    | MAX_DURATION = <time> [MINUTES}     
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE} }  
    | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<reorganize_option>::=  
{  
       LOB_COMPACTION = { ON | OFF }  
    |  COMPRESS_ALL_ROW_GROUPS =  { ON | OFF}  
}  
  
<set_index_option>::=  
{  
      ALLOW_ROW_LOCKS = { ON | OFF }  
    | ALLOW_PAGE_LOCKS = { ON | OFF }  
    | IGNORE_DUP_KEY = { ON | OFF }  
    | STATISTICS_NORECOMPUTE = { ON | OFF }  
    | COMPRESSION_DELAY= {0 | delay [Minutes]}  
}  

<resumable_index_option> ::=
 { 
    MAXDOP = max_degree_of_parallelism
    | MAX_DURATION =<time> [MINUTES]
    | <low_priority_lock_wait>  
 }
 
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,   
                          ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )  
}  

```  
  
```  
-- Syntax for SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER INDEX { index_name | ALL }  
    ON   [ schema_name. ] table_name  
{  
      REBUILD {  
            [ PARTITION = ALL [ WITH ( <rebuild_index_option> ) ] ] 
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> )] ] 
      }  
    | DISABLE  
    | REORGANIZE [ PARTITION = partition_number ]  
}  
[;]  

<rebuild_index_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]   
}

<single_partition_rebuild_index_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
}  
  
```    
## <a name="arguments"></a>引數  
 *index_name*  
 這是索引的名稱。 在資料表或檢視表內，索引名稱必須是唯一的，但在資料庫內就不一定要是唯一的。 索引名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。  
  
 ALL  
 指定與資料表或檢視表相關聯的所有索引 (不論索引類型為何)。 如果有一個或多個索引在離線或唯讀檔案群組中，或有一個或多個索引類型不允許指定的作業，指定 ALL 便會使陳述式失敗。 下表列出索引作業和不允許的索引類型。  
  
|所有的這項作業使用關鍵字|如果資料表有一個或多個下列項目，便告失敗|  
|----------------------------------------|----------------------------------------|  
|REBUILD WITH ONLINE = ON|XML 索引<br /><br /> 空間索引<br /><br /> 資料行存放區索引：**適用於：** (SQL Server 2012 起） 的 SQL Server 和 Azure SQL Database。|  
|REBUILD PARTITION = |未分割索引、XML 索引、空間索引或停用的索引|  
|REORGANIZE|ALLOW_PAGE_LOCKS 設定為 OFF 的索引|  
|重新組織資料分割 = |未分割索引、XML 索引、空間索引或停用的索引|  
|IGNORE_DUP_KEY = ON|XML 索引<br /><br /> 空間索引<br /><br /> 資料行存放區索引：**適用於：** (SQL Server 2012 起） 的 SQL Server 和 Azure SQL Database。|  
|ONLINE = ON|XML 索引<br /><br /> 空間索引<br /><br /> 資料行存放區索引：**適用於：** (SQL Server 2012 起） 的 SQL Server 和 Azure SQL Database。|
| 可繼續 = ON  | 不支援可繼續索引**所有**關鍵字。 <br /><br /> **適用於**： 開始使用 SQL Server 2017 和 Azure SQL Database （功能處於公開預覽狀態） |   
  
> [!WARNING]
>  如需詳細資訊，可以在線上執行索引作業，請參閱[線上索引作業的指導方針](../../relational-databases/indexes/guidelines-for-online-index-operations.md)。

 如果資料分割指定了 ALL = ，必須對齊所有索引。 這表示它們會根據對等的分割區函數來進行分割。 使用所有的資料分割會導致產生具有相同的所有索引資料分割重建或重新組織。 如需有關分割區索引的詳細資訊，請參閱＜ [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)＞。  
  
 *database_name*  
 這是資料庫的名稱。  
  
 *schema_name*  
 這是資料表或檢視表所屬的結構描述名稱。  
  
 *table_or_view_name*  
 這是與索引相關聯的資料表或檢視表的名稱。 若要顯示物件的索引報表，請使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目錄檢視。  
  
 SQL Database 支援三部分名稱格式 database_name。[schema_name].table_or_view_name 當 database_name 是目前資料庫或 database_name 是 tempdb 和 table_or_view_name 開頭為 #。  
  
 重建 [WITH **(**\<rebuild_index_option 時 > [ **，**...*n*]**)** ]  
 指定將利用相同的資料行、索引類型、唯一性屬性和排序次序來重建索引。 這個子句相當於[DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)。 REBUILD 會啟用停用的索引。 除非指定了 ALL 關鍵字，否則重建叢集索引不會重建相關聯的非叢集索引。 如果未指定索引選項，現有的索引選項中所儲存值[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)會套用。 其值不會儲存在任何索引選項**sys.indexes**，套用的預設格式選項的引數定義中。  
  
 如果指定了 ALL，且基礎資料表是堆積，重建作業便不會影響資料表。 與資料表相關聯的任何非叢集索引都會重建。  
  
 如果資料庫復原模式設為大量記錄模式或簡單模式，重建作業便可以只進行最基本的記錄。  
  
> [!NOTE]
>  當您重建主要 XML 索引時，在索引作業的持續時間，無法使用基礎使用者資料表。  
  
**適用於**: SQL Server （從 SQL Server 2012 開始） 和 Azure SQL Database。
  
 資料行存放區索引，重建作業：  
  
1.  不使用的排序次序。  
  
2.  在進行重建時，取得資料表或分割區上的獨佔鎖定。  在重建期間，資料處於「離線」狀態而且無法使用，即使使用 NOLOCK、RCSI 或 SI 亦然。  
  
3.  將所有資料重新壓縮到資料行存放區。 當重建進行時，有兩個資料行存放區索引複本存在。 當重建完成時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會刪除原始資料行存放區索引。  
  
 如需有關如何重建資料行存放區索引的詳細資訊，請參閱[資料行存放區索引的磁碟重組](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
PARTITION  

**適用於**: SQL Server （從 SQL Server 2008 開始） 和 Azure SQL Database。  
  
 指定只重建或重新組織索引的一個分割區。 如果無法指定分割區*index_name*不是分割區的索引。  
  
 PARTITION = ALL 會重建所有分割區。  
  
> [!WARNING]
>  您可以對包含超過 1,000 個分割區的資料表，建立及重建不以資料表為準的索引，但不予支援。 此做法可能會導致在作業期間效能降低或耗用過多記憶體。 建議當分割區數超過 1,000 時，一律使用以資料表為準的索引。  
  
 *r*  
   
**適用於**: SQL Server （從 SQL Server 2008 開始） 和 Azure SQL Database。
  
 要重建或重新組織之分割區索引的分割區數。 是可以參考變數的常數運算式。 其中包括使用者定義類型變數或函數及使用者定義函數，但無法參考 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 必須存在，或陳述式會失敗。  
  
 與**(**\<single_partition_rebuild_index_option 時 >**)**  
   
**適用於**: SQL Server （從 SQL Server 2008 開始） 和 Azure SQL Database。  
  
 SORT_IN_TEMPDB、 MAXDOP 和 DATA_COMPRESSION 是重建單一分割區時，可以指定的選項 (資料分割 =  *n* )。 不能在單一分割區重建作業中指定 XML 索引。  
  
 DISABLE  
 將索引標示為已停用，無法供 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用。 任何索引都可以停用。 已停用之索引的索引定義會保留在系統目錄中，但不含基礎索引資料。 停用叢集索引可以防止使用者存取基礎資料表資料。 若要啟用索引，請使用 ALTER INDEX REBUILD 或 CREATE INDEX WITH DROP_EXISTING。 如需詳細資訊，請參閱[停用索引和條件約束](../../relational-databases/indexes/disable-indexes-and-constraints.md)和[Enable Indexes and Constraints](../../relational-databases/indexes/enable-indexes-and-constraints.md)。  
  
 重新組織資料列存放區索引  
 資料列存放區索引，重新組織指定若要重新組織索引分葉層級。  重新組織作業為：  
  
-   一律在線上執行。 這表示不會保留長期封鎖的資料表鎖定，而且在 ALTER INDEX REORGANIZE 交易期間，可以繼續查詢或更新基礎資料表。  
  
-   不允許已停用索引  
  
-   ALLOW_PAGE_LOCKS 設為 OFF 時，不允許  
  
-   它在交易內執行，並回復交易時，無法復原。  
  
重新組織與**(**加上 LOB_COMPACTION = { **ON** |關閉} **)**  
 適用於資料列存放區索引。  
  
加上 LOB_COMPACTION = ON  
  
-   指定要壓縮所有包含這些大型物件 (LOB) 資料類型的資料的頁面： image、 text、 ntext、 varchar （max）、 nvarchar （max）、 varbinary （max） 和 xml。 壓縮此資料可以減少在磁碟上的資料大小。  
  
-   為叢集索引，這會壓縮所有包含在資料表的 LOB 資料行。  
  
-   對於非叢集索引，這會壓縮索引中的非索引鍵 （內含） 資料行的所有 LOB 資料行。  
  
-   全部重新組織會加上 LOB_COMPACTION 執行的所有索引。 每個索引，這會壓縮叢集的索引、 基礎資料表或在非叢集索引的內含資料行中的所有 LOB 資料行。  
  
加上 LOB_COMPACTION = 關閉  
  
-   不壓縮包含大型物件資料的頁面。  
  
-   OFF 對堆積沒有作用。  
  
重新組織資料行存放區索引  
REORGANIZE 會線上執行。  
  
資料行存放區索引，重新組織會將每個已關閉的差異資料列群組壓縮到資料行存放區，以壓縮的資料列群組。  
  
-   若要將已關閉的差異資料列群組移至壓縮資料列不需要重新組織。 背景 tuple mover (TM) 處理程序會定期喚醒來壓縮已關閉的差異資料列群組。 我們建議使用 REORGANIZE 時 tuple mover 落後。 重新組織可以更積極地壓縮資料列群組。  
  
-   若要壓縮所有開啟和關閉資料列群組，請參閱本節中的重新組織與 (COMPRESS_ALL_ROW_GROUPS) 選項。  
  
在 SQL Server （從 2016年開始） 和 SQL Database 中的資料行存放區索引，重新組織會執行下列額外的磁碟重組最佳化線上：  
  
-   實際 10%或更多的資料列已以邏輯方式刪除時，請從資料列群組移除資料列。 在實體媒體上回收已刪除的位元組。 例如，假設 1 百萬個資料列壓縮的資料列群組刪除到 100 萬個資料列，SQL Server 將會移除已刪除的資料列，並重新壓縮 900 個 k 資料列與資料列群組。 它會將儲存在存放區透過移除刪除的資料列。  
  
-   結合了以增加每個資料列群組最多 1,024,576 資料列的資料列的一個或多個壓縮資料列。 例如，如果您大量匯入 5 個批次的 102,400 個資料列就會 5 壓縮的資料列。 如果您執行重新組織，這些資料列群組會取得 1 壓縮的資料列群組大小 512,000 資料列的主題合併。 這是假設沒有任何字典的大小或記憶體的限制。  
  
-   資料列群組中的 10%或更多的資料列已以邏輯方式刪除，SQL Server 將嘗試結合一或多個資料列群組中的這個資料列群組。    例如，具有 500,000 個資料列壓縮的資料列群組 1 和 1,048,576 個資料列的最大值與壓縮資料列群組 21。  資料列群組 21 有 60%的已刪除的資料列，讓保持 409,830 資料列。 SQL Server 就會結合這些兩個資料列壓縮新的資料列群組沒有 909,830 資料列群組。  
  
重新組織與 (COMPRESS_ALL_ROW_GROUPS = {ON |**OFF** })  
 在 SQL Server （從 2016年開始） 和 SQL Database，COMPRESS_ALL_ROW_GROUPS 可用來開啟或已關閉差異資料列群組強制資料行存放區。 使用此選項時，不需要重建清空差異資料列群組的資料行存放區索引。  此特性加其他移除和合併磁碟重組功能可讓它不再需要重建索引，在大部分情況下。    
-   ON 會將所有資料列群組強制至資料行存放區，不論大小和狀態 （關閉或開啟）。  
  
-   關閉會強制至資料行存放區的所有 CLOSED 資料列群組。  
  
設定**(** \<set_index 選項 > [ **，**...*n*] **)**  
 在不重建或重新組織索引的情況下，指定索引選項。 停用的索引不能指定 SET。  
  
PAD_INDEX = { ON | OFF }  
   
**適用於**: SQL Server （從 SQL Server 2008 開始） 和 Azure SQL Database。  
  
 指定索引填補。 預設值為 OFF。  
  
 ON  
 FILLFACTOR 指定的可用空間百分比會套用到索引的中繼層級頁面上。 如果 PAD_INDEX 設為 ON，同時不指定 FILLFACTOR 的填滿因數值儲存在[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)用。  
  
 關閉或*填滿因數*未指定  
 填入中繼層級頁面至接近填滿的程度。 這會保留至少足以容納一個資料列的空間，且該資料列具有索引所能擁有的大小上限 (以中繼頁面的索引鍵組為基礎)。  
  
 如需詳細資訊，請參閱 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)。  
  
填滿因數 =*填滿因數*  
 
 **適用於**: SQL Server （從 SQL Server 2008 開始） 和 Azure SQL Database。
  
 指定一個百分比來指出在建立或改變索引期間，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 應該使各索引頁面之分葉層級填滿的程度。 *填滿因數*必須是介於 1 到 100 之間的整數值。 預設值是 0。 填滿因數值 0 和 100 在各方面都是一樣的。  
  
 只有在最初建立或重建索引時，才適用明確的 FILLFACTOR 設定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 不會動態保留頁面中空白空間的指定百分比。 如需詳細資訊，請參閱 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)。  
  
 若要檢視填滿因數設定，請使用**sys.indexes**。  
  
> [!IMPORTANT]
>  利用 FILLFACTOR 值來建立或變更叢集索引時，會影響資料所佔用的儲存空間量，因為 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 在建立叢集索引時，會轉散發資料。  
  
 SORT_IN_TEMPDB = {ON |**OFF** }  
 

**適用於**: SQL Server （從 SQL Server 2008 開始） 和 Azure SQL Database。  
  
 指定是否要排序結果儲存在**tempdb**。 預設值為 OFF。  
  
 ON  
 用來建立索引的中繼排序結果會儲存在**tempdb**。 如果**tempdb**是一組不同的使用者資料庫以外的磁碟，這可能會減少建立索引所需的時間。 不過，這會增加建立索引時所使用的磁碟空間量。  
  
 OFF  
 中繼排序結果會儲存在與用來儲存索引相同的資料庫中。  
  
 如果不需要排序作業，或者可以在記憶體中執行排序，則忽略 SORT_IN_TEMPDB 選項。  
  
 如需詳細資訊，請參閱[索引的 SORT_IN_TEMPDB 選項](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)。  
  
 IGNORE_DUP_KEY  **=**  {ON |OFF}  
 指定當插入作業嘗試將重複的索引鍵值插入唯一索引時所產生的錯誤回應。 IGNORE_DUP_KEY 選項只適用於在建立或重建索引之後所發生的插入作業。 預設值為 OFF。  
  
 ON  
 當重複的索引鍵值插入唯一索引時，就會出現警告訊息。 只有違反唯一性條件約束的資料列才會失敗。  
  
 OFF  
 當重複的索引鍵值插入唯一索引時，就會出現錯誤訊息。 整個 INSERT 作業將會回復。  
  
 在檢視上建立索引、 非唯一索引、 XML 索引、 空間索引和篩選的索引時，無法設定 IGNORE_DUP_KEY 為 ON。  
  
 若要檢視 IGNORE_DUP_KEY，請使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。  
  
 在與舊版本相容的語法中，WITH IGNORE_DUP_KEY 相當於 WITH IGNORE_DUP_KEY = ON。  
  
 STATISTICS_NORECOMPUTE  **=**  {ON |OFF}  
 指定是否要重新計算散發統計資料。 預設值為 OFF。  
  
 ON  
 不會自動重新計算過期的統計資料。  
  
 OFF  
 啟用自動統計資料更新。  
  
 若要還原自動統計資料更新，請將 STATISTICS_NORECOMPUTE 設為 OFF，或執行不含 NORECOMPUTE 子句的 UPDATE STATISTICS。  
  
> [!IMPORTANT]
>  停用散發統計資料的自動重新計算，可防止查詢最佳化工具取得與資料表有關之查詢的最佳執行計畫。  
  
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
  
 
**適用於**: SQL Server （從 SQL Server 2014 開始） 和 Azure SQL Database。  
  
 線上 **=**  {ON |**OFF** }\<在套用至 rebuild_index_option 時 >  
 指定在索引作業期間，查詢和資料修改是否能夠使用基礎資料表和相關聯的索引。 預設值為 OFF。  
  
 如果是 XML 索引或空間索引，則只支援 ONLINE = OFF，而如果將 ONLINE 設定為 ON，將會引發錯誤。  
  
> [!NOTE]
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的所有版本都無法使用線上索引作業。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2016 版本和支援的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ON  
 索引作業持續期間不會保留長期資料表鎖定。 在索引作業的主要階段期間，來源資料表上只保留意圖共用 (IS) 鎖定。 這使得基礎資料表和索引的查詢或更新能夠繼續運作。 在作業開始時，共用 (S) 鎖定會在來源物件上保留一段很短的時間。 在作業結束時，如果建立非叢集索引，S (共用) 鎖定會在來源上保留一段很短的時間；在線上建立或卸除叢集索引時，以及重建叢集或非叢集索引時，將會取得 SCH-M (結構描述修改) 鎖定。 建立本機暫存資料表的索引時，ONLINE 不可設為 ON。  
  
 OFF  
 在索引作業期間會套用資料表鎖定。 建立、重建或卸除叢集索引、空間索引或 XML 索引的離線索引作業，或是重建或卸除非叢集索引的離線索引作業，將會取得資料表的結構描述修改 (Sch-M) 鎖定。 這可防止所有使用者在作業持續期間存取基礎資料表。 建立非叢集索引的離線索引作業會取得資料表的共用 (S) 鎖定。 這可避免對基礎資料表進行更新，但仍可執行讀取作業，如 SELECT 陳述式。  
  
 如需詳細資訊，請參閱[線上索引作業的運作方式](../../relational-databases/indexes/how-online-index-operations-work.md)。  
  
 您可以在線上重建索引，其中包括全域暫存資料表的索引，但下列情況除外：  
  
-   XML 索引  
  
-   本機暫存資料表的索引  
  
-   分割區索引的子集 (可以在線上重建整個分割區索引)。  

-  在 V12 之前的 SQL Database 和 SQL Server 2012 之前, 的 SQL Server 不允許`ONLINE`選項的叢集的索引建立或重建作業，當基底資料表包含**varchar （max)**或**varbinary （max)**資料行。

可繼續 **=**  {ON |**OFF**}

**適用於**： 開始使用 SQL Server 2017 和 Azure SQL Database （功能處於公開預覽狀態）  

 指定的線上索引作業是否為可繼續。

 在索引作業已繼續。

 關閉索引作業會繼續。

MAX_DURATION  **=**  *時間*[**分鐘**] 搭配使用**可繼續 = ON** (需要**ONLINE = ON**).
 
**適用於**： 開始使用 SQL Server 2017 和 Azure SQL Database （功能處於公開預覽狀態）  

表示時間 （以分鐘為單位的整數值） 可繼續線上索引作業之前在暫停執行。 

ALLOW_ROW_LOCKS  **=**  { **ON** |OFF}  
 
**適用於**: SQL Server （從 SQL Server 2008 開始） 和 Azure SQL Database。  
  
 指定是否允許資料列鎖定。 預設值是 ON。  
  
 ON  
 當存取索引時，允許資料列鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會決定使用資料列鎖定的時機。  
  
 OFF  
 不使用資料列鎖定。  
  
ALLOW_PAGE_LOCKS  **=**  { **ON** |OFF}  
  
**適用於**: SQL Server （從 SQL Server 2008 開始） 和 Azure SQL Database。
  
 指定是否允許頁面鎖定。 預設值是 ON。  
  
 ON  
 當您存取索引時，允許頁面鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會決定使用頁面鎖定的時機。  
  
 OFF  
 不使用頁面鎖定。  
  
> [!NOTE]
>  當 ALLOW_PAGE_LOCKS 設為 OFF 時，無法重新組織索引。  
  
 MAXDOP  **=**  max_degree_of_parallelism  
 
**適用於**: SQL Server （從 SQL Server 2008 開始） 和 Azure SQL Database。  
  
 覆寫**的最大平行處理原則程度**索引作業期間的組態選項。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 請利用 MAXDOP 來限制執行平行計畫所用的處理器數目。 最大值是 64 個處理器。  
  
> [!IMPORTANT]
>  雖然所有 XML 索引在語法上都支援 MAXDOP 選項，但是對於空間索引或主要 XML 索引而言，ALTER INDEX 目前只會使用單一處理器。  
  
 *max_degree_of_parallelism*可以是：  
  
 1  
 隱藏平行計畫的產生。  
  
 \>1  
 將平行索引作業所用的最大處理器數目限制為指定的數目。  
  
 0 (預設值)  
 根據目前的系統工作負載，使用實際數目或比實際數目更少的處理器。  
  
 如需詳細資訊，請參閱 [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
> [!NOTE]
>  並非 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每個版本都無法使用平行索引作業。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2016 版本和支援的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 COMPRESSION_DELAY  **=**  { **0** |*持續時間 [分鐘]* }  
 這項功能可從 SQL Server 2016 開始  
  
 針對以磁碟為基礎的資料表，延遲指定分鐘的時間必須保持在關閉狀態的差異資料列群組的最小數目差異資料列群組之前中 SQL Server 可以壓縮到壓縮的資料列群組。 因為磁碟基礎的資料表不會追蹤插入和更新時間在個別的資料列，SQL Server 適用於延遲差異資料列群組處於已關閉狀態。  
預設值是 0 分鐘。  
  
 預設值是 0 分鐘。  
  
 如需有關何時使用 COMPRESSION_DELAY，請參閱資料行存放區索引進行即時作業分析的建議。  
  
 DATA_COMPRESSION  
 針對指定的索引、分割區編號或分割區範圍指定資料壓縮選項。 選項如下：  
  
 無  
 不壓縮索引或指定的分割區。 這不適用於資料行存放區索引。  
  
 ROW  
 使用資料列壓縮來壓縮索引或指定的分割區。 這不適用於資料行存放區索引。  
  
 PAGE  
 使用頁面壓縮來壓縮索引或指定的分割區。 這不適用於資料行存放區索引。  
  
 COLUMNSTORE  
   
**適用於**: SQL Server （從 SQL Server 2014 開始） 和 Azure SQL Database。
  
 只適用於資料行存放區索引，包括非叢集資料行存放區索引和叢集資料行存放區索引。 COLUMNSTORE 會指定解壓縮以 COLUMNSTORE_ARCHIVE 選項壓縮的索引或指定的分割區。 當還原資料時，資料將會繼續以用於所有資料行存放區索引的資料行存放區壓縮來壓縮。  
  
 COLUMNSTORE_ARCHIVE  
  
**適用於**: SQL Server （從 SQL Server 2014 開始） 和 Azure SQL Database。
  
 只適用於資料行存放區索引，包括非叢集資料行存放區索引和叢集資料行存放區索引。 COLUMNSTORE_ARCHIVE 將進一步將指定的分割區壓縮成較小的大小。 這可用於封存，或是其他需要較小儲存體，而且可負擔更多時間來儲存和擷取的狀況。  
  
 如需有關壓縮的詳細資訊，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
 在資料分割上**(** {\<編號運算式 > |\<範圍 >}[**，**… n] **)**  
    
**適用於**: SQL Server （從 SQL Server 2008 開始） 和 Azure SQL Database。 
  
 指定套用 DATA_COMPRESSION 設定的分割區。 如果未分割此索引，ON PARTITIONS 引數將會產生錯誤。 如果未提供 ON PARTITIONS 子句，DATA_COMPRESSION 選項會套用到分割區索引的所有分割區。  
  
 \<編號運算式 > 可以下列方式指定：  
  
-   提供分割區的編號，例如：ON PARTITIONS (2)。  
  
-   為數個個別分割區提供以逗號分隔的分割區編號，例如：ON PARTITIONS (1, 5)。  
  
-   同時提供範圍和個別分割區，例如：ON PARTITIONS (2, 4, 6 TO 8)。  
  
 \<範圍 > 可以指定為資料分割數分隔的例如： ON PARTITIONS (6 TO 8)。  
  
 若要為不同的分割區設定不同類型的資料壓縮，請指定 DATA_COMPRESSION 選項一次以上，例如：  
  
```tsql  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
);  
```  
  
 線上 **=**  {ON |**OFF** }\<在套用至 single_partition_rebuild_index_option 時 >  
 指定線上或離線是否重建索引或基礎資料表的索引資料分割。 如果**重建**線上執行 (**ON**) 這個資料表中的資料可供索引作業期間的查詢和資料修改。  預設值是**OFF**。  
  
 ON  
 索引作業持續期間不會保留長期資料表鎖定。 在索引作業的主要階段期間，來源資料表上只保留意圖共用 (IS) 鎖定。 需要資料表上的 S 鎖定索引重建和 SCH-M 鎖定結尾的線上索引重建資料表上的開頭。 雖然這兩個鎖定是短暫的中繼資料鎖定，尤其是 Sch-M 鎖定必須等候所有封鎖交易完成。 在等候期間，Sch-M 鎖定會在存取相同資料表時，封鎖等待在這個鎖定之後的所有其他交易。  
  
> [!NOTE]
>  線上索引重建可設定*low_priority_lock_wait*本節稍後說明的選項。  
  
 OFF  
 在索引作業期間會套用資料表鎖定。 這可防止所有使用者在作業持續期間存取基礎資料表。  
  
 搭配使用 WAIT_AT_LOW_PRIORITY **ONLINE = ON**只。  
 
**適用於**: SQL Server （從 SQL Server 2014 開始） 和 Azure SQL Database。
  
 線上索引重建必須等候這個資料表的封鎖作業。 **WAIT_AT_LOW_PRIORITY**表示線上索引重建作業將會等候低優先權鎖定，讓其他作業，線上索引建立作業等候時繼續進行。 省略**WAIT AT LOW PRIORITY**選項相當於`WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`。 如需詳細資訊，請參閱[WAIT_AT_LOW_PRIORITY](alter-index-transact-sql.md)。 
  
 MAX_DURATION =*時間*[**分鐘**]  
  
**適用於**: SQL Server （從 SQL Server 2014 開始） 和 Azure SQL Database。
  
 執行 DDL 命令時，線上索引重建鎖定將會以低優先權等候的等候時間 (以分鐘為單位指定的整數值)。 如果操作已遭到封鎖**MAX_DURATION**時間的其中一個**ABORT_AFTER_WAIT**會在執行動作。 **MAX_DURATION**時間永遠是以分鐘和 word**分鐘**可以省略。  
 
 ABORT_AFTER_WAIT = [**NONE** | **自助** | **封鎖**}]  
   
**適用於**: SQL Server （從 SQL Server 2014 開始） 和 Azure SQL Database。
  
 無  
 繼續等候一般 (標準) 優先權的鎖定。  
  
 SELF  
 結束目前正在執行的線上索引重建 DDL 作業，但不採取任何動作。  
  
 BLOCKERS  
 終止封鎖線上索引重建 DDL 作業的所有使用者交易，讓作業可以繼續。 **封鎖**選項需要登入具有**ALTER ANY CONNECTION**權限。  
 
 RESUME 
 
**適用於**： 開頭為 SQL Server 2017 （功能處於公開預覽狀態）

繼續已暫停，以手動方式或因失敗而索引作業。

MAX_DURATION 搭配**可繼續 = ON**

 
**適用於**： 開始使用 SQL Server 2017 和 Azure SQL Database （功能處於公開預覽狀態）

時間 （以分鐘為單位的整數值），可繼續線上索引作業執行之後繼續。 一旦已逾期，如果仍在執行已暫停，可繼續作業。

搭配使用 WAIT_AT_LOW_PRIORITY**可繼續 = ON**和**ONLINE = ON**。  
  
**適用於**： 開始使用 SQL Server 2017 和 Azure SQL Database （功能處於公開預覽狀態）
  
 等候這個資料表的封鎖作業已暫停之後繼續線上索引重建。 **WAIT_AT_LOW_PRIORITY**表示線上索引重建作業將會等候低優先權鎖定，讓其他作業，線上索引建立作業等候時繼續進行。 省略**WAIT AT LOW PRIORITY**選項相當於`WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`。 如需詳細資訊，請參閱[WAIT_AT_LOW_PRIORITY](alter-index-transact-sql.md)。 


PAUSE
 
**適用於**： 開始使用 SQL Server 2017 和 Azure SQL Database （功能處於公開預覽狀態）
  
暫停擱置的線上索引重建作業。

中止

**適用於**： 開始使用 SQL Server 2017 和 Azure SQL Database （功能處於公開預覽狀態）   

中止已宣告為可繼續在執行中或暫停索引作業。 您必須明確地執行**中止**命令終止擱置的索引重建作業。 失敗或暫停繼續索引作業不會終止其執行。相反地，它會使操作無限期暫停狀態。
  
## <a name="remarks"></a>備註  
 ALTER INDEX 無法用來重新進行索引的分割區，或將它移到另一個檔案群組。 您不能利用這個陳述式來修改索引定義，例如新增或刪除資料行，或變更資料行順序。 請搭配 DROP_EXISTING 子句來使用 CREATE INDEX，以執行這些作業。  
  
 未明確指定選項時，會套用目前的設定。 例如，如果 REBUILD 子句並未指定 FILLFACTOR 設定，在重建過程中，會使用系統目錄中所儲存的填滿因數值。 若要檢視目前的索引選項設定，請使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。  
  
> [!NOTE]
>  ONLINE、MAXDOP 和 SORT_IN_TEMPDB 的值並未儲存在系統目錄中。 除非索引陳述式中另有指定，否則會使用選項的預設值。
  
 在多重處理器的電腦上，ALTER INDEX REBUILD 也如同其他查詢一樣，會利用更多處理器來執行與修改索引相關的掃描和排序作業。 當您執行 ALTER INDEX REORGANIZE，具有或不加上 LOB_COMPACTION，**的最大平行處理原則程度**值是單一執行緒的作業。 如需詳細資訊，請參閱 [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
 如果索引所在的檔案群組離線或設為唯讀，便無法重新組織或重建索引。 當指定了 ALL 關鍵字，且有一個或多個索引在離線或唯讀檔案群組中，陳述式會失敗。  
  
## <a name="rebuilding-indexes"></a>重建索引  
 重建索引會卸除和重新建立索引。 這會移除片段；根據指定的或現有的填滿因數設定壓縮頁面來收回磁碟空間，以及重新排序連續頁面中的索引資料列。 當指定 ALL 時，會在單一交易中卸除和重建資料表的所有索引。 不需要事先卸除 FOREIGN KEY 條件約束。 當重建含有 128 個或更多範圍的索引時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會延遲取消配置實際的頁面，也會延遲其關聯鎖定，直到認可交易之後。  
  
 重建或重新組織小型索引通常不會減少片段。 小型索引的頁面有時候會儲存在混合範圍上， 混合範圍最多可由八個物件所共用，所以當重新組織或重建索引之後，小型索引中的片段可能不會減少。  
  
 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始，並不會在建立或重建資料分割索引之後掃描資料表中所有的資料列建立統計資料。 反之，查詢最佳化工具會使用預設的採樣演算法來產生統計資料。 如果要在掃描資料表中所有資料列時取得分割區索引的統計資料，請使用 CREATE STATISTICS 或 UPDATE STATISTICS 搭配 FULLSCAN 子句。  
  
 在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，有時候您可以重建非叢集索引來更正硬體故障所造成的任何不一致情況。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中，您仍可能離線重建非叢集索引來修復索引和叢集索引之間的這類不一致的情況。 不過，您無法利用線上重建索引的方式來修復非叢集索引不一致的情況，因為線上重建機制會以現有的非叢集索引做為重建基礎而保存不一致的情況。 離線時重建索引可能會導致強制掃描叢集索引 (或堆積)，因而移除不一致的情況。 請卸除並重新建立非叢集索引，以確保從叢集索引中重建。 如果要從不一致的情況中復原，在舊版中，我們建議的方法是從備份中還原受影響的資料，不過，您現在可以利用離線重建非叢集索引的方式來修復索引不一致的情況。 如需詳細資訊，請參閱 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)。  
  
 為了重建叢集資料行存放區索引，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會進行以下作業：  
  
1.  在進行重建時，取得資料表或分割區上的獨佔鎖定。 在重建期間，資料處於「離線」狀態而且無法使用。  
  
2.  藉由實際刪除已經以邏輯方式從資料表刪除的資料列，以重組資料行存放區，而已刪除的位元組會在實體媒體上回收。  
  
3.  從原始資料行存放區索引讀取所有資料，包括差異存放區。 這會將資料合併成新的資料列群組，並將資料列群組壓縮到資料行存放區。  
  
4.  進行重建時，實體媒體上需要有空間可儲存資料行存放區索引的兩份副本。 當重建完成時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會刪除原始叢集資料行存放區索引。  
  
## <a name="reorganizing-indexes"></a>重新組織索引  
 重新組織索引所用的系統資源最少。 它會實際重新排序分葉層級的頁面，使它們由左至右符合分葉節點的邏輯順序，以重新組織資料表和檢視表之叢集和非叢集索引的分葉層級。 重新組織也會壓縮索引頁面。 壓縮是以現有填滿因數值為基礎。 若要檢視填滿因數設定，請使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。  
  
 當指定 ALL 時，會重新組織資料表的叢集和非叢集關聯式索引及 XML 索引。 當指定 ALL 時，適用某些限制，請參閱＜引數＞一節中的 ALL 定義。  
  
 如需詳細資訊，請參閱 [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
## <a name="disabling-indexes"></a>停用索引  
 停用索引可防止使用者存取索引，如果是叢集索引，則可防止使用者存取基礎資料表的資料。 索引定義會保留在系統目錄中。 停用檢視的非叢集索引或叢集索引時，會實際刪除索引資料。 停用叢集索引可防止存取資料，資料仍會保留在 B 型樹狀目錄中，但不進行維護，直到卸除或重建索引為止。 若要檢視啟用或停用索引的狀態，請查詢**sys.indexes**中的資料行**sys.indexes**目錄檢視。  
  
 如果資料表在異動複寫發行集中，您便無法停用關聯於主索引鍵資料行的任何索引。 複寫需要這些索引。 若要停用索引，您必須先從發行集中卸除資料表。 如需詳細資訊，請參閱[發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
 請利用 ALTER INDEX REBUILD 陳述式或 CREATE INDEX WITH DROP_EXISTING 陳述式來啟用索引。 當 ONLINE 選項設為 ON 時，無法重建停用的叢集索引。 如需詳細資訊，請參閱 [停用索引和條件約束](../../relational-databases/indexes/disable-indexes-and-constraints.md)。  
  
## <a name="setting-options"></a>設定選項  
 您可以在不重建或重新組織指定之索引的情況下，設定這個索引的 ALLOW_ROW_LOCKS、ALLOW_PAGE_LOCKS、IGNORE_DUP_KEY 和 STATISTICS_NORECOMPUTE 選項。 修改的值會立即套用在索引上。 若要檢視這些設定，請使用**sys.indexes**。 如需詳細資訊，請參閱 [設定索引選項](../../relational-databases/indexes/set-index-options.md)。  
  
### <a name="row-and-page-locks-options"></a>資料列和頁面鎖定選項  
 如果 ALLOW_ROW_LOCKS = ON 且 ALLOW_PAGE_LOCK = ON，當您存取索引時，允許資料列、頁面和資料表層級的鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會選擇適當的鎖定，且可以將鎖定從資料列或頁面鎖定擴大到資料表鎖定。  
  
 如果 ALLOW_ROW_LOCKS = OFF 且 ALLOW_PAGE_LOCK = OFF，當您存取索引時，只允許資料表層級的鎖定。  
  
 如果指定 ALL，且設定了資料列或頁面鎖定，便會將這些設定套用至所有索引上。 當基礎資料表是堆積時，會依照下列方式來套用設定：  
  
|||  
|-|-|  
|ALLOW_ROW_LOCKS = ON 或 OFF|套用在堆積和任何相關聯的非叢集索引上。|  
|ALLOW_PAGE_LOCKS = ON|套用在堆積和任何相關聯的非叢集索引上。|  
|ALLOW_PAGE_LOCKS = OFF|完整套用在非叢集索引上。 這表示在非叢集索引上，不允許所有頁面鎖定。 在堆積上，不允許的鎖定只有頁面的共用 (S)、更新 (U) 和獨佔 (X) 鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 仍能取得意圖頁面鎖定 (IS、IU 或 IX)，供內部使用。|  
  
## <a name="online-index-operations"></a>線上索引作業  
 當重建索引且 ONLINE 選項設為 ON 時，查詢和資料修改可以使用基礎物件、資料表和相關聯的索引。 您也可以在線上重建位於單一分割區之索引的一部分。 在改變過程中，只會在非常短的時間內，保留獨佔的資料表鎖定。  
  
 索引一律是在線上重新組織。 這個過程不會長期保留鎖定，因此，不會封鎖執行中的查詢或更新。  
  
 只有在執行下列動作時，您才能在相同資料表或資料表分割區上執行並行的線上索引作業：  
  
-   建立多個非叢集索引。  
  
-   在相同資料表上重新組織不同的索引。  
  
-   在重建相同資料表的非重疊索引時，重新組織不同的索引。  
  
 同時執行的所有其他線上索引作業都會失敗。 例如，您不能在相同資料表上，同時重建兩個或更多索引，或在相同資料表上重建現有索引時，建立新的索引。  

### <a name="resumable-index-operations"></a>可繼續索引作業

**適用於**： 開始使用 SQL Server 2017 和 Azure SQL Database （功能處於公開預覽狀態）

線上索引重建指定為可繼續使用可繼續 = ON 選項。 
-  可繼續選項在指定索引的中繼資料不會保留且只適用於目前的 DDL 陳述式的持續時間。 因此，可繼續 = ON 子句必須明確指定要啟用 resumability。

-  請注意兩個不同的 MAX_DURATION 選項。 其中一個與 low_priority_lock_wait 相關，且可繼續與其他相關 = ON 選項。
   -  MAX_DURATION 選項支援可繼續 = ON 選項或**low_priority_lock_wait**引數的選項。 
   MAX_DURATION 的繼續選項指定要重建索引的時間間隔。 使用這個時間之後重建索引會暫停，或它完成其執行。 使用者會決定已暫停索引重建可繼續執行。 **時間**MAX_DURATION 的分鐘數必須是大於 0 分鐘且小於或等於一週 （7 x 24 x 60 = 10080 分鐘）。 需要長暫停索引作業可能會影響特定資料表的 DML 效能，以及資料庫的磁碟容量，由於兩部索引原始並新建的一個需要的磁碟空間與需要 DML 作業期間更新。 如果省略了 MAX_DURATION 選項，在索引作業將繼續直到完成或直到發生失敗。 
-   \<Low_priority_lock_wait > 引數選項可讓您決定如何在索引作業可以繼續進行封鎖 SCH-M 鎖定。
 
-  重新執行原始的 ALTER INDEX REBUILD 陳述式具有相同參數，就會繼續已暫停的索引重建作業。 您也可以執行 ALTER INDEX 繼續陳述式，以繼續已暫停的索引重建作業。
-  SORT_IN_TEMPDB = ON 選項不支援可繼續索引 
-  DDL 命令，可繼續與 = ON 無法在明確交易內執行 (不能是一部分 begin tran... 認可區塊）。
-  暫停的索引作業會繼續。
-   當繼續已暫停的索引作業時，您可以變更 MAXDOP 值為新值。  如果未指定 MAXDOP 時繼續暫停的索引作業時，要採取的最後一個 MAXDOP 值。 如果 MAXDOP 選項已完全未指定的索引重建作業，會採取的預設值。
- 若要立即暫停索引作業，您可以停止進行中的命令 (Ctrl + C) 或您可以執行 ALTER INDEX 暫停的命令或在執行 KILL *session_id*命令。 此命令暫停之後繼續使用繼續選項。
-  ABORT 命令刪除裝載原始重建索引和索引作業會中止的工作階段  
-  沒有額外的資源所需的除了可繼續在索引重建
   -    其他所需的空間保留正在建立索引，包括當索引在暫停的時間
   -    防止任何 DDL 修改 DDL 狀態
-  準刪除清除將執行階段索引暫停，但它將會暫停期間執行的索引   
下列功能已停用可繼續索引重建作業
   -    重建已停用的索引不支援可繼續 = ON
   -    ALTER INDEX REBUILD ALL 命令
   -    使用 重建索引的 ALTER TABLE  
   -    DDL 命令與"RESUMEABLE = ON"無法在明確交易內執行 (不能是一部分 begin tran... 認可的區塊）
   -    重建索引對計算或時間戳記資料行做為索引鍵資料行。
-   如果基底資料表包含 LOB 資料行可繼續叢集索引重建需要 SCH-M 鎖定中這項作業的開頭
   -    SORT_IN_TEMPDB = ON 選項不支援可繼續索引 

> [!NOTE]
> DDL 命令執行，直到完成、 暫停或失敗。 此命令會暫停，以免將指出作業已暫停，且索引建立未完成發出錯誤。 目前的索引狀態的詳細資訊可從取得[sys.index_resumable_operations](../../relational-databases/system-catalog-views/sys-index-resumable-operations.md)。 做為前發生失敗時將會發出錯誤以及。 

  
 如需詳細資訊，請參閱 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)。  
  
 ### <a name="waitatlowpriority-with-online-index-operations"></a>WAIT_AT_LOW_PRIORITY 與線上索引作業  
  
 為了執行線上索引重建的 DDL 陳述式，特定資料表上執行的所有使用中封鎖交易都必須完成。 當線上索引重建執行時，它會封鎖這個資料表上準備開始執行的所有新交易。 雖然線上索引重建的鎖定期間很短，但是等候特定資料表上所有未完成的交易完成並封鎖要開始的新交易，可能會大幅影響輸送量，導致工作負載速度變慢或逾時，並且大幅限制對基礎資料表的存取。 **WAIT_AT_LOW_PRIORITY**選項可讓 DBA 管理線上索引重建，並允許它們選取 3 個選項的其中一個所需的 S 鎖定和 SCH-M 鎖定。 在所有 3 的情況下，如果等待時間內 ( `(MAX_DURATION = n [minutes])` )、 有沒有封鎖的活動，線上索引重建會立即執行，而不要等候和 DDL 陳述式已完成。  
  
## <a name="spatial-index-restrictions"></a>空間索引的限制  
 當您重建空間索引時，在索引作業的持續時間，無法使用基礎使用者資料表，因為空間索引會持有結構描述鎖定。  
  
 使用者資料表中的 PRIMARY KEY 條件約束無法在空間索引定義於該資料表的資料行上時，加以修改。 若要變更 PRIMARY KEY 條件約束，請先卸除此資料表的每一個空間索引。 在修改 PRIMARY KEy 條件約束之後，您可以重新建立每一個空間索引。  
  
 在單一分割區重建作業中，您不能指定任何空間索引。 但是，您可以在完整分割區重建中指定空間索引。  
  
 若要變更空間索引特定的選項 (例如 BOUNDING_BOX 或 GRID)，您可以使用指定 DROP_EXISTING = ON 的 CREATE SPATIAL INDEX 陳述式，或是卸除此空間索引並建立新的索引。 如需範例，請參閱 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)中的＜備註＞一節。  
  
## <a name="data-compression"></a>資料壓縮  
 如需資料壓縮的詳細資訊，請參閱 [資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
 若要評估變更 PAGE 和 ROW 壓縮如何會影響的資料表、 索引或分割區，使用[sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md)預存程序。  
  
 下列限制適用於分割區索引：  
  
-   當您使用`ALTER INDEX ALL ...`，您無法變更單一分割區壓縮設定如果資料表有非對齊的索引。  
  
-   ALTER INDEX\<索引 >...REBUILD PARTITION ... 語法會重建此索引的指定資料分割。  
  
-   ALTER INDEX\<索引 >...REBUILD WITH ... 語法會重建此索引的所有資料分割。  
  
## <a name="statistics"></a>Statistics  
 當您執行**ALTER INDEX ALL...** 在資料表中，會更新只與索引統計資料相關聯。 針對資料表 (而非索引) 所建立的自動或手動統計資料不會進行更新。  
  
## <a name="permissions"></a>Permissions  
 若要執行 ALTER INDEX，至少需要資料表或檢視表的 ALTER 權限。  
  
## <a name="version-notes"></a>版本資訊  
  
-   SQL Database 不會使用檔案群組和 filestream 選項。  
  
-   無法使用 SQL Server 2012 之前資料行存放區索引。 

-  可繼續索引作業會從 SQL Server 2017 和 Azure SQL Database （功能處於公開預覽） |   
  
## <a name="basic-syntax-example"></a>基本語法範例：   
  
```tsql 
ALTER INDEX index1 ON table1 REBUILD;  
  
ALTER INDEX ALL ON table1 REBUILD;  
  
ALTER INDEX ALL ON dbo.table1 REBUILD;  
```

## <a name="examples-columnstore-indexes"></a>範例： 資料行存放區索引  
 這些範例會套用至資料行存放區索引。  
  
### <a name="a-reorganize-demo"></a>A. 重新組織示範  
 此範例說明如何使用 ALTER INDEX REORGANIZE 命令。  它會建立具有多個資料列群組，並接著示範如何 REORGANIZE 會合併資料列群組的資料表。  
  
```  
-- Create a database   
CREATE DATABASE [ columnstore ];  
GO  
  
-- Create a rowstore staging table  
CREATE TABLE [ staging ] (  
     AccountKey              int NOT NULL,  
     AccountDescription      nvarchar (50),  
     AccountType             nvarchar(50),  
     AccountCodeAlternateKey     int  
     )  
  
-- Insert 10 million rows into the staging table.   
DECLARE @loop int  
DECLARE @AccountDescription varchar(50)  
DECLARE @AccountKey int  
DECLARE @AccountType varchar(50)  
DECLARE @AccountCode int  
  
SELECT @loop = 0  
BEGIN TRAN  
    WHILE (@loop < 300000)   
      BEGIN  
        SELECT @AccountKey = CAST (RAND()*10000000 as int);  
        SELECT @AccountDescription = 'accountdesc ' + CONVERT(varchar(20), @AccountKey);  
        SELECT @AccountType = 'AccountType ' + CONVERT(varchar(20), @AccountKey);  
        SELECT @AccountCode =  CAST (RAND()*10000000 as int);  
  
        INSERT INTO  staging VALUES (@AccountKey, @AccountDescription, @AccountType, @AccountCode);  
  
        SELECT @loop = @loop + 1;  
    END  
COMMIT  
  
-- Create a table for the clustered columnstore index  
  
CREATE TABLE cci_target (  
     AccountKey              int NOT NULL,  
     AccountDescription      nvarchar (50),  
     AccountType             nvarchar(50),  
     AccountCodeAlternateKey int  
     )  
  
-- Convert the table to a clustered columnstore index named inxcci_cci_target;  
```tsql
CREATE CLUSTERED COLUMNSTORE INDEX idxcci_cci_target ON cci_target;  
```  
  
 使用 TABLOCK 選項來插入資料列以平行方式。 從 SQL Server 2016 開始，在 INSERT INTO 作業可以平行執行時使用 TABLOCK。  
  
```tsql  
INSERT INTO cci_target WITH (TABLOCK) 
SELECT TOP 300000 * FROM staging;  
```  
  
 執行這個命令，請參閱開啟的差異資料列群組。 資料列群組數目取決於平行處理原則程度。  
  
```tsql  
SELECT *   
FROM sys.dm_db_column_store_row_group_physical_stats   
WHERE object_id  = object_id('cci_target');  
```  
  
 執行這個命令，強制將所有已關閉及開啟資料列群組至資料行存放區。  
  
```tsql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
 再次執行此命令，而且您會看到較小的資料列群組會合併成一個壓縮的資料列群組。  
  
```tsql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="b-compress-closed-delta-rowgroups-into-the-columnstore"></a>B. 已關閉的差異資料列群組壓縮至資料行存放區  
 此範例會使用 REORGANIZE 選項來壓縮每個已關閉的差異資料列群組到資料行存放區為壓縮的資料列群組。   這並非必要，但當 tuple mover 無法被壓縮速度夠快，CLOSED 資料列群組時非常有用。  
  
```tsql  
-- Uses AdventureWorksDW  
-- REORGANIZE all partitions  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
  
-- REORGANIZE a specific partition  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0;  
```  
  
### <a name="c-compress-all-open-and-closed-delta-rowgroups-into-the-columnstore"></a>C. 所有開啟和關閉差異資料列群組壓縮至資料行存放區  
 不適用於： SQL Server 2012 和 2014年  
  
 從 SQL Server 2016 開始，您可以執行重新組織與 (COMPRESS_ALL_ROW_GROUPS = ON) 每個開啟和已關閉差異資料列群組壓縮到壓縮的資料列群組資料行存放區。    這會清空差異存放區，並強制取得壓縮成資料行存放區的所有資料列。 這是很有用特別之後執行許多插入作業，因為這些作業在一個或多個差異存放區中儲存資料列。  
  
 REORGANIZE 會結合資料列群組填滿的資料列的最大數目的資料列群組\<= 1,024,576。 因此，壓縮所有開啟和關閉資料列群組時您不會得到很多，其中只有少數資料列壓縮的資料列群組。 您想要盡可能減少壓縮的大小並改善查詢效能為完整的資料列群組。  
  
```tsql  
-- Uses AdventureWorksDW2016  
-- Move all OPEN and CLOSED delta rowgroups into the columnstore.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
  
-- For a specific partition, move all OPEN AND CLOSED delta rowgroups into the columnstore  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0 WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="d-defragment-a-columnstore-index-online"></a>D. 重組資料行存放區索引，線上  
 不適用於： SQL Server 2012 和 2014年。  
  
 從 SQL Server 2016 開始，重新組織沒有多個壓縮差異 rowgroup 成資料行存放區。 它也會執行線上磁碟重組。 首先，它減少資料行存放區的大小 10%或更多資料列群組中的資料列已刪除時，實際移除刪除的資料列。  接著，它會結合資料列群組在一起以形成最多有個 1,024,576 每個資料列群組的資料列的最大值的較大資料列群組。  取得重新壓縮所有資料列群組會變更。  
  
> [!NOTE]
>  從 SQL Server 2016 開始，重建資料行存放區索引已不再需要在大部分情況下因為 REORGANIZE 實際移除刪除的資料列，並將資料列群組合併。 使用 COMPRESS_ALL_ROW_GROUPS 選項會強制所有開啟或已關閉差異資料列群組至其先前只能使用重建資料行存放區。   重新組織在線上，以便讓查詢繼續操作發生，因此會在背景。  
  
```tsql  
-- Uses AdventureWorks  
-- Defragment by physically removing rows that have been logically deleted from the table, and merging rowgroups.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
```  
  
### <a name="e-rebuild-a-clustered-columnstore-index-offline"></a>E. 重建叢集資料行存放區索引的離線  
 適用於： SQL Server 2012、 SQL Server 2014  
  
 啟動 SQL Server 2016，然後在[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，我們建議使用 ALTER INDEX REORGANIZE 而不 ALTER INDEX REBUILD。  
  
> [!NOTE]
>  在 SQL Server 2012 和 2014年中，重新組織僅用於 CLOSED 資料列群組壓縮至資料行存放區。 若要執行磁碟重組作業並強制將所有差異資料列群組至資料行存放區的唯一方式是重建索引。  
  
 這個範例示範如何重建叢集資料行存放區索引，並且強制所有差異資料列群組到資料行存放區。 第一個步驟是準備包含叢集資料行存放區索引的 FactInternetSales2 資料表，並插入前四個資料行的資料。  
  
```tsql  
-- Uses AdventureWorksDW  
  
CREATE TABLE dbo.FactInternetSales2 (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
  
CREATE CLUSTERED COLUMNSTORE INDEX cci_FactInternetSales2  
ON dbo.FactInternetSales2;  
  
INSERT INTO dbo.FactInternetSales2  
SELECT ProductKey, OrderDateKey, DueDateKey, ShipDateKey  
FROM dbo.FactInternetSales;  
  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 結果會顯示沒有一個 OPEN 資料列群組，這表示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]等候再關閉該資料列群組並將資料移至資料行存放區中加入多個資料列。 這個下一個陳述式會重建叢集資料行存放區索引，強制將所有資料列至資料行存放區。  
  
```tsql  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REBUILD;  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 SELECT 陳述式的結果顯示資料列群組為 COMPRESSED，這表示資料列群組的資料行區段現在已壓縮，而且儲存在資料行存放區中。  
  
### <a name="f-rebuild-a-partition-of-a-clustered-columnstore-index-offline"></a>F. 重建叢集資料行存放區索引的離線的分割區  
 它用於： SQL Server 2012、 SQL Server 2014  
  
 若要重建大型叢集資料行存放區索引的分割區，使用 ALTER INDEX REBUILD 與資料分割選項。 這個範例會重建資料分割為 12。 從 SQL Server 2016 開始，我們建議重建取代 REORGANIZE。  
  
```tsql  
ALTER INDEX cci_fact3   
ON fact3  
REBUILD PARTITION = 12;  
```  
  
### <a name="g-change-a-clustered-columstore-index-to-use-archival-compression"></a>G. 變更藉索引來使用封存壓縮  
 不適用於： SQL Server 2012  
  
 您可以選擇使用 COLUMNSTORE_ARCHIVE 資料壓縮選項，以減少更進一步叢集資料行存放區索引的大小。 這是適合您想要保留成本較低的存放裝置上的舊資料。 我們建議您只有使用解壓縮，這通常是因為無法存取的資料設定為低於一般的資料行存放區壓縮。  
  
 下列範例會重建叢集資料行存放區索引來使用封存壓縮，然後示範如何移除封存壓縮。 最後的結果只會使用資料行存放區壓縮。  
  
```tsql  
--Prepare the example by creating a table with a clustered columnstore index.  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL  
);  
  
CREATE CLUSTERED INDEX cci_SimpleTable ON SimpleTable (ProductKey);  
  
CREATE CLUSTERED COLUMNSTORE INDEX cci_SimpleTable  
ON SimpleTable  
WITH (DROP_EXISTING = ON);  
  
--Compress the table further by using archival compression.  
ALTER INDEX cci_SimpleTable ON SimpleTable  
REBUILD  
WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE);  
  
--Remove the archive compression and only use columnstore compression.  
ALTER INDEX cci_SimpleTable ON SimpleTable  
REBUILD  
WITH (DATA_COMPRESSION = COLUMNSTORE);  
GO  
```  
  
## <a name="examples-rowstore-indexes"></a>範例： 資料列存放區索引  
  
### <a name="a-rebuilding-an-index"></a>A. 重建索引  
 下列範例會在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫的 `Employee` 資料表上重建單一索引。  
  
```tsql  
ALTER INDEX PK_Employee_EmployeeID ON HumanResources.Employee REBUILD;  
```  
  
### <a name="b-rebuilding-all-indexes-on-a-table-and-specifying-options"></a>B. 在資料表上重建所有索引以及指定選項  
 下列範例指定 `ALL` 關鍵字。 這樣會重建與 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中 Production.Product 資料表相關聯的所有索引。 指定三個選項。  
  
**適用於**: SQL Server （從 SQL Server 2008 開始） 和 Azure SQL Database。  
  
```tsql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH (FILLFACTOR = 80, SORT_IN_TEMPDB = ON, STATISTICS_NORECOMPUTE = ON);  
```  
  
 下列範例會加入包括低優先權鎖定選項的 ONLINE 選項，並加入資料列壓縮選項。  
  
**適用於**: SQL Server （從 SQL Server 2014 開始） 和 Azure SQL Database。  
  
```tsql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH   
(  
    FILLFACTOR = 80,   
    SORT_IN_TEMPDB = ON,  
    STATISTICS_NORECOMPUTE = ON,  
    ONLINE = ON ( WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 4 MINUTES, ABORT_AFTER_WAIT = BLOCKERS ) ),   
    DATA_COMPRESSION = ROW  
);  
```  
  
### <a name="c-reorganizing-an-index-with-lob-compaction"></a>C. 重新組織具有 LOB 壓縮的索引  
 下列範例會重新組織 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中的單一叢集索引。 由於索引在分葉層級中包含 LOB 資料類型，因此，這個陳述式也會壓縮包含大型物件資料的所有頁面。 請注意，您不需要指定 WITH (LOB_COMPACTION) 選項，因為預設值是 ON。  
  
```tsql  
ALTER INDEX PK_ProductPhoto_ProductPhotoID ON Production.ProductPhoto REORGANIZE WITH (LOB_COMPACTION);  
```  
  
### <a name="d-setting-options-on-an-index"></a>D. 設定索引選項  
 下列範例會設定 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中 `AK_SalesOrderHeader_SalesOrderNumber` 索引的幾個選項。  
  
**適用於**: SQL Server （從 SQL Server 2008 開始） 和 Azure SQL Database。  
  
```tsql  
ALTER INDEX AK_SalesOrderHeader_SalesOrderNumber ON  
    Sales.SalesOrderHeader  
SET (  
    STATISTICS_NORECOMPUTE = ON,  
    IGNORE_DUP_KEY = ON,  
    ALLOW_PAGE_LOCKS = ON  
    ) ;  
GO
```  
  
### <a name="e-disabling-an-index"></a>E. 停用索引  
 下列範例會停用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中 `Employee` 資料表的非叢集索引。  
  
```tsql  
ALTER INDEX IX_Employee_ManagerID ON HumanResources.Employee DISABLE;
```  
  
### <a name="f-disabling-constraints"></a>F. 停用條件約束  
 下列範例會停用 PRIMARY KEY 條件約束停用中的主索引鍵索引[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]資料庫。 基礎資料表的 FOREIGN KEY 條件約束會自動停用，並且會顯示一則警告訊息。  
  
```tsql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department DISABLE;  
```  
  
 結果集會傳回這則警告訊息。  
  
 ```tsql  
 Warning: Foreign key 'FK_EmployeeDepartmentHistory_Department_DepartmentID'  
 on table 'EmployeeDepartmentHistory' referencing table 'Department'  
 was disabled as a result of disabling the index 'PK_Department_DepartmentID'.
 ```  
  
### <a name="g-enabling-constraints"></a>G. 啟用條件約束  
 下列範例會啟用 F 範例所停用的 PRIMARY KEY 和 FOREIGN KEY 條件約束。  
  
 PRIMARY KEY 條件約束是藉由重建 PRIMARY KEY 索引來啟用。  
  
```tsql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department REBUILD;  
```  
  
 然後會啟用 FOREIGN KEY 條件約束。  
  
```tsql  
ALTER TABLE HumanResources.EmployeeDepartmentHistory  
CHECK CONSTRAINT FK_EmployeeDepartmentHistory_Department_DepartmentID;  
GO  
```  
  
### <a name="h-rebuilding-a-partitioned-index"></a>H. 重建分割區索引  
 下列範例會重建 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中分割區索引 `5` 的單一分割區，分割區編號是 `IX_TransactionHistory_TransactionDate`。 分割區 5 在線上重建，而且低優先權鎖定的 10 分鐘等候時間會分別套用至索引重建作業取得的每一個鎖定。 如果在此時間無法取得鎖定來完成索引重建，重建作業陳述式會中止。  
  
**適用於**: SQL Server （從 SQL Server 2014 開始） 和 Azure SQL Database。  
  
```tsql  
-- Verify the partitioned indexes.  
SELECT *  
FROM sys.dm_db_index_physical_stats (DB_ID(),OBJECT_ID(N'Production.TransactionHistory'), NULL , NULL, NULL);  
GO  
--Rebuild only partition 5.  
ALTER INDEX IX_TransactionHistory_TransactionDate  
ON Production.TransactionHistory  
REBUILD Partition = 5   
   WITH (ONLINE = ON (WAIT_AT_LOW_PRIORITY (MAX_DURATION = 10 minutes, ABORT_AFTER_WAIT = SELF)));  
GO  
```  
  
### <a name="i-changing-the-compression-setting-of-an-index"></a>I. 變更索引的壓縮設定  
 下列範例會在非分割資料列存放區資料表上重建索引。  
  
```tsql
ALTER INDEX IX_INDEX1   
ON T1  
REBUILD   
WITH (DATA_COMPRESSION = PAGE);  
GO  
```  
  
 如需其他資料壓縮範例，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
 
### <a name="j-online-resumable-index-rebuild"></a>J. 擱置的線上索引重建

**適用於**： 開始使用 SQL Server 2017 和 Azure SQL Database （功能處於公開預覽狀態）    

 下列範例會示範如何使用擱置的線上索引重建。 

1. 執行線上索引重建以繼續作業與 MAXDOP = 1。

   ```tsql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, MAXDOP=1, RESUMABLE=ON) ;
   ```

2. 執行相同命令一次 （如上述） 索引作業已暫停之後，會繼續自動索引重建作業。

3. 執行線上索引重建為具有 MAX_DURATION 設 240 分鐘一次可繼續作業。

   ```tsql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, RESUMABLE=ON, MAX_DURATION=240) ; 
   ```
4. 暫停繼續執行線上索引重建。

   ```tsql
   ALTER INDEX test_idx on test_table PAUSE ;
   ```   
5. 繼續線上索引重建的索引重建可繼續作業，並指定新值的 MAXDOP 設定為 4 執行。

   ```tsql
   ALTER INDEX test_idx on test_table RESUME WITH (MAXDOP=4) ;
   ```
6. 繼續線上索引重建作業為可繼續執行索引線上重建。 將 MAXDOP 設定為 2、 設定索引 240 分鐘一次，並發生封鎖的鎖定等候 10 分鐘的索引，以 resmumable 正在執行的執行時間和之後，刪除所有封鎖器。 

   ```tsql
      ALTER INDEX test_idx on test_table  
         RESUME WITH (MAXDOP=2, MAX_DURATION= 240 MINUTES, 
         WAIT_AT_LOW_PRIORITY (MAX_DURATION=10, ABORT_AFTER_WAIT=BLOCKERS)) ;
   ```      
7. 中止擱置索引重建作業，也就是執行中或暫停。

   ```tsql
   ALTER INDEX test_idx on test_table ABORT ;
   ``` 
  
## <a name="see-also"></a>另請參閱  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [建立空間索引 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [建立 XML 索引 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [DROP INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [停用索引和條件約束](../../relational-databases/indexes/disable-indexes-and-constraints.md)   
 [XML 索引 &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [線上執行索引作業](../../relational-databases/indexes/perform-index-operations-online.md)   
 [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  



