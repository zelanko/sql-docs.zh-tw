---
title: "資料壓縮 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-data-compression"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "頁面壓縮 [Database Engine]"
  - "索引 [SQL Server], 壓縮"
  - "壓縮索引 [SQL Server]"
  - "儲存壓縮 [Database Engine]"
  - "資料表 [SQL Server], 壓縮"
  - "儲存體 [SQL Server], 壓縮"
  - "壓縮 [SQL Server]"
  - "資料列壓縮 [Database Engine]"
  - "壓縮 [SQL Server], 關於壓縮資料表及索引"
  - "資料壓縮 [Database Engine]"
  - "壓縮資料表 [SQL Server]"
ms.assetid: 5f33e686-e115-4687-bd39-a00c48646513
caps.latest.revision: 60
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 60
---
# 資料壓縮
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 支援資料列和頁面壓縮 (針對資料列存放區的資料表和索引)，亦支援資料行存放區和資料行存放區封存壓縮 (針對資料行存放區的資料表和索引)。  
  
 如果是資料列存放區資料表和索引，使用資料壓縮功能有助於減少資料庫的大小。 除了節省空間之外，資料壓縮也有助於改善 I/O 密集型工作負載的效能，因為資料會儲存在更少的頁面中，而且查詢需要從磁碟讀取的頁面也變少了。 但是在與應用程式交換資料時，資料庫伺服器上需要額外的 CPU 資源來壓縮和解壓縮資料。 您可以針對下列資料庫物件來設定資料列和頁面壓縮：  
  
-   儲存為堆積的整個資料表。  
  
-   儲存為叢集索引的整個資料表。  
  
-   整個非叢集索引。  
  
-   整個索引檢視。  
  
-   如果是分割資料表和索引，您可以針對每個資料分割設定壓縮選項，而物件的不同資料分割則不必擁有相同的壓縮設定。  
  
 如果是資料行存放區資料表和索引，所有資料行存放區資料表和索引一律都使用資料行存放區壓縮，而且使用者無法進行設定。 當您可負擔額外的時間和 CPU 資源來儲存及擷取資料時，使用資料行存放區封存壓縮會進一步減少資料大小。  您可以針對下列資料庫物件來設定資料行存放區封存壓縮：  
  
-   整個資料行存放區資料表或整個叢集資料行存放區索引。  因為資料行存放區資料表會儲存成叢集資料行存放區索引，所以兩種方法有相同的結果。  
  
-   整個非叢集資料行存放區索引。  
  
-   如果是分割資料行存放區資料表和資料行存放區索引，您可以針對每個資料分割設定封存壓縮選項，而不同資料分割則不必擁有相同的封存壓縮設定。  
  
> [!NOTE]  
>  資料也可以使用 GZIP 演算法格式進行壓縮。 這是額外的步驟，最適合在封存舊資料進行長期儲存時壓縮部分資料。 使用 COMPRESS 函數壓縮的資料無法編製索引。 如需詳細資訊，請參閱 [COMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/compress-transact-sql.md)。  
  
## 使用資料列和頁面壓縮時的考量  
 當您使用資料列和頁面壓縮時，請注意以下考量事項：  
  
-   Service Pack 或後續版本中的資料壓縮詳細資料可能會變更，恕不另行通知。

-   壓縮適用於： [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]  
  
-   每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中都無法使用壓縮。 如需詳細資訊，請參閱 [SQL Server 2016 版本支援的功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)。  
  
-   壓縮不適用於系統資料表。  
  
-   壓縮可讓更多的資料列儲存在頁面上，但是不會變更資料表或索引的資料列大小上限。  
  
-   當資料列大小上限加上壓縮負擔超過 8060 個位元組的資料列大小上限時，資料表將無法啟用壓縮。 例如，因為有額外的壓縮負荷，所以無法壓縮具有資料行 c1**char(8000)** 及 c2**char(53)** 的資料表。 當使用 Vardecimal 儲存格式時，將會在啟用此格式時執行資料列大小檢查。 對於資料列和頁面壓縮而言，最初壓縮物件時會執行資料列大小檢查，然後在插入或修改每一個資料列時加以檢查。 壓縮會強制執行下列兩個規則：  
  
    -   固定長度類型的更新一定要成功。  
  
    -   停用資料壓縮一定要成功。 即使壓縮的資料列適合頁面大小，這表示它小於 8060 個位元組；如果它未壓縮， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會防止不適合資料列大小的更新。  
  
