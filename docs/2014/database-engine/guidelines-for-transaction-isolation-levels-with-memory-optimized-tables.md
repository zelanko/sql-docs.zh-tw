---
title: 具有記憶體最佳化資料表的交易隔離等級的指導方針 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e365e9ca-c34b-44ae-840c-10e599fa614f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26f0193d40a01858bc3fe651a23b389a4ffcb6ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779153"
---
# <a name="guidelines-for-transaction-isolation-levels-with-memory-optimized-tables"></a>搭配記憶體最佳化的資料表使用交易隔離等級的方針
  在許多情況下，您必須指定交易隔離等級。 記憶體最佳化資料表的交易隔離不同於磁碟基礎的資料表。  
  
 指定交易隔離等級的需求：  
  
-   TRANSACTION ISOLATION LEVEL 是包含原生編譯預存程序內容之 ATOMIC 區塊的必要選項。  
  
-   由於隔離等級在跨容器交易的使用限制，解譯的 [!INCLUDE[tsql](../includes/tsql-md.md)] 中記憶體最佳化資料表的使用，通常必須伴隨著資料表提示，指定用來存取資料表之隔離等級。 如需有關隔離等級提示和跨容器交易的詳細資訊，請參閱 <<c0> [ 交易隔離等級](../../2014/database-engine/transaction-isolation-levels.md)。  
  
-   所需的交易隔離等級必須明確宣告。 無法使用鎖定提示 (例如 XLOCK) 來保證交易中某些資料列或資料表的隔離。  
  
-   存取資料庫的應用程式應該實作重試邏輯，以處理毀滅交易之衝突、驗證失敗和認可相依性失敗所產生的錯誤。 請注意，即使是唯讀交易也會發生認可相依性失敗。  
  
-   記憶體最佳化的資料表應該避免長時間執行的交易。 這類交易會增加衝突及後續交易終止的可能性。 長時間執行的交易也可能會延緩記憶體回收。 交易執行的時間愈久，記憶體中 OLTP 就會將最近刪除的資料列版本保留得愈久，這會減少新交易的查閱效能。  
  
 磁碟基礎的資料表通常依賴鎖定及封鎖進行交易隔離。 記憶體最佳化的資料表依賴多重版本設定和衝突偵測以保證隔離。 如需詳細資訊，請參閱 < 衝突偵測、 驗證和認可相依性檢查在[Transactions in Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md)。  
  
 磁碟基礎的資料表允許多重版本設定與隔離等級 SNAPSHOT 和 READ_COMMITTED_SNAPSHOT。 對於記憶體最佳化的資料表，所有隔離等級都是根據多個版本，包括 REPEATABLE READ 和 SERIALIZABLE。  
  
## <a name="types-of-transactions"></a>交易的類型  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的每一個查詢都是在交易的內容中執行。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的交易有三種類型：  
  
-   自動認可交易： 如果沒有使用中交易內容，而且在工作階段中隱含交易未設為 ON，每個查詢都有自己的交易內容。 交易在陳述式開始執行時開始，在陳述式完成時完成。  
  
-   明確交易： 使用者透過明確 BEGIN TRAN 或 BEGIN ATOMIC 啟動交易。 交易在對應 COMMIT 和 ROLLBACK 或 END 之後完成 (在 ATOMIC 區塊的情況下)。  
  
-   隱含交易： 當 IMPLICIT_TRANSACTIONS 選項設為 ON 時，只要使用者執行陳述式，而且沒有使用中交易內容時，交易就會隱含啟動。 交易是透過明確 COMMIT 和 ROLLBACK 完成的。  
  
## <a name="baseline-read-committed-isolation"></a>基準 READ COMMITTED 隔離  
 READ COMMITTED 是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的預設隔離等級。  
  
 READ COMMITTED 隔離等級可確保交易無視於在目前交易之外變更的任何未認可的資料。 換句話說，交易只會讀取資料庫已經認可的資料，或是由目前交易所變更的資料。  
  
 記憶體最佳化的資料表支援的所有隔離等級都提供讀取認可保證。 因此，如果交易不需要更強大的保證，您可以使用記憶體最佳化資料表支援的任何隔離等級。 相較於其他隔離等級，SNAPSHOT 使用最少的系統資源。  
  
 SNAPSHOT 隔離等級提供的保證 (記憶體最佳化資料表支援的最低隔離等級) 包含 READ COMMITTED 保證。 交易中的每個陳述式都會讀取資料庫的相同一致版本。 不只是交易所讀取的所有資料列都會認可至資料庫，所有讀取作業也會看到同一組交易所做的同一組變更。  
  
 **指導方針**:如果只需要 READ COMMITTED 隔離保證，使用快照集隔離來存取記憶體最佳化的資料表，透過原生編譯的預存程序與解譯[!INCLUDE[tsql](../includes/tsql-md.md)]。  
  
 對於自動認可交易，READ COMMITTED 隔離等級隱含對應到記憶體最佳化資料表的 SNAPSHOT 隔離。 因此，如果 TRANSACTION ISOLATION LEVEL 工作階段設定為 READ COMMITTED，當存取記憶體最佳化的資料表時，不需要透過資料表提示指定隔離等級。  
  
 下列自動認可交易範例示範記憶體最佳化資料表 Customers 和正規資料表 [Order History] 之間的聯結，當做特定批次的一部分：  
  
