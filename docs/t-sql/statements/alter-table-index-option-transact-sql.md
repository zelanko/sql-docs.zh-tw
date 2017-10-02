---
title: "index_option (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- index_option
ms.assetid: 8a14f12d-2fbf-4036-b8b2-8db3354e0eb7
caps.latest.revision: 68
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: e7563f9fe992dcf4f9308cccbf11f6310b7925a7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/08/2017

---
# <a name="alter-table-indexoption-transact-sql"></a>ALTER TABLE index_option (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定一組選項可以套用到索引建立使用的條件約束定義的一部分[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
{   
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | SORT_IN_TEMPDB = { ON | OFF }   
  | ONLINE = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = { NONE |ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
      [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
      [ , ...n ] ) ]  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
  
<single_partition_rebuild__option> ::=  
{  
    SORT_IN_TEMPDB = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = {NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE } }  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,   
                           ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )   
}  
```  
  
## <a name="arguments"></a>引數  
 PAD_INDEX  **=**  {ON |**OFF** }  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定索引填補。 預設值為 OFF。  
  
 ON  
 FILLFACTOR 指定的可用空間百分比會套用到索引的中繼層級頁面上。  
  
 關閉或*填滿因數*未指定  
 在中繼頁面上提供索引鍵組之後，中繼層級頁面容量的填滿程度會保留至少足以容納一個資料列的空間，且該資料列的大小上限是索引所能擁有的大小上限。  
  
 填滿因數 **=** *填滿因數*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定一個百分比來指出在建立或改變索引期間，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 應該使各索引頁面之分葉層級填滿的程度。 指定的值必須是 1 至 100 之間的整數值。 預設值是 0。  
  
> [!NOTE]  
>  從各方面來說，填滿因數值 0 和 100 都相同。  
  
 IGNORE_DUP_KEY  **=**  {ON |**OFF** }  
 指定當插入作業嘗試將重複的索引鍵值插入唯一索引時所產生的錯誤回應。 IGNORE_DUP_KEY 選項只適用於在建立或重建索引之後所發生的插入作業。 選項沒有任何作用，執行時[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)， [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)，或[更新](../../t-sql/queries/update-transact-sql.md)。 預設值為 OFF。  
  
 ON  
 重複的索引鍵值插入唯一索引時，就會發生一則警告訊息。 只有違反唯一性條件約束的資料列失敗。  
  
 OFF  
 重複的索引鍵值插入唯一索引時，就會發生的錯誤訊息。 整個 INSERT 作業就會回復。  
  
 在檢視上建立索引、 非唯一索引、 XML 索引、 空間索引和篩選的索引時，無法設定 IGNORE_DUP_KEY 為 ON。  
  
 若要檢視 IGNORE_DUP_KEY，請使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。  
  
 在與舊版本相容的語法中，WITH IGNORE_DUP_KEY 相當於 WITH IGNORE_DUP_KEY = ON。  
  
 STATISTICS_NORECOMPUTE  **=**  {ON |**OFF** }  
 指定是否要重新計算統計資料。 預設值為 OFF。  
  
 ON  
 不會自動重新計算過期的統計資料。  
  
 OFF  
 啟用自動統計資料更新。  
  
 ALLOW_ROW_LOCKS  **=**  { **ON** |OFF}  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定是否允許資料列鎖定。 預設值是 ON。  
  
 ON  
 當存取索引時，允許資料列鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會決定使用資料列鎖定的時機。  
  
 OFF  
 不使用資料列鎖定。  
  
 ALLOW_PAGE_LOCKS  **=**  { **ON** |OFF}  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定是否允許頁面鎖定。 預設值是 ON。  
  
 ON  
 當存取索引時，允許頁面鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會決定使用頁面鎖定的時機。  
  
 OFF  
 不使用頁面鎖定。  
  
 SORT_IN_TEMPDB  **=**  {ON |**OFF** }  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定是否要排序結果儲存在**tempdb**。 預設值為 OFF。  
  
 ON  
 用來建立索引的中繼排序結果會儲存在**tempdb**。 這可能會減少建立索引，如果所需的時間**tempdb**是一組不同的使用者資料庫以外的磁碟上。 不過，這會增加建立索引時所使用的磁碟空間量。  
  
 OFF  
 中繼排序結果會儲存在與用來儲存索引相同的資料庫中。  
  
 線上 **=**  {ON |**OFF** }  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定在索引作業期間，查詢和資料修改是否能夠使用基礎資料表和相關聯的索引。 預設值為 OFF。 REBUILD 可以執行為 ONLINE 作業。  
  
> [!NOTE]  
>  唯一的非叢集索引不能在線上建立。 這包括因 UNIQUE 或 PRIMARY KEY 條件約束而建立的索引。  
  
 ON  
 索引作業持續期間不會保留長期資料表鎖定。 在索引作業的主要階段期間，來源資料表上只保留意圖共用 (IS) 鎖定。 這可使基礎資料表和索引的查詢或更新能夠進行。 在作業開始時，共用 (S) 鎖定會在來源物件上保留一段很短的時間。 在作業結束時，如果正在建立非叢集索引，則有一段短時間會在來源上取得 S (共用) 鎖定；或者，當以線上方式建立或卸除叢集索引時，以及正在重建叢集索引或非叢集索引時，則會取得 SCH-M (結構描述修改) 鎖定。 雖然線上索引鎖定是短暫的中繼資料鎖定，尤其是 Sch-M 鎖定必須等候這個資料表上的所有封鎖交易完成。 在等候期間，Sch-M 鎖定會在存取相同資料表時，封鎖等待在這個鎖定之後的所有其他交易。 建立本機暫存資料表的索引時，ONLINE 不可設為 ON。  
  
> [!NOTE]  
>  線上索引重建可設定*low_priority_lock_wait*本節稍後說明的選項。 *low_priority_lock_wait*在線上索引重建期間管理 S 和 SCH-M 鎖定優先順序。  
  
 OFF  
 在索引作業期間會套用資料表鎖定。 這可防止所有使用者在作業持續期間存取基礎資料表。 建立、重建或卸除叢集索引的離線索引作業，或重建或卸除非叢集索引的離線索引作業，會取得資料表的結構描述修改 (Sch-M) 鎖定。 這可防止所有使用者在作業持續期間存取基礎資料表。 建立非叢集索引的離線索引作業會取得資料表的共用 (S) 鎖定。 這可避免對基礎資料表進行更新，但仍可執行讀取作業，如 SELECT 陳述式。  
  
 如需詳細資訊，請參閱[線上索引作業的運作方式](../../relational-databases/indexes/how-online-index-operations-work.md)。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的所有版本都無法使用線上索引作業。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 MAXDOP  **=**  *max_degree_of_parallelism*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 覆寫**的最大平行處理原則程度**索引作業期間的組態選項。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 請利用 MAXDOP 來限制執行平行計畫所用的處理器數目。 最大值是 64 個處理器。  
  
 *max_degree_of_parallelism*可以是：  
  
 - 1-隱藏平行計畫的產生。  
 - \>1-會限制為指定的數字將平行索引作業所用的處理器數目上限。  
 - 0 （預設）-使用處理器的實際數目或更少根據目前的系統工作負載。  
  
 如需詳細資訊，請參閱 [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
> [!NOTE]  
>  並非每個版本都可使用平行索引作業[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 DATA_COMPRESSION  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 針對指定的資料表、分割區編號或分割區範圍指定資料壓縮選項。 選項如下：  
  
 無  
 不壓縮資料表或指定的分割區。 只適用於資料列存放區資料表，不適用於資料行存放區資料表。  
  
 ROW  
 使用資料列壓縮來壓縮資料表或指定的分割區。 只適用於資料列存放區資料表，不適用於資料行存放區資料表。  
  
 PAGE  
 使用頁面壓縮來壓縮資料表或指定的分割區。 只適用於資料列存放區資料表，不適用於資料行存放區資料表。  
  
 COLUMNSTORE  
 **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 只適用於資料行存放區資料表。 COLUMNSTORE 指定解壓縮之前以 COLUMNSTORE_ARCHIVE 選項壓縮的分割區。 當還原資料時，資料行存放區索引會繼續以用於所有資料行存放區資料表的資料行存放區壓縮。  
  
 COLUMNSTORE_ARCHIVE  
 **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 只適用於資料行存放區資料表，這些資料表會與叢集資料行存放區索引一起儲存。 進一步 COLUMNSTORE_ARCHIVE 壓縮指定的資料分割成較小的大小。 這可用於封存，或是其他需要較少儲存體，而且可負擔更多時間來儲存和擷取的狀況  
  
 如需有關壓縮的詳細資訊，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
在資料分割上**(** {\<編號運算式 > |\<範圍 >}[ **,**... *n*  ] **)** **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定套用 DATA_COMPRESSION 設定的分割區。 如果資料表未分割，ON PARTITIONS 引數會產生錯誤。 如果未提供 ON PARTITIONS 子句，DATA_COMPRESSION 選項會套用至資料分割資料表的所有資料分割。  
  
\<編號運算式 > 可以下列方式指定：  
  
-   提供資料分割的編號，例如：ON PARTITIONS (2)。  
-   為數個個別分割區提供以逗號分隔的分割區編號，例如：ON PARTITIONS (1, 5)。  
-   同時提供範圍和個別分割區，例如：ON PARTITIONS (2, 4, 6 TO 8)。  
  
\<範圍 > 可以指定為資料分割數分隔的例如： ON PARTITIONS (6 TO 8)。  
  
 若要為不同的分割區設定不同類型的資料壓縮，請指定 DATA_COMPRESSION 選項一次以上，例如：  
  
```sql  
--For rowstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
)  
  