-   當指定了資料分割清單時，壓縮類型可以在個別資料分割上設定為 ROW、PAGE 或 NONE。 如果未指定資料分割的清單，將會設定所有資料分割，並包含陳述式中所指定的資料壓縮屬性。 在建立資料表或索引時，除非另外指定，否則資料壓縮會設定為 NONE。 在修改資料表時，除非另外指定，否則會保留現有的壓縮。  
  
-   如果您指定資料分割清單或超出範圍的資料分割，將會產生錯誤。  
  
-   非叢集索引不會繼承資料表的壓縮屬性。 若要壓縮索引，您必須明確設定索引的壓縮屬性。 根據預設，當建立索引時，索引的壓縮設定將會設定為 NONE。  
  
-   在堆積上建立叢集索引時，此叢集索引會繼承堆積的壓縮狀態，除非指定了替代的壓縮狀態。  
  
-   當堆積設定了頁面層級壓縮時，頁面只會以下列方式接收頁面層級壓縮：  
  
    -   資料會在啟用大量最佳化的情況下大量匯入。  
  
    -   使用 INSERT INTO ...WITH (TABLOCK) 語法與資料表沒有非叢集索引。  
  
    -   執行 ALTER TABLE ...REBUILD 陳述式並指定 PAGE 壓縮選項來重建資料表。  
  
-   重建堆積之前，配置在堆積中成為 DML 作業一部分的新頁面將不會使用 PAGE 壓縮。 您可以透過移除並重新套用壓縮，或建立並移除叢集索引，重建堆積。  
  
-   變更堆積的壓縮設定需要重建資料表上的所有非叢集索引，好讓它們擁有指向堆積內新資料列位置的指標。  
  
-   您可以在線上或離線時啟用或停用 ROW 或 PAGE 壓縮。 在堆積上啟用壓縮對於線上作業而言是單一執行緒的作業。  
  
-   啟用或停用資料列或頁面壓縮的磁碟空間需求與建立或重建索引的需求相同。 對於分割的資料而言，您可以一次啟用或停用一個資料分割的壓縮來減少所需的空間。  
  
-   若要決定資料分割資料表中資料分割的壓縮狀態，請查詢 sys.partitions 目錄檢視的 data_compression 資料行。  
  
-   當您壓縮索引時，可以在壓縮資料列和頁面的情況下壓縮分葉層級頁面。 非分葉層級頁面不會收到頁面壓縮。  
  
-   由於大數值資料類型的大小之緣故，這些類型有時會單獨儲存在特殊用途的頁面上，與一般資料列的資料分開。 資料壓縮不適用於個別儲存的資料。  
  
-   在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中實作 Vardecimal 儲存格式的資料表將會在升級時保留此設定。 您可以將資料列壓縮套用到具有 Vardecimal 儲存格式的資料表。 但是，由於資料列壓縮是 Vardecimal 儲存格式的超集，所以沒有理由保留 Vardecimal 儲存格式。 當您將 Vardecimal 儲存格式結合資料列壓縮時，十進位值不會取得額外的壓縮。 您可以將頁面壓縮套用到具有 Vardecimal 儲存格式的資料表；但是，Vardecimal 儲存格式資料行可能不會封存其他壓縮。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支援 Vardecimal 儲存格式；但是，由於資料列層級的壓縮會達成相同的目標，所以 Vardecimal 儲存格式已被取代。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## 使用資料行存放區和資料行存放區封存壓縮  
  
||  
|-|  
|**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至[目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))、[!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]。|  
  
### 基本概念  
 資料行存放區資料表和索引永遠都會以資料行存放區壓縮形式來儲存。 您可以進一步減少資料行存放區資料的大小，只要設定稱為封存壓縮的額外壓縮即可。  為了執行封存壓縮， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對資料執行 Microsoft XPRESS 壓縮演算法。 您可以使用下列資料壓縮類型來新增或移除封存壓縮：  
  
