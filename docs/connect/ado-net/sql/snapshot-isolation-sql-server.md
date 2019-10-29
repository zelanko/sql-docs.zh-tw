---
title: SQL Server 中的快照集隔離
description: 描述快照集隔離的支援，這是為了減少交易式應用程式中的封鎖而設計的資料列版本設定機制。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 43ae5dd3-50f5-43a8-8d01-e37a61664176
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 8ef462246d35694ba9bf38954ca8c58635e44e7f
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452086"
---
# <a name="snapshot-isolation-in-sql-server"></a>SQL Server 中的快照集隔離

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

快照集隔離可增強 OLTP 應用程式的平行存取。  
  
## <a name="understanding-snapshot-isolation-and-row-versioning"></a>瞭解快照集隔離和資料列版本設定  
一旦啟用快照集隔離，即會在 **tempdb** 中維護每筆交易所更新的資料列版本。 唯一的交易序號會識別每個交易，而且會針對每個資料列版本記錄這些唯一的數位。 交易適用于在交易序號之前具有序號的最新資料列版本。 交易會忽略在交易開始之後所建立的較新資料列版本。  
  
「快照集」一詞反映了交易中的所有查詢，會根據交易開始時資料庫的狀態，查看資料庫的相同版本或快照集。 在快照集交易中的基礎資料列或資料頁上不會取得鎖定，這允許其他交易執行，而不會被先前的 incompleted 交易封鎖。 修改資料的交易不會封鎖讀取資料的交易，而讀取資料的交易不會封鎖寫入資料的交易，因為它們通常會在 SQL Server 中預設的讀取認可隔離等級之下。 此非封鎖性的行為也會大幅降低複雜交易發生死結的可能性。  
  
快照集隔離會使用開放式平行存取模型。 如果快照集交易嘗試認可自交易開始後已變更之資料的修改，交易將會回復，並會引發錯誤。 您可以針對存取要修改之資料的 SELECT 語句使用 UPDLOCK 提示，以避免發生這種情況。 如需詳細資訊，請參閱 SQL Server 線上叢書中的「鎖定提示」。  
  
您必須先設定 ALLOW_SNAPSHOT_ISOLATION ON 資料庫選項來啟用快照集隔離，才能在交易中使用它。 如此會啟動在暫存資料庫 (**tempdb**) 中儲存資料列版本的機制。 您必須在使用 Transact-sql ALTER DATABASE 語句的每個資料庫中啟用快照集隔離。 在這方面，快照集隔離與讀取認可、可重複讀取、SERIALIZABLE 和讀取未認可的傳統隔離等級不同，這不需要任何設定。 下列語句會啟用快照集隔離，並以快照集取代預設的讀取認可行為：  
  
```sql  
ALTER DATABASE MyDatabase  
SET ALLOW_SNAPSHOT_ISOLATION ON  
  
ALTER DATABASE MyDatabase  
SET READ_COMMITTED_SNAPSHOT ON  
```  
  
設定 READ_COMMITTED_SNAPSHOT ON 選項，可讓您存取預設讀取認可隔離等級下的已建立版本資料列。 如果 READ_COMMITTED_SNAPSHOT 選項設定為 OFF，您就必須明確設定每個會話的快照隔離等級，才能存取已建立版本的資料列。  
  
## <a name="managing-concurrency-with-isolation-levels"></a>管理具有隔離等級的平行存取  
Transact-sql 語句執行時所用的隔離等級會決定其鎖定和資料列版本設定行為。 隔離等級具有全連線的範圍，一旦設定了 SET TRANSACTION 隔離等級語句的連接，它會持續有效，直到連接關閉或設定了另一個隔離等級為止。 當連接關閉並傳回集區時，會保留最後一個 SET TRANSACTION 隔離等級語句的隔離等級。 後續連接重複使用共用的連接，會使用在連線共用時生效的隔離等級。  
  
在連接內發出的個別查詢可以包含鎖定提示，以修改單一語句或交易的隔離，但不會影響連接的隔離等級。 在預存程式或函數中設定的隔離等級或鎖定提示，並不會變更呼叫它們之連接的隔離等級，而且只會在預存過程或函式呼叫的持續時間內生效。  
  
舊版的 SQL Server 支援四種 SQL-92 標準中所定義的隔離等級：  
  
- 讀取未認可是最不嚴格的隔離等級，因為它會忽略其他交易所放置的鎖定。 在讀取未認可下執行的交易，可能會讀取其他交易尚未認可的已修改資料值;這些稱為「已變更」的讀取。  
  
- READ COMMITTED 是 SQL Server 的預設隔離等級。 它會藉由指定語句無法讀取已經修改但尚未由其他交易認可的資料值，來防止中途讀取。 其他交易仍然可以在目前交易內個別語句的執行之間修改、插入或刪除資料，導致無法重複的讀取或「虛設」資料。  
  
