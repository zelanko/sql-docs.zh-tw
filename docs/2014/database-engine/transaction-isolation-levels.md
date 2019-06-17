---
title: 交易隔離等級 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 8a6a82bf-273c-40ab-a101-46bd3615db8a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eaac46d0fd741e53493903d6fe0bb4656e9499a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774117"
---
# <a name="transaction-isolation-levels"></a>交易隔離等級
  存取記憶體最佳化的資料表的交易，可支援下列隔離等級。  
  
-   SNAPSHOT  
  
-   REPEATABLE READ  
  
-   SERIALIZABLE  
  
-   READ COMMITTED  
  
 交易隔離等級可以指定為原生編譯預存程序之不可部分完成的區塊的一部分。 如需詳細資訊，請參閱 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)。 從解譯的 [!INCLUDE[tsql](../includes/tsql-md.md)] 存取記憶體最佳化的資料表時，可以使用資料表層級的提示指定隔離等級。  
  
 當您定義原生編譯的預存程序時，必須指定交易隔離等級。 從解譯之 [!INCLUDE[tsql](../includes/tsql-md.md)] 中的使用者交易存取記憶體最佳化的資料表時，您必須在資料表提示中指定隔離等級。 如需詳細資訊，請參閱 <<c0> [ 指導方針與記憶體最佳化資料表的交易隔離等級](../relational-databases/in-memory-oltp/memory-optimized-tables.md)。  
  
 包含自動認可交易之記憶體最佳化的資料表支援 READ COMMITTED 隔離等級。 READ COMMITTED 在使用者交易或不可部分完成的區塊中無效。 明確或隱含使用者交易則不支援 READ COMMITTED。 包含自動認可交易的記憶體最佳化資料表可支援 READ_COMMITTED_SNAPSHOT 隔離等級，前提是查詢未存取任何以磁碟為基礎的資料表。 此外，搭配 SNAPSHOT 隔離使用解譯的 [!INCLUDE[tsql](../includes/tsql-md.md)] 所啟動的交易，無法存取記憶體最佳化的資料表。 搭配 REPEATABLE READ 或 SERIALIZABLE 隔離使用解譯的 [!INCLUDE[tsql](../includes/tsql-md.md)] 啟動的交易，必須使用 SNAPSHOT 隔離來存取記憶體最佳化的資料表。 如需有關此案例的詳細資訊，請參閱 <<c0> [ 跨容器交易](cross-container-transactions.md)。  
  
 READ COMMITTED 是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的預設隔離等級。 當工作階段的隔離等級為 READ COMMITED (或更低) 時，您可以執行下列其中一個動作：  
  
-   明確使用存取記憶體最佳化資料表的較高的隔離等級提示 (例如，WITH (SNAPSHOT) )。  
  
-   指定 `MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT` 設定選項，可以將記憶體最佳化之資料表的隔離等級，設定為 SNAPSHOT (等同於在每個記憶體最佳化之資料表中加入 WITH(SNAPSHOT) 提示)。 如需詳細資訊`MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT`，請參閱 < [ALTER DATABASE SET 選項&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
 或者，如果工作階段的隔離等級為 READ COMMITTED，您可以使用自動認可交易。  
  
 在解譯的 [!INCLUDE[tsql](../includes/tsql-md.md)] 中啟動的 SNAPSHOT 交易無法存取記憶體最佳化資料表。  
  
 記憶體最佳化的資料表所支援的交易隔離等級，會提供與以磁碟為基礎之資料表相同的邏輯保證。 用於提供隔離等級保證的機制則不同。  
  
 如果是以磁碟為基礎的資料表，大部分的隔離等級保證都會使用鎖定來實作，透過封鎖來避免衝突。 如果是記憶體最佳化的資料表，則會使用衝突偵測機制來施行保證，以免需要進行鎖定。 例外狀況是磁碟資料表上的 SNAPSHOT 隔離。 這個實作方式類似於在記憶體最佳化的資料表上使用衝突偵測機制的 SNAPSHOT 隔離。  
  
 SNAPSHOT  
 這個隔離等級會指定交易中任何陳述式所讀取的資料，都是交易開始時就存在之資料的交易一致性版本。 交易只能辨識交易開始之前所認可的資料修改。 在目前交易中執行的陳述式，看不到其他交易在目前交易開始之後所進行的資料修改。 交易中的陳述式會取得已認可之資料的快照集，如同資料在交易開始時的狀態。  
  
 寫入作業 (更新、插入和刪除) 永遠都會與其他交易完全隔離。 因此，SNAPSHOT 交易中的寫入作業可能會與其他交易的寫入作業發生衝突。 當目前交易嘗試更新或刪除目前交易開始之後由另一筆已認可的交易所更新或刪除的資料列時，此交易將會終止，並產生以下錯誤訊息。  
  
 錯誤 41302。 目前交易嘗試更新自此交易啟動以來已經更新的資料表 X 記錄。 交易已中止。  
  
 當目前交易嘗試插入之資料列的主索引鍵值與目前交易之前另一筆已認可的交易所插入的資料列相同時，將會認可失敗並產生下列錯誤訊息。  
  
 錯誤 41325。 目前的交易無法認可，因為可序列化驗證失敗。  
  
 如果交易寫入的資料表在交易認可之前卸除，交易將會終止並產生下列錯誤訊息：  
  
 錯誤 41305。 目前的交易無法認可，因為可重複的讀取驗證失敗。  
  
 REPEATABLE READ  
 此隔離等級包括 SNAPSHOT 隔離等級所提供的保證。 此外，REPEATABLE READ 保證，對於交易讀取的任何資料列而言，當認可交易時，另一筆交易尚未變更此資料列。 交易中的每個讀取作業都可重複，直到交易結束為止。  
  
 如果目前交易已讀取在目前交易之前的另一筆已認可的交易所更新的任何資料列，則認可會失敗並出現下列錯誤訊息。  
  
 錯誤 41305。 目前的交易無法認可，因為可重複的讀取驗證失敗。  
  
 SERIALIZABLE  
 此隔離等級包括 REPEATABLE READ 所提供的保證。 快照集和交易結束之間未出現任何虛設項目列。 虛設項目列符合選取、更新或刪除的篩選條件。  
  
 執行此交易時，就像是沒有並行交易一樣。 所有動作幾乎都發生在單一序列化時間點 (認可時間)。  
  
 如果違反任何保證，便無法認可交易，而且會出現下列錯誤訊息：  
  
 錯誤 41325。 目前的交易無法認可，因為可序列化驗證失敗。  
  
## <a name="see-also"></a>另請參閱  
 [了解記憶體最佳化資料表上的交易](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [具有記憶體最佳化資料表的交易隔離等級的指導方針](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [經記憶體最佳化的資料表上交易的重試邏輯方針](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
  