--For columnstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = COLUMNSTORE ON PARTITIONS (1, 3, 5),   
DATA_COMPRESSION = COLUMNSTORE_ARCHIVE ON PARTITIONS (2, 4, 6 TO 8)  
)  
```  
  
**\<single_partition_rebuild__option >**  
 在大多數情況下，重建索引會重建資料分割索引的所有資料分割。 下列選項套用到單一資料分割時，不會重建所有資料分割。  
  
-   SORT_IN_TEMPDB  
-   MAXDOP  
-   DATA_COMPRESSION  
  
**low_priority_lock_wait**  
 **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 A**交換器**或線上索引重建完成，因為此資料表沒有封鎖作業。 *WAIT_AT_LOW_PRIORITY*表示，如果**交換器**或線上索引重建作業無法立即完成，它會等候。 作業會保存低優先權鎖定，讓其他鎖定與 DDL 陳述式，繼續進行衝突的作業。 省略**WAIT AT LOW PRIORITY**選項相當於`WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`。  
  
MAX_DURATION =*時間*[**分鐘**]  
 等候時間 （以分鐘為單位的整數值），**交換器**或執行 DDL 命令時，必須取得的線上索引重建鎖定等候。 SWITCH 或線上索引重建作業會嘗試立即完成。 如果操作已遭到封鎖**MAX_DURATION**時間的其中一個**ABORT_AFTER_WAIT**動作執行。 **MAX_DURATION**時間永遠是以分鐘和 word**分鐘**可以省略。  
  
ABORT_AFTER_WAIT = [**NONE** | **自助** | **封鎖**}]  
 無  
 繼續**交換器**或線上索引重建作業，而不變更鎖定優先順序 （使用一般優先順序）。  
  
SELF  
 結束**交換器**或線上索引重建 DDL 作業目前正在執行而不採取任何動作。  
  
BLOCKERS  
 刪除所有目前封鎖的使用者交易**交換器**或線上索引重建 DDL 作業，讓作業可以繼續。  
 封鎖程式需要**ALTER ANY CONNECTION**權限。  
  
## <a name="remarks"></a>備註  
 如需索引選項的完整說明，請參閱[CREATE INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_constraint &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-table-column-constraint-transact-sql.md)   
 [computed_column_definition &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-table-computed-column-definition-transact-sql.md)   
 [table_constraint &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)  
  
 

