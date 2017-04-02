---
title: "資料行存放區索引資料載入 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b29850b5-5530-498d-8298-c4d4a741cdaf
caps.latest.revision: 31
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 28
---
# 資料行存放區索引資料載入
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  使用標準 SQL 大量載入將資料載入資料行存放區索引，然後慢慢插入方法。 這些方法包括 bcp、Integration Services 以及 Transact-SQL merge 或 insert 陳述式。  
  
 資料行存放區索引的新手嗎？ 請檢閱[資料行存放區索引指南](../Topic/Columnstore%20Indexes%20Guide.md)中的詞彙與概念。  
  
 需要深入討論嗎？ 請參閱此 [部落格文章](http://blogs.msdn.com/b/sqlcat/archive/2015/03/11/data-loading-performance-considerations-on-tables-with-clustered-columnstore-index.aspx)。  
  
##  <a name="dataload_cci"></a> 大量載入叢集資料行存放區索引  
 若要將資料列大量載入叢集資料行存放區索引，可以使用 bcp 命令列工具、Integration Services，或從暫存表格選取資料列。  
  
 ![載入叢集資料行存放區索引中](../../relational-databases/indexes/media/sql-server-pdw-columnstore-loadprocess.gif "載入叢集資料行存放區索引中")  
  
 如圖所示，大量載入︰  
  
1.  不會預先排序資料。 資料會以收到的順序插入資料列群組。  
  
2.  如果批次大小 > = 102400，資料列會直接進入壓縮的資料列群組。 建議選擇批次大小 > = 102400 進行有效率的大量匯入，因為在由背景執行緒、Tuple Mover (TM) 最終將資料列移至壓縮的資料列群組之前，可避免資料移到差異資料列群組中。  
  
3.  如果批次大小 < 102400 或剩餘的資料列 < 102400，資料列就會載入差異資料列群組。  
  
 大量載入叢集資料行存放區索引具備下列可用的最佳化方式  
  
-   平行載入︰您可以執行多個並行大量匯入 (bcp 或大量插入)，而同時每項作業載入不同的資料檔案。 與資料列存放區不同的是，您不需要指定 TABLOCK，這是因為每個大量匯入執行緒都會專門將資料載入不同的資料列群組 (壓縮或差異資料列群組)，且對其具有獨占鎖定。   使用 TABLOCK 會在資料表上強制進行獨佔鎖定，而您無法以平行方式匯入資料。  
  
-   記錄最佳化︰將資料載入壓縮的資料列群組時，大量載入會記錄最少的內容。 當資料載入批次大小 < 102400 的差異資料列群組時，沒有最低限度記錄。  
  
-   鎖定最佳化︰載入壓縮資料列群組時，會取資料列群組的 X 鎖定。 然而，當大量載入差異資料列群組時，已取得資料列群組的 X 鎖定，但 SQL Server 仍會鎖定「頁/範圍」的鎖定，這是因為 X 資料列群組鎖定不是鎖定階層的一部分。  
  
 如果您有非叢集索引或有多個非叢集索引，對於索引本身而言，不會有任何鎖定或記錄最佳化，但仍然會有如上所述的叢集資料行存放區索引最佳化。  
  
## 差異存放區的運作方式  
 叢集資料行存放區索引在將資料列壓縮到壓縮的資料列群組之前，在差異存放區中最多可收集 1,048,576 個資料列。 如此可改善資料行存放區索引的壓縮。 當差異存放區的資料列群組包含 1,048,576 個資料列時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將資料列群組標示為已關閉。 稱為 *tuple-mover* 的背景處理序，會找到每個已關閉的資料列群組，並將其壓縮到資料行存放區中。  
  
 每一個叢集資料行存放區索引可以有多個差異存放區。  
  
-   如果差異存放區已鎖定， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將嘗試鎖定另一個差異存放區。 如果沒有可用的差異存放區， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將建立新的差異存放區。  
  
-   若是資料分割資料表，每個分割區可能會有多個差異存放區。  
  
 下列案例說明載入的資料列何時會直接進入資料行存放區，或何時會進入差異存放區。  
  
 在範例中，每個資料列群組可以有 102,400-1,048,576 個資料列。 實際上，在記憶體不足的情況下，資料列群組的大小上限可能會小於 1,048,576 個資料列。  
  
|大量載入的資料列|已加入壓縮資料列群組的資料列數|已加入差異資料列群組的資料列數|  
|-----------------------|-------------------------------------------|--------------------------------------|  
|102,000|0|102,000|  
|145,000|145,000<br /><br /> 資料列群組大小：145,000|0|  
|1,048,577|1,048,576<br /><br /> 資料列群組大小：1,048,576。|1|  
|2,252,152|2,252,152<br /><br /> 資料列群組大小：1,048,576、1,048,576、155,000|0|  
  
 下列範例顯示將 1,048,577 個資料列載入資料表的結果。 結果顯示，資料行存放區中有一個 COMPRESSED 資料列群組 (壓縮的資料行區段)，而差異存放區中有 1 個資料列。  
  
```  
SELECT object_id, index_id, partition_number, row_group_id, delta_store_hobt_id, state state_desc, total_rows, deleted_rows, size_in_bytes   
FROM sys.dm_db_column_store_row_group_physical_stats  
```  
  
 ![Rowgroup and deltastore for a batch load](../../relational-databases/indexes/media/sql-server-pdw-columnstore-batchload.gif "Rowgroup and deltastore for a batch load")  
  
## 從暫存表格載入  
 資料載入的一個常見模式，是將資料先載入暫存表格再進行一些轉換後，使用下列命令將其載入目標資料表  
  
```  
INSERT INTO <columnstore index>  SELECT <list of columns> FROM <Staging Table>  
  
```  
  
 此命令會以 BCP 或大量插入等類似方式，將資料載入資料行存放區索引，但是為單一批次。 如果在暫存表格中的資料列數目 < 102400，資料列會載入差異資料列群組，否則資料列會直接載入壓縮的資料列群組中。  有一項很重要的限制是，這項 INSERT 作業為單一執行緒。 若要平行載入資料，可以建立多個暫存表格，或發出 INSERT/SELECT 同時設定暫存表格不重疊的資料列範圍。  SQL Server 2016 時已無這項限制。 下列命令會從暫存表格以平行方式載入資料，但您必須指定 TABLOCK  
  
```  
INSERT INTO <columnstore index>  WITH (TABLOCK)  SELECT <list of columns> FROM <Staging Table>  
```  
  
 從暫存表格載入叢集資料行存放區索引時，提供下列最佳化方式  
  
-   記錄最佳化︰將資料載入壓縮的資料列群組時，會記錄最少的內容。 當資料載入差異資料列群組時，沒有記錄的最低限制。  
  
-   鎖定最佳化︰載入壓縮資料列群組時，會取資料列群組的 X 鎖定。 然而，有了差異資料列群組時，會取得資料列群組的 X 鎖定，但 SQL Server 仍會鎖定 PAGE/EXTENT 的鎖定，這是因為 X 資料列群組鎖定不是鎖定階層的一部分。  
  
 如果您有一或多個非叢集索引，對於索引本身而言，沒有任何鎖定或記錄最佳化，但仍然會有如上所述的叢集資料行存放區索引最佳化。  
  
## 具有緩慢插入的載入  
 *緩慢插入* 是指使用 INSERT INTO 將資料列載入資料行存放區的方式。 每個資料列都會加入差異資料列群組。 緩慢進入的資料列會直接進入差異存放區資料列群組，並於該處累積到接近 1,048,576 個資料列時關閉該資料列群組為止，或是累積到資料行存放區索引重建為止。  
  
```  
INSERT INTO <table-name> VALUES (<set of values>)  
```  
  
 請注意，使用 INSERT INTO 將值插入叢集資料行存放區索引的並行執行緒，可以將資料列插入相同的差異存放區資料列群組。  
  
 資料列群組包含 1,048,576 個資料列之後，差異資料列群組會標示為已關閉，但仍可供查詢、更新/刪除作業之用，但新插入的資料列會進入現有或新建立的差異存放區資料列群組。 有一個背景執行緒 *Tuple Mover (TM)* 會每隔 5 分鐘左右定期壓縮已關閉的差異資料列群組。 您可以明確叫用下列命令來壓縮已關閉的差異資料列群組  
  
```  
ALTER INDEX <index-name> on <table-name> REORGANIZE  
```  
  
 如果想要強制關閉差異資料列群組並進行壓縮，可以執行下列命令。 如果已完成載入資料列，而且預期不會再有任何新的資料列，可以執行此命令。 明確地關閉並壓縮差異資料列群組，可以進一步保留儲存體，並改善分析查詢效能。 不想要插入新資料列的最佳做法是叫用此命令。  
  
```  
ALTER INDEX <index-name> on <table-name> REORGANIZE with (COMPRESS_ALL_ROW_GROUPS = ON)  
```  
  
## 載入資料分割資料表  
 對於分割資料， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會先將每個資料列指派至一個分割區，然後在分割區內對資料執行資料行存放區作業。 每個分割區都有自己的資料列群組以及至少一個差異存放區。  
  
## 載入非叢集資料行存放區索引  
 在具有非叢集資料行存放區索引資料的資料列存放區資料表上， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會一律將資料插入基底資料表。 資料絶對不會直接插入資料行存放區索引。  
  
## 另請參閱  
 [資料行存放區索引指南](../Topic/Columnstore%20Indexes%20Guide.md)   
 [資料行存放區索引建立版本功能摘要](../Topic/Columnstore%20Indexes%20Versioned%20Feature%20Summary.md)   
 [資料行存放區索引效能](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [開始使用資料行存放區進行即時作業分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [資料倉儲的資料行存放區索引](../Topic/Columnstore%20Indexes%20for%20Data%20Warehousing.md)   
 [資料行存放區索引重組](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  