---
title: "資料行存放區索引 - 資料倉儲 | Microsoft 文件"
ms.custom: 
ms.date: 01/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21fd153b-116d-47fc-a926-f1528299a391
caps.latest.revision: 15
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ba866cdea9d6158affc31e74572bb9610ab94489
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="columnstore-indexes---data-warehouse"></a>資料行存放區索引 - 資料倉儲
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  結合資料分割的資料行存放區索引對於建置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料倉儲非常重要。  
  
## <a name="whats-new"></a>新功能  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 導入了這些增強資料行存放區效能的功能：  
  
-   AlwaysOn 支援在可讀取之次要複本上的資料行存放區索引進行查詢。  
  
-   Multiple Active Result Sets (MARS) 支援資料行存放區索引。  
  
-   全新的 [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md) 動態管理檢視，可提供資料列群組層級的效能疑難排解資訊。  
  
-   資料行存放區索引上的單一執行緒查詢可以批次模式執行。 以前只有多執行緒查詢可以批次模式執行。  
  
-   SORT 運算子可在批次模式中執行。  
  
-   多個 DISTINCT 作業可在批次模式中執行。  
  
-   視窗彙總現可在資料庫相容性層級 130 的批次模式下執行  
  
-   彙總下推可有效處理彙總。 支援所有資料庫相容性層級。  
  
-   字串述詞下推可有效處理字串述詞。 支援所有資料庫相容性層級。  
  
-   資料庫相容性等級 130 的快照集隔離  
  
## <a name="improve-performance-by-combining-nonclustered-and-columnstore-indexes"></a>透過結合非叢集和資料行存放區索引來改善效能  
 自 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]起，您可以在叢集資料行存放區索引上定義非叢集索引。  
  
### <a name="example-improve-efficiency-of-table-seeks-with-a-nonclustered-index"></a>例如：以非叢集索引改善資料表搜尋的效率  
 若要改善在資料倉儲中搜尋資料表的效率，您可以建立專用的非叢集索引來執行對資料表搜尋有最佳效能的查詢。 例如，針對 btree 索引執行比對值或傳回小範圍值的查詢，其效能會比針對資料行存放區索引執行的好。 它們不需要透過資料行存放區索引的完整資料表掃描，且透過 btree 索引執行二進位搜尋，會較快傳回正確的結果。  
  
```  
--BASIC EXAMPLE: Create a nonclustered index on a columnstore table.  
  
--Create the table  
CREATE TABLE t_account (  
    AccountKey int NOT NULL,  
    AccountDescription nvarchar (50),  
    AccountType nvarchar(50),  
    UnitSold int  
);  
GO  
  
--Store the table as a columnstore.  
CREATE CLUSTERED COLUMNSTORE INDEX taccount_cci ON t_account;  
GO  
  
--Add a nonclustered index.  
CREATE UNIQUE INDEX taccount_nc1 ON t_account (AccountKey);  
```  
  
### <a name="example-use-a-nonclustered-index-to-enforce-a-primary-key-constraint-on-a-columnstore-table"></a>範例：使用非叢集索引在資料行存放區資料表上強制執行主索引鍵條件約束。  
 根據設計，資料行存放區資料表不允許主索引鍵條件約束。 現在您可以在資料行存放區資料表上使用非叢集索引強制執行主索引鍵條件約束。 在非 NULL 的資料行上主索引鍵等同 UNIQUE 條件約束，而且 SQL Server 會實作 UNIQUE 條件約束來當作非叢集索引。 結合這些事實，以下範例在非 NULL 資料行 accountkey 上定義 UNIQUE 條件約束。 結果是一個將主索引鍵條件約束強制做為非 NULL 資料行上之 UNIQUE 條件約束的非叢集索引。  
  
 接下來，該資料表會轉換為叢集資料行存放區索引。 轉換期間會保留非叢集索引。 結果是一個包含強制執行主索引鍵條件約束之非叢集索引的叢集資料行存放區索引。 因為資料行存放區資料表上的任何更新或插入都會影響非叢集索引，所以任何違反唯一條件約束和非 NULL 的作業都會造成整個作業失敗。  
  
 結果是一個包含強制在兩個索引上執行主索引鍵條件約束之非叢集索引的資料行存放區索引。  
  
```  
--EXAMPLE: Enforce a primary key constraint on a columnstore table.   
  
--Create a rowstore table with a unique constraint.  
--The unique constraint is implemented as a nonclustered index.  
CREATE TABLE t_account (  
    AccountKey int NOT NULL,  
    AccountDescription nvarchar (50),  
    AccountType nvarchar(50),  
    UnitSold int,  
  
    CONSTRAINT uniq_account UNIQUE (AccountKey)  
);  
  
--Store the table as a columnstore.   
--The unique constraint is preserved as a nonclustered index on the columnstore table.  
CREATE CLUSTERED COLUMNSTORE INDEX t_account_cci ON t_account  
  
--By using the previous two steps, every row in the table meets the UNIQUE constraint  
--on a non-NULL column.  
--This has the same end-result as having a primary key constraint  
--All updates and inserts must meet the unique constraint on the nonclustered index or they will fail.  
  
--If desired, add a foreign key constraint on AccountKey.  
  
ALTER TABLE [dbo].[t_account]  
WITH CHECK ADD FOREIGN KEY([AccountKey]) REFERENCES my_dimension(Accountkey)  
;  
  
```  
  
### <a name="improve-performance-by-enabling-row-level-and-row-group-level-locking"></a>藉由啟用資料列層級和資料列群組層級鎖定來改善效能  
 為了補充資料行存放區索引功能上的非叢集索引， [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 提供選取、更新和刪除作業的詳細鎖定功能。 查詢能夠針對非叢集索引在索引搜尋上以資料列層級鎖定執行，或針對資料行存放區索引在完整資料表掃描上以資料行群組層級鎖定執行。 藉由適當地使用資料列層級和資料列群組層級鎖定，來以此方法達到更高的獨取/寫入並行。  
  
```  
--Granular locking example  
--Store table t_account as a columnstore table.  
CREATE CLUSTERED COLUMNSTORE INDEX taccount_cci ON t_account  
GO  
  
--Add a nonclustered index for use with this example  
CREATE UNIQUE INDEX taccount_nc1 ON t_account (AccountKey);  
GO  
  
--Look at locking with access through the nonclustered index  
SET TRANSACTION ISOLATION LEVEL repeatable read;  
GO  
  
BEGIN TRAN  
    -- The query plan chooses a seek operation on the nonclustered index  
    -- and takes the row lock  
    SELECT * FROM t_account WHERE AccountKey = 100;  
END TRAN  
  
```  
  
### <a name="snapshot-isolation-and-read-committed-snapshot-isolations"></a>快照集隔離和讀取認可快照集隔離  
 使用「快照集隔離」(SI) 來保證交易的一致性，以及「讀取認可快照集隔離」(RCSI) 來確保資料行存放區索引上查詢陳述式層級的一致性。 這可讓查詢執行而不會封鎖資料寫入器。 此非封鎖性的行為也會大幅降低複雜交易發生死結的可能性。 如需詳細資訊，請參閱 MSDN 上的 [SQL Server 中的快照集隔離](http://msdn.microsoft.com/library/tcbchxcb\(v=vs.110\).aspx) 。  
  
## <a name="see-also"></a>另請參閱  
 資料行存放區索引指南   
 資料行存放區索引資料載入   
 資料行存放區索引建立版本功能摘要   
 [資料行存放區索引效能](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [開始使用資料行存放區進行即時作業分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [資料行存放區索引重組](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  