-   使用 **COLUMNSTORE_ARCHIVE** 資料壓縮，以封存壓縮來壓縮資料行存放區的資料。  
  
-   使用 **COLUMNSTORE** 資料壓縮，將封存壓縮解壓縮。 這樣產生的資料將會持續以資料行存放區壓縮形式壓縮。  
  
 若要新增封存壓縮，請使用 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) 或 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) 搭配 REBUILD 選項和 DATA COMPRESSION = COLUMNSTORE。  
  
 範例:  
  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE ON PARTITIONS (2,4)) ;  
  
```  
  
 若要移除封存壓縮並將資料還原成資料行存放區壓縮，請使用 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) 或 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) 搭配 REBUILD 選項和 DATA COMPRESSION = COLUMNSTORE。  
  
 範例:  
  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE ON PARTITIONS (2,4) ) ;  
  
```  
  
 下一個範例會在某些資料分割上將資料壓縮設定為資料行存放區，以及在其他資料分割上設定為資料行存放區封存。  
  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (  
    DATA_COMPRESSION =  COLUMNSTORE ON PARTITIONS (4,5),  
    DATA COMPRESSION = COLUMNSTORE_ARCHIVE ON PARTITIONS (1,2,3)  
) ;  
```  
  
### 效能  
 以封存壓縮壓縮資料行存放區索引將會造成該索引的效能比沒有封存壓縮的資料行存放區索引還要慢。  只有當您可以負擔使用額外時間和 CPU 資源來壓縮及擷取資料時，才使用封存壓縮。  
  
 效能減緩的好處就是減少儲存體，這對於不常存取的資料很實用。 例如，如果您每個月的資料都有一個資料分割，而您的大多數活動發生在最近的月份，您可以封存較舊的月份來減少儲存需求。  
  
### 中繼資料  
 下列系統檢視表包含叢集索引之資料壓縮的相關資訊：  
  
-   [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) - **type** 及 **type_desc** 資料行包含 CLUSTERED COLUMNSTORE 和 NONCLUSTERED COLUMNSTORE。  
  
-   [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) – **data_compression** 及 **data_compression_desc** 資料行包含 COLUMNSTORE 和 COLUMNSTORE_ARCHIVE。  
  
 [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) 程序不適用於資料行存放區索引。  
  
## 壓縮對分割資料表和索引有何影響  
 當您搭配分割資料表和索引使用資料壓縮時，請注意以下考量事項：  
  
-   當使用 ALTER PARTITION 陳述式分割資料分割時，兩個資料分割都會繼承原始資料分割的資料壓縮屬性。  
  
-   當合併兩個資料分割時，所產生的資料分割會繼承目標資料分割的資料壓縮屬性。  
  
-   若要切換資料分割，此資料分割的資料壓縮屬性必須符合資料表的壓縮屬性。  
  
-   您可以使用兩種語法變化來修改分割資料表或索引的壓縮：  
  
    -   下列語法只會重建參考的資料分割：  
  
        ```  
        ALTER TABLE <table_name>   
        REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  <option>)  
        ```  
  
    -   下列語法會將現有的壓縮設定用於任何未參考的資料分割，藉以重建整個資料表：  
  
        ```  
        ALTER TABLE <table_name>   
        REBUILD PARTITION = ALL   
        WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(<range>),  
        ... )  
        ```  
  
     分割索引會遵循使用 ALTER INDEX 的相同原則。  
  
-   當卸除叢集索引時，除非修改了資料分割配置，否則對應的堆積資料分割會保留其資料壓縮設定。 如果資料分割配置有所變更，所有資料分割都會重建為未壓縮的狀態。 若要卸除叢集索引及變更資料分割配置，您需要執行以下步驟：  
  
     1. 卸除叢集索引。  
  
     2. 使用指定壓縮選項的 ALTER TABLE ...REBUILD ... 選項來修改資料表。  
  
     在線上卸除叢集索引將會是非常快速的作業，因為只會移除叢集索引的上層。 在線上卸除叢集索引時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須重建堆積兩次，一次在步驟 1，另一次在步驟 2。  
  
## 壓縮將如何影響複寫 
||  
|-|  
|**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至[目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|   
 當您搭配複寫使用資料壓縮時，請注意以下考量事項：  
  
-   當快照集代理程式產生最初的結構描述指令碼時，新的結構描述會將相同的壓縮設定用於資料表和它的索引。 不能只在資料表上啟用壓縮，而不在索引上啟用壓縮。  
  
-   如果是異動複寫，發行項結構描述選項會判斷哪些相依的物件和屬性必須編寫指令碼。 如需詳細資訊，請參閱 [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。  
  
     散發代理程式在套用指令碼時，不會檢查是否有下層的訂閱者。 如果選取了壓縮的複寫，在下層訂閱者上建立資料表將會失敗。 如果是混合拓撲，請勿啟用壓縮的複寫。  
  
-   如果是合併式複寫，發行集相容性層級會覆寫結構描述選項，並判斷將要編寫指令碼的結構描述物件。  
  
     在混合拓撲的情況下，如果它不必支援新的壓縮選項，則發行集相容性層級應該設定為下層的訂閱者版本。 如果需要的話，請於建立資料表之後在訂閱者上壓縮資料表。  
  
 下表顯示在複寫期間控制壓縮的複寫設定。  
  
|使用者意圖|複寫資料表或索引的資料分割配置|複寫壓縮設定|指令碼行為|  
|-----------------|-----------------------------------------------------|------------------------------------|------------------------|  
|複寫資料分割配置，以及在資料分割的訂閱者上啟用壓縮。|True|True|同時針對資料分割配置和壓縮設定編寫指令碼。|  
|複寫資料分割配置，但是不壓縮訂閱者上的資料。|True|False|針對資料分割配置編寫指令碼，但是不針對資料分割的壓縮設定編寫指令碼。|  
|不複寫資料分割配置，而且不壓縮訂閱者上的資料。|False|False|不針對資料分割或壓縮設定編寫指令碼。|  
|如果所有資料分割都在發行者上壓縮，則壓縮訂閱者上的資料表，但是不複寫資料分割配置。|False|True|檢查所有資料分割是否啟用壓縮。<br /><br /> 針對資料表層級上的壓縮編寫指令碼。|  
  
## 壓縮對於其他 SQL Server 元件有何影響 
||  
|-|  
|**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至[目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|
   
 壓縮會發生在儲存引擎中，而且資料會以非壓縮狀態呈現給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的大多數其他元件。 這樣會將壓縮對其他元件的影響限制為以下情況：  
  
-   大量匯入及匯出作業  
  
     當匯出資料時 (即使是原生格式)，資料為非壓縮資料列格式的輸出。 這可能會造成匯出的資料檔大小比來源資料大出許多。  
  
     當匯入資料時，如果目標資料表已啟用壓縮，則儲存引擎會將資料轉換成壓縮的資料列格式。 這樣可能會造成 CPU 使用量增加 (相較於資料匯入未壓縮的資料表時)。  
  
     將資料大量匯入具有頁面壓縮的堆積內時，大量匯入作業會在插入具有頁面壓縮的資料時，嘗試壓縮這些資料。  
  
-   壓縮不會影響備份和還原。  
  
-   壓縮不會影響記錄傳送。  
  
-   資料壓縮與疏鬆資料行不相容。 因此，包含疏鬆資料行的資料表無法加以壓縮，也無法將疏鬆資料行加入至壓縮的資料表。  
  
-   啟用壓縮可能會造成查詢計畫變更，因為系統會使用不同的頁數以及每頁不同的資料列數來儲存資料。  
  
## 另請參閱  
 [資料列壓縮實作](../../relational-databases/data-compression/row-compression-implementation.md)   
 [頁面壓縮實作](../../relational-databases/data-compression/page-compression-implementation.md)   
 [Unicode 壓縮實作](../../relational-databases/data-compression/unicode-compression-implementation.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
  