- 可重複讀取是比讀取認可更嚴格的隔離等級。 它包含讀取認可，此外也指定在目前的交易認可之前，沒有其他交易可修改或刪除目前交易已讀取的資料。 平行存取低於讀取認可，因為在交易期間會保留讀取資料的共用鎖定，而不是在每個語句的結尾釋放。  
  
- SERIALIZABLE 是限制最嚴格的隔離等級，原因為其鎖定了索引鍵的整個範圍，且會將鎖定保留到交易完成。 它包含可重複讀取，並新增其他交易無法將新資料列插入至交易已讀取之範圍的限制，直到交易完成為止。  
  
如需詳細資訊，請參閱[交易鎖定與資料列版本設定指南](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md)。  
  
### <a name="snapshot-isolation-level-extensions"></a>Snapshot 隔離等級擴充功能  
SQL Server 在引進 SNAPSHOT 隔離等級的同時，還引進了 SQL-92 隔離等級的延伸模組及 READ COMMITTED 的其他實作。 READ_COMMITTED_SNAPSHOT 隔離等級可透明地取代所有交易的 READ COMMITTED。  
  
- SNAPSHOT 隔離會指定在交易內讀取的資料永遠不會反映其他同時交易所做的變更。 交易開始時，會使用存在的資料列版本。 讀取時不會對資料進行鎖定，因此快照集交易不會封鎖其他交易寫入資料。 寫入資料的交易不會封鎖快照集交易讀取資料。 您必須設定 ALLOW_SNAPSHOT_ISOLATION 資料庫選項來啟用快照集隔離，才能使用它。  
  
- READ_COMMITTED_SNAPSHOT 資料庫選項會決定在資料庫中啟用快照集隔離時，預設讀取認可隔離等級的行為。 如果您未明確指定 READ_COMMITTED_SNAPSHOT ON，則會將讀取認可套用至所有隱含交易。 這會產生與設定 READ_COMMITTED_SNAPSHOT OFF （預設值）相同的行為。 當 READ_COMMITTED_SNAPSHOT OFF 生效時，資料庫引擎會使用共用鎖定來強制執行預設隔離等級。 如果您將 READ_COMMITTED_SNAPSHOT 資料庫選項設為 [開啟]，資料庫引擎就會使用資料列版本設定和快照集隔離做為預設值，而不是使用鎖定來保護資料。  
  
## <a name="how-snapshot-isolation-and-row-versioning-work"></a>快照集隔離和資料列版本設定的工作方式  
啟用 SNAPSHOT 隔離等級之後，每次更新資料列時，SQL Server 資料庫引擎都會在 **tempdb** 中儲存原始資料列的複本，並將交易序號新增至資料列。 以下是發生的事件順序：  
  
1. 隨即會起始新的交易，並將交易序號指派給它。  
  
2. 資料庫引擎會讀取交易內的資料列，並從 **tempdb** 擷取序號與該交易序號最接近且低於它的資料列版本。  
  
3. 資料庫引擎檢查交易序號是否不在快照集交易啟動時，未認可交易的交易序號清單中。  
  
4. 交易從 **tempdb** 讀取交易開始時的資料列版本。 它不會在啟動交易之後看到插入的新資料列，因為這些序號值會高於交易序號的值。  
  
5. 目前的交易可以看到交易開始後刪除的資料列，原因為 **tempdb** 中會有一個序號值較低的資料列版本。  
  
快照集隔離的最後結果是交易會看到交易開始時所存在的所有資料，而不會在基礎資料表上接受或放置任何鎖定。 這可能會在發生爭用的情況下導致效能改進。  
  
快照集交易一律會使用開放式並行存取控制，並將任何會防止其他交易更新資料列的鎖定取消預繳。 如果快照集交易嘗試將更新認可至交易開始後變更的資料列，則會回復交易，並引發錯誤。  
  
## <a name="working-with-snapshot-isolation-in-adonet"></a>在 ADO.NET 中使用快照集隔離  
<xref:Microsoft.Data.SqlClient.SqlTransaction> 類別支援 ADO.NET 中的快照集隔離。 如果已啟用資料庫的快照集隔離，但並未設定 READ_COMMITTED_SNAPSHOT ON，則必須在呼叫 <xref:Microsoft.Data.SqlClient.SqlConnection.BeginTransaction%2A> 方法時，使用 **IsolationLevel.Snapshot** 列舉值來初始化 <xref:Microsoft.Data.SqlClient.SqlTransaction>。 此程式碼片段假設連接是開啟的 <xref:Microsoft.Data.SqlClient.SqlConnection> 物件。  
  
```csharp  
SqlTransaction sqlTran =   
  connection.BeginTransaction(IsolationLevel.Snapshot);  
```  
  
### <a name="example"></a>範例  
下列範例示範不同的隔離等級如何藉由嘗試存取鎖定的資料來運作，而且不打算用於實際執行的程式碼中。  
  
