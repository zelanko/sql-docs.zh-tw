---
title: 跨容器交易 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5d84b51a-ec17-4c5c-b80e-9e994fc8ae80
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 290aff0bfcb01e098ae87b48cf582cdf999314c4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62807422"
---
# <a name="cross-container-transactions"></a>跨容器交易
  跨容器交易是隱含或明確的使用者交易，其包含對原生編譯的預存程序或記憶體最佳化的資料表作業的呼叫。  
  
 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，預存程序的呼叫不會起始交易。 在自動認可模式中執行原生編譯的程序時 (不在使用者交易的內容中)，將不會視為跨容器交易。  
  
 參考記憶體最佳化的資料表的任何解譯的查詢都視為跨容器交易的一部分，不論是從明確或隱含交易執行還是在自動認可模式中執行。  
  
##  <a name="isolation-of-individual-operations"></a><a name="isolation"></a>隔離個別作業  
 每一筆 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 交易都有隔離等級。 預設隔離等級為 Read Committed。 若要使用不同的隔離等級，您可以使用[SET TRANSACTION 隔離等級 &#40;transact-sql&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)設定隔離等級。  
  
 相較於以磁碟為基礎的資料表作業，在記憶體最佳化的資料表上執行作業通常更需要在不同的隔離等級。 在交易中，為陳述式集合或個別讀取作業設定不同隔離等級是可行的。  
  
### <a name="specifying-the-isolation-level-of-individual-operations"></a>指定個別作業的隔離等級  
 若要為交易中的一組陳述式設定不同的隔離等級，您可以使用 `SET TRANSACTION ISOLATION LEVEL`。 以下的交易範例會使用 serializable 的隔離等級當做預設值。 位於 t3、t2 和 t1 的插入和選取作業會在 repeatable read 的隔離之下執行。  
  
```sql  
set transaction isolation level serializable  
go  
  
begin transaction  
 ......  
  set transaction isolation level repeatable read  
  
  insert t3 select * from t1 join t2 on t1.id=t2.id  
  
  set transaction isolation level serializable  
 ......  
commit  
```  
  
 若要為個別讀取作業設定不同於交易預設值的隔離等級，您可以使用資料表提示 (例如，可序列化)。 每個選取都會對應到讀取作業，而每個更新和每個刪除都會對應到讀取，因為在可以更新和刪除資料列之前永遠都必須先讀取它。 插入作業沒有隔離等級，因為寫入在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中永遠都是隔離的。 在下列範例中，交易的預設隔離等級為 read committed，不過，資料表 t1 會在 serializable 隔離之下存取，而 t2 會在 snapshot 隔離之下存取。  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
 ......  
  
  insert t3 select * from t1 (serializable) join t2 (snapshot) on t1.id=t2.id  
  
  ......  
commit  
```  
  
### <a name="isolation-semantics-for-individual-operations"></a>個別作業的隔離語意  
 可序列化交易 T 會在完全隔離的情況下執行。 就像是其他每一筆交易在 T 開始之前已經認可，或者在 T 認可之後開始一樣。 當交易中有不同的作業具有不同隔離等級時，它會變得更複雜。  
  
 中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的交易隔離等級的一般語義以及對鎖定的影響，會在[&#40;Transact-sql&#41;的設定交易隔離等級](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)中說明。  
  
 如果是不同作業可能會有不同隔離等級的跨容器交易，您必須了解個別讀取作業的隔離語意。 寫入作業永遠都會隔離。 不同交易中的寫入無法影響彼此。  
  
 資料讀取作業會傳回滿足篩選條件的許多資料列。  
  
 讀取會做為交易 T 的一部分來執行。讀取作業的隔離等級可以根據來理解，  
  
 認可狀態  
 認可狀態指的是，是否可以保證資料讀取為已認可狀態。  
  
 (交易) 一致性  
 一組讀取的交易一致性指的是，是否保證所有資料列版本讀取都精確包含來自相同一組交易的更新。  
  
 穩定性會保證系統給出有關資料讀取的資訊給交易 T。  
 穩定性指的是交易的讀取是否可重複。 也就是說，如果讀取已重複，它們是否會傳回相同的資料列和資料列版本？  
  
 特定保證指的是交易的邏輯結束時間。 一般而言，邏輯結束時間是資料庫認可交易的時間。 如果記憶體最佳化的資料表是由交易所存取，則邏輯結束時間在技術上為驗證階段的開始  （如需詳細資訊，請參閱[記憶體優化資料表中交易](../relational-databases/in-memory-oltp/memory-optimized-tables.md)的交易存留期討論。  
  
 不論隔離等級為何，交易 (T) 永遠都會看到自己的更新：  
  
 READ UNCOMMITTED  
 資料讀取可能不會處於已認可、一致或穩定狀態。 不過，它將會包含 T 稍早完成的寫入作業。  
  
 READ COMMITTED  
 將會認可資料讀取。  
  
 SNAPSHOT  
 snapshot 隔離之下由 T 執行的所有讀取作業都有相同的邏輯讀取時間，也就是交易的開始時間。 將會保證資料讀取為已認可狀態，而且在邏輯讀取時間維持一致性。 也會保證重複原始讀取時間的讀取會傳回相同的結果。  
  
 REPEATABLE READ  
 保證資料讀取為已認可狀態，而且一直到交易的邏輯結束時間為止都很穩定。  
  
 SERIALIZABLE  
 可重複讀取的所有保證，以及與 T 所執行之所有可序列化讀取作業相關的交易一致性。虛設避免表示掃描工作只能傳回 T 所寫入的其他資料列，但沒有其他交易寫入的資料列。  
  
 以下列交易為例：  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
  -- remove all rows from t3; the related read operation is performed under read committed   
  -- isolation, as this is the default for the transaction  
  delete from t3  
  
  -- copy the contents from t1 to t3; the read on t1 is performed under the serializable   
  -- isolation level  
  insert t3 select * from t1 (serializable)  
  
  -- compare t3 and t1; note: the result set may not be empty, as rows may have been added   
  -- by other transaction before this select, due to the read committed isolation level  
  select * from t3 except t1  
  
  -- compare t1 and t3; note: the result set is empty, as no rows have been added to t1   
  -- since its contents were copied to t1, due to the serializable isolation level  
  select * from t1 except t3  
commit  
```  
  
 此交易會從 t3 刪除 read committed 隔離之下的所有資料列、複製 t1 到 t3 中在 serializable 隔離之下的所有資料列，然後比較 t1 和 t3。 部分資料列 [不在 t1 中] 可能已加入到 t3，因為此資料表已清空。 沒有任何資料列已加入至 t1，因為複製為 serializable。  
  
 雖然在交易結束時從 t1 讀取的語意為 read committed，但是它實際上為 serializable，因為之前在交易中的 serializable 隔離之下已執行相同的讀取：可序列化保證如果在之後的任何交易時間點執行讀取，將會傳回相同的資料列。  
  
## <a name="cross-container-transactions-and-isolation-levels"></a>跨容器交易和隔離等級  
 跨容器交易可視為具有兩端：以磁碟為基礎的那一端 (適用於以磁碟為基礎資料表的作業) 和記憶體最佳化的那一端 (適用於記憶體最佳化資料表的作業)。 這兩端可能會有不同的隔離等級。 事實上，每一端的個別讀取作業可能會有不同的隔離等級。  
  
 如果符合下列其中一個條件，給定交易 T 的磁碟端會到達某個隔離等級 X：  
  
-   它會從 X 開始。也就是說，會話預設值是 X，因為您執行`SET TRANSACTION ISOLATION LEVEL`了，或者它是[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]預設值。  
  
-   在交易期間，使用 `SET TRANSACTION ISOLATION LEVEL` 將預設隔離等級變更為 X。  
  
-   以磁碟為基礎的資料表讀取作業會使用 `WITH (X)` 語法在隔離等級 X 之下執行。  
  
 如果在 T 的執行期間，記憶體最佳化資料表的任何讀取作業或是任何原生方式編譯的預存程序在隔離等級 Y 之下執行，T 的記憶體最佳化那一端會到達隔離等級 Y。  
  
 以下列交易為例。 此處，t1 和 t2 是以磁碟為基礎的資料表，而 t3 和 t4 是記憶體最佳化的資料表。  
  
 交易的磁碟端會到達 read committed 隔離等級，因為它是從這個等級開始。 磁碟端也會到達 repeatable read 隔離等級，因為第一個讀取作業是在這個隔離等級之下執行。 交易結束時的刪除作業會在 read committed 隔離等級之下執行，因此不會引進新的隔離等級。  
  
 交易的記憶體最佳化那一端可以到達兩個等級的其中一個：如果 condition1 為 true，它會到達可序列化隔離，而如果為 false，則記憶體最佳化那一端只會到達快照集隔離。  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
  select * from t1 (repeatableread)  
  
  if condition1 begin  
    insert t3 select * from t4 (serializable)  
  end  
  else begin  
    insert t3 select * from t4 (snapshot)  
  end  
  
  delete from t1  
commit  
```  
  
### <a name="supported-isolation-levels-for-cross-container-transactions"></a>跨容器交易支援的隔離等級  
 在跨容器交易中，搭配記憶體最佳化的資料表作業使用的隔離等級有一些限制。  
  
 記憶體最佳化的資料表可支援 SNAPSHOT、REPEATABLE READ 和 SERIALIZABLE 隔離等級。 如果是自動認可交易，記憶體最佳化的資料表可支援 READ COMMITTED 隔離等級。  
  
 以下是支援的案例：  
  
-   READ UNCOMMITTED、READ COMMITTED 和 READ_COMMITTED_SNAPSHOT 跨容器交易可以在 SNAPSHOT、REPEATABLE READ 和 SERIALIZABLE 隔離之下存取記憶體最佳化的資料表。 交易的 READ COMMITTED 保證依然存在；資料庫已認可此交易讀取的所有資料列。  
  
-   REPEATABLE READ 和 SERIALIZABLE 交易可以在 SNAPSHOT 隔離之下存取記憶體最佳化的資料表。  
  
## <a name="read-only-cross-container-transactions"></a>唯讀的跨容器交易  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的大部分唯讀交易都會在認可時間回復。 因為資料庫不需認可任何變更，所以系統會釋出交易所使用的資源。 如果是唯讀的磁碟交易，交易所做的所有鎖定都會在此時釋放。 如果是跨越單一原生編譯程序執行的唯讀記憶體最佳化交易，則不會執行驗證。  
  
 自動認可模式中的跨容器唯讀交易會在交易結束時回復。 未執行任何驗證。  
  
 如果交易在 REPEATABLE READ 或 SERIALIZABLE 隔離之下存取記憶體最佳化資料表，則明確或隱含的跨容器唯讀交易會在認可時間執行驗證。 如需驗證的詳細資訊，請參閱[記憶體優化資料表中交易](../relational-databases/in-memory-oltp/memory-optimized-tables.md)的衝突偵測、驗證和認可相依性檢查一節。  
  
## <a name="see-also"></a>另請參閱  
 [瞭解記憶體優化資料表上的交易](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [具有記憶體優化資料表的交易隔離等級方針](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)   
 [記憶體最佳化資料表交易的重試邏輯方針](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
  