```sql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
GO  
SELECT *   
FROM dbo.Customers AS c   
LEFT JOIN dbo.[Order History] AS oh   
    ON c.customer_id = oh.customer_id;  
```  
  
 下列明確或隱含交易範例示範相同聯結，但是這次是在明確的使用者交易中。 記憶體最佳化的資料表 Customers 是在快照隔離下存取，透過資料表提示 WITH (SNAPSHOT) 所指示，而正規資料表 [Order History] 則是在讀取認可隔離下存取：  
  
```sql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
GO  
BEGIN TRAN  
SELECT * FROM dbo.Customers c with (SNAPSHOT)   
LEFT JOIN dbo.[Order History] oh   
    ON c.customer_id=oh.customer_id  
...  
COMMIT  
```  
  
### <a name="operational-differences"></a>操作差異  
 除了讀取認可保證以外，使用磁碟基礎之資料表的應用程式可能還依賴兩個重要實作詳細資料。 將磁碟基礎的資料表 (使用 READ COMMITTED 隔離進行存取) 轉換為記憶體最佳化的資料表 (使用 SNAPSHOT 隔離進行存取) 時，請注意下列事項：  
  
-   磁碟基礎之資料表的 READ COMMITTED 隔離等級實作 (假設 READ_COMMITTED_SNAPSHOT 為 OFF) 使用鎖定來防止讀取器和寫入器之間的衝突。 當寫入器開始更新資料列時，它會取得鎖定，直到交易認可時才釋放鎖定。 任何讀取作業都會被封鎖，並等待寫入交易認可。  
  
     有些應用程式可能會假設讀取器一定會等候寫入器認可，特別是在應用程式層中兩筆交易之間有任何同步處理時。  
  
     **指導方針：** 應用程式不可依賴封鎖行為。 如果應用程式需要並行交易之間同步處理，這類邏輯可以實作在應用程式層，或在資料庫層中，透過[sp_getapplock &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-getapplock-transact-sql)。  
  
-   在使用 READ COMMITTED 隔離的交易，每個陳述式都會看到資料庫中最新版本的資料列。 因此，後續陳述式會看到資料庫狀態變更。  
  
     使用 WHILE 迴圈輪詢資料表，直到找到新資料列為止，就是使用這個假設的應用程式模式範例。 在迴圈的每個反覆運算，查詢會看到資料庫的最新更新。  
  
     **指導方針：** 如果應用程式需要輪詢記憶體最佳化的資料表，以取得最新的資料列寫入資料表，將輪詢迴圈移交易範圍之外。  
  
     下列是使用這個假設的範例應用程式模式。 使用 WHILE 迴圈輪詢資料表，直到找到新資料列為止。 在每個迴圈反覆運算，查詢會存取資料庫的最新更新。  
  
 下列範例指令碼會輪詢資料表 t1，直到它具有資料列。 接著從資料表移除單一資料列，進一步處理。  
  
 請注意，輪詢邏輯必須在交易範圍之外，因為它使用快照隔離來存取資料表 t1。 在交易範圍內使用輪詢邏輯，會建立長時間執行的交易，這是不良作法。  
  
```sql  
-- poll table  
WHILE NOT EXISTS (SELECT 1 FROM dbo.t1)  
BEGIN   
  -- if empty, wait and poll again  
  WAITFOR DELAY '00:00:01'  
END  
  
BEGIN TRANSACTION  
  DECLARE @id int  
  SELECT TOP 1 @id=id FROM dbo.t1 WITH (SNAPSHOT)  
  DELETE FROM dbo.t1 WITH (SNAPSHOT) WHERE id=@id  
  
  -- insert processing based on @id  
COMMIT  
```  
  
## <a name="locking-table-hints"></a>鎖定資料表提示  
 鎖定提示 ([資料表提示&#40;TRANSACT-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)) 例如 HOLDLOCK 和 XLOCK 可以搭配以磁碟為基礎的資料表有[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]採取更多的鎖定所需之指定的隔離等級。  
  
 記憶體最佳化的資料表不使用鎖定。 可使用較高的隔離等級，例如 REPEATABLE READ 和 SERIALIZABLE，來宣告所需的保證。  
  
 不支援鎖定提示。 請改為透過交易隔離等級宣告所需的保證。 (支援 NOLOCK，因為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 沒有在記憶體最佳化的資料表上鎖定。 請注意，與磁碟基礎的資料表相反，NOLOCK 不表示記憶體最佳化資料表的 READ UNCOMMITTED 行為)。  
  
## <a name="see-also"></a>另請參閱  
 [了解記憶體最佳化資料表上的交易](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [指導方針的記憶體最佳化資料表上的交易重試邏輯](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)   
 [交易隔離等級](../../2014/database-engine/transaction-isolation-levels.md)  
  
  