該程式碼會連線至 SQL Server 中的 **AdventureWorks** 範例資料庫，並會建立名為 **TestSnapshot** 的資料表並插入一個資料列。 程式碼會使用 ALTER DATABASE Transact-sql 語句來開啟資料庫的快照集隔離，但不會設定 READ_COMMITTED_SNAPSHOT 選項，讓預設的讀取認可隔離層級行為生效。 然後，程式碼會執行下列動作：  
  
1. 它會開始但不會完成 sqlTransaction1，這會使用 SERIALIZABLE 隔離等級來啟動更新交易。 這有鎖定資料表的效果。  
  
2. 其會開啟第二個連線並使用 SNAPSHOT 隔離等級初始化第二筆交易，以讀取 **TestSnapshot** 資料表中的資料。 因為已啟用快照集隔離，所以此交易可以讀取 sqlTransaction1 開始之前已存在的資料。  
  
3. 它會開啟第三個連接，並使用讀取認可隔離等級來起始交易，以嘗試讀取資料表中的資料。 在這種情況下，程式碼無法讀取資料，原因為第一個交易在資料表上設定的鎖定阻止其讀取資料並發生逾時。如果使用 REPEATABLE READ 及 SERIALIZABLE 隔離等級也會導致相同的結果，原因為第一個交易設定的鎖定也會阻止這些隔離等級進行讀取。  
  
4. 它會開啟第四個連接，並使用讀取未認可隔離等級來起始交易，這會在 sqlTransaction1 中執行未認可值的已中途讀取。 如果未認可第一個交易，此值可能永遠不會存在於資料庫中。  
  
5. 其會復原第一筆交易，並藉由刪除 **TestSnapshot** 資料表及停用 **AdventureWorks** 資料庫的快照集隔離來進行清除。  
  
> [!NOTE]
>  下列範例會使用相同的連接字串，並關閉連接共用。 如果連接已集區，重設其隔離等級並不會重設伺服器上的隔離等級。 因此，使用相同共用內部連線的後續連線，會從其隔離等級開始，並設定為共用的連線。 關閉連接共用的替代方法是針對每個連接明確設定隔離等級。  
  
[!code-csharp[DataWorks Isolation_Snapshot.Demo#1](~/../sqlclient/doc/samples/Isolation_Snapshot.cs#1)]
  
### <a name="example"></a>範例  
下列範例示範在修改資料時，快照集隔離的行為。 此程式碼會執行下列動作：  
  
1. 連線至 **AdventureWorks** 範例資料庫並啟用 SNAPSHOT 隔離。  
  
2. 建立名為 **TestSnapshotUpdate** 的資料表並插入三列範例資料。  
  
3. 會開始，但不會完成，使用快照集隔離來 sqlTransaction1。 在交易中選取了三個數據列。  
  
4. 為 **AdventureWorks** 建立第二個 **SqlConnection**，並建立第二個使用 READ COMMITTED 隔離等級的交易，其會更新 sqlTransaction1 中所選取其中一個資料列內的值。  
  
5. 認可 sqlTransaction2。  
  
6. 回到 sqlTransaction1，並嘗試更新 sqlTransaction1 已認可的相同資料列。 會引發錯誤3960，並自動復原 sqlTransaction1。 **SqlException.Number** 及 **SqlException.Message** 顯示在 [主控台] 視窗中。  
  
7. 執行清除程式碼以關閉 **AdventureWorks** 中的快照集隔離，並刪除 **TestSnapshotUpdate** 資料表。  
  
    [!code-csharp[DataWorks Isolation_Snapshot1#1](~/../sqlclient/doc/samples/Isolation_Snapshot1.cs#1)]
  
### <a name="using-lock-hints-with-snapshot-isolation"></a>使用鎖定提示與快照集隔離  
在上一個範例中，第一個交易會選取資料，第二筆交易則會在第一筆交易完成之前更新資料，而當第一筆交易嘗試更新相同的資料列時，就會產生更新衝突。 您可以在交易開始時提供鎖定提示，以減少長時間執行之快照集交易中發生更新衝突的機會。 下列 SELECT 語句使用 UPDLOCK 提示來鎖定選取的資料列：  
  
```sql  
SELECT * FROM TestSnapshotUpdate WITH (UPDLOCK)   
  WHERE PriKey BETWEEN 1 AND 3  
```  
  
使用 UPDLOCK 鎖定提示，會封鎖在第一個交易完成之前嘗試更新資料列的任何資料列。 這可確保選取的資料列在交易之後更新時不會發生衝突。 請參閱 SQL Server 線上叢書中的「鎖定提示」。  
  
如果您的應用程式有多個衝突，快照集隔離可能不是最佳選擇。 提示應該只在真的需要時才使用。 您的應用程式不應該設計成會持續依賴鎖定提示來進行操作。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)
- [交易鎖定與資料列版本設定指南](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md)
