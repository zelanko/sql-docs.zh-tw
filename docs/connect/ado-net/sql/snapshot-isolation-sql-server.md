---
title: SQL Server 中的快照集隔離
description: 描述對快照集隔離的支援，這是為了減少交易式應用程式中的封鎖而設計的資料列版本設定機制。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 43ae5dd3-50f5-43a8-8d01-e37a61664176
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 2d2e27fafabc259be6bfbc0137b66e34d310f449
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251151"
---
# <a name="snapshot-isolation-in-sql-server"></a>SQL Server 中的快照集隔離

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

快照集隔離可增強 OLTP 應用程式的並行存取。  
  
## <a name="understanding-snapshot-isolation-and-row-versioning"></a>了解快照集隔離與資料列版本設定  
一旦啟用快照集隔離，即會在 **tempdb** 中維護每筆交易所更新的資料列版本。 唯一的交易序號會識別每個交易，而且會針對每個資料列版本記錄這些唯一的編號。 交易適用於在交易序號之前具有序號的最新資料列版本。 交易會忽略在交易開始之後所建立的較新資料列版本。  
  
「快照集」一詞反映了交易中的所有查詢都會根據交易開始時資料庫的狀態，看到資料庫的相同版本或快照集。 不會在快照集交易中的底層資料列或資料分頁上取得任何鎖定，這會允許其他交易執行，而不會遭先前未完成的交易封鎖。 修改資料的交易不會封鎖讀取資料的交易，而讀取資料的交易不會封鎖寫入資料的交易，因為它們通常會在 SQL Server 中預設的 READ COMMITTED 隔離等級之下。 此非封鎖性的行為也會大幅降低複雜交易發生死結的可能性。  
  
快照集隔離會使用開放式並行存取模型。 如果快照集交易嘗試認可自交易開始後已變更的資料修改，交易將會回復並引發錯誤。 您可以針對存取要修改之資料的 SELECT 陳述式使用 UPDLOCK 提示，以避免發生這種情況。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜鎖定提示＞。  
  
在交易中使用快照集隔離之前，必須先透過設定 [ALLOW_SNAPSHOT_ISOLATION ON] 資料庫選項將其啟用。 如此會啟動在暫存資料庫 (**tempdb**) 中儲存資料列版本的機制。 您必須在使用 Transact-SQL ALTER DATABASE 陳述式的每個資料庫中啟用快照集隔離。 在這方面，快照集隔離與 READ COMMITTED、REPEATABLE READ、SERIALIZABLE 和 READ UNCOMMITTED 的傳統隔離等級不同，上述等級不需要任何設定。 下列陳述式會啟用快照集隔離，並以 SNAPSHOT 取代預設的 READ COMMITTED 行為：  
  
```sql  
ALTER DATABASE MyDatabase  
SET ALLOW_SNAPSHOT_ISOLATION ON  
  
ALTER DATABASE MyDatabase  
SET READ_COMMITTED_SNAPSHOT ON  
```  
  
設定 [READ_COMMITTED_SNAPSHOT ON] 選項可讓您存取預設 READ COMMITTED 隔離等級下已建立版本的資料列。 如果 [READ_COMMITTED_SNAPSHOT] 選項設定為 [OFF]，您必須明確設定每個工作階段的快照集隔離等級，才能存取已建立版本的資料列。  
  
## <a name="managing-concurrency-with-isolation-levels"></a>管理具有隔離等級的並行存取  
Transact-SQL 陳述式執行時所用的隔離等級會決定其鎖定與資料列版本設定行為。 隔離等級具有全連線的範圍，一旦針對連線使用 SET TRANSACTION ISOLATION LEVEL 陳述式進行設定，就會維持有效狀態，直到連線關閉或設定了另一個隔離等級為止。 當連線關閉並返回集區時，會保留最後一個 SET TRANSACTION ISOLATION LEVEL 陳述式的隔離等級。 重複使用共用連線的後續連線，會使用在共用連線時有效的隔離等級。  
  
在連線內發出的個別查詢可以包含鎖定提示，以修改單一陳述式或交易的隔離，但不會影響連線的隔離等級。 在預存程序或函式中設定的隔離等級或鎖定提示，並不會變更呼叫它們之連線的隔離等級，而且只會在預存程序或函式呼叫的持續時間內有效。  
  
舊版的 SQL Server 支援四種 SQL-92 標準中定義的隔離等級：  
  
- READ UNCOMMITTED 是最不嚴格的隔離等級，因為這會忽略其他交易所進行的鎖定。 在 READ UNCOMMITTED 下執行的交易可以讀取其他交易尚未認可的已修改資料值；這些稱為「中途」讀取。  
  
- READ COMMITTED 是 SQL Server 的預設隔離等級。 這會透過指定陳述式無法讀取已修改但尚未由其他交易認可的資料值，來防止中途讀取。 其他交易仍然可以在目前交易內個別陳述式的執行之間修改、插入或刪除資料，導致無法重複的讀取或「虛設項目」資料。  
  
- REPEATABLE READ 是比 READ COMMITTED 嚴格的隔離等級。 其包含 READ COMMITTED，而且會額外指定在目前的交易認可之前，沒有其他交易可修改或刪除目前交易已讀取的資料。 並行存取低於 READ COMMITTED，因為在交易期間會保留讀取資料上的共用鎖定，而不是在每個陳述式結尾處釋放。  
  
- SERIALIZABLE 是限制最嚴格的隔離等級，原因為其鎖定了索引鍵的整個範圍，且會將鎖定保留到交易完成。 其包含 REPEATABLE READ，並加上一個限制，就是在交易完成之前，其他交易無法將新資料列插入至已由交易讀取的範圍。  
  
如需詳細資訊，請參閱[交易鎖定與資料列版本設定指南](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md)。  
  
### <a name="snapshot-isolation-level-extensions"></a>快照集隔離等級延伸模組  
SQL Server 在引進 SNAPSHOT 隔離等級的同時，還引進了 SQL-92 隔離等級的延伸模組及 READ COMMITTED 的其他實作。 READ_COMMITTED_SNAPSHOT 隔離等級可透明地取代所有交易的 READ COMMITTED。  
  
- SNAPSHOT 隔離會指定交易內讀取的資料永遠不會反映其他同時交易所做的變更。 交易會使用在交易開始時已存在的資料列版本。 讀取時不會對資料進行鎖定，因此 SNAPSHOT 交易不會封鎖其他交易寫入資料。 寫入資料的交易不會封鎖快照集交易讀取資料。 您必須透過設定 [ALLOW_SNAPSHOT_ISOLATION] 資料庫選項來啟用快照集隔離，才能使用該功能。  
  
- 當資料庫中啟用快照集隔離時，[READ_COMMITTED_SNAPSHOT] 資料庫選項會決定預設 READ COMMITTED 隔離等級的行為。 如果您未明確指定 [READ_COMMITTED_SNAPSHOT ON]，則會將 [READ COMMITTED] 套用至所有隱含交易。 這會產生與設定 [READ_COMMITTED_SNAPSHOT OFF] \(預設值\) 相同的行為。 當 [READ_COMMITTED_SNAPSHOT OFF] 生效時，資料庫引擎會使用共用鎖定來強制執行預設的隔離等級。 如果將 [READ_COMMITTED_SNAPSHOT] 資料庫選項設定為 [ON]，資料庫引擎就會使用資料列版本設定與快照集隔離作為預設值，而不是使用鎖定來保護資料。  
  
## <a name="how-snapshot-isolation-and-row-versioning-work"></a>快照集隔離與資料列版本設定的運作方式  
啟用 SNAPSHOT 隔離等級之後，每次更新資料列時，SQL Server 資料庫引擎都會在 **tempdb** 中儲存原始資料列的複本，並將交易序號新增至資料列。 以下是事件的發生順序：  
  
1. 系統會起始新交易，並指派交易序號給新交易。  
  
2. 資料庫引擎會讀取交易內的資料列，並從 **tempdb** 擷取序號與該交易序號最接近且低於它的資料列版本。  
  
3. 資料庫引擎會檢查當快照集交易開始時，交易序號是否不在作用中未認可交易的交易序號清單中。  
  
4. 交易從 **tempdb** 讀取交易開始時的資料列版本。 您不會在交易開始之後看到插入的新資料列，因為那些序號值將會高於交易序號的值。  
  
5. 目前的交易可以看到交易開始後刪除的資料列，原因為 **tempdb** 中會有一個序號值較低的資料列版本。  
  
快照集隔離的淨效應是交易會看到交易開始時已存在的所有資料，而不會在底層資料表上接受或進行任何鎖定。 這能夠會在發生競爭的情況下造成效能提升。  
  
快照集交易一律會使用開放式並行存取控制，並將保留任何會防止其他交易更新資料列的鎖定。 如果快照集交易嘗試認可在交易開始後所變更資料列的更新，則會回復交易，並引發錯誤。  
  
## <a name="working-with-snapshot-isolation-in-adonet"></a>在 ADO.NET 中使用快照集隔離  
ADO.NET 中透過 <xref:Microsoft.Data.SqlClient.SqlTransaction> 類別支援快照集隔離。 如果已啟用資料庫的快照集隔離，但並未設定 READ_COMMITTED_SNAPSHOT ON，則必須在呼叫 <xref:Microsoft.Data.SqlClient.SqlConnection.BeginTransaction%2A> 方法時，使用 **IsolationLevel.Snapshot** 列舉值來初始化 <xref:Microsoft.Data.SqlClient.SqlTransaction>。 此程式碼片段會假設連線是開啟的 <xref:Microsoft.Data.SqlClient.SqlConnection> 物件。  
  
```csharp  
SqlTransaction sqlTran =   
  connection.BeginTransaction(IsolationLevel.Snapshot);  
```  
  
### <a name="example"></a>範例  
下列範例示範不同的隔離等級如何透過嘗試存取鎖定的資料來運作，而且這不適合在實際執行的程式碼中使用。  
  
該程式碼會連線至 SQL Server 中的 **AdventureWorks** 範例資料庫，並會建立名為 **TestSnapshot** 的資料表並插入一個資料列。 此程式碼會使用 ALTER DATABASE Transact-SQL 陳述式來開啟資料庫的快照集隔離，但不會設定 [READ_COMMITTED_SNAPSHOT 選項]，讓預設的 READ COMMITTED 隔離等級行為生效。 然後此程式碼會執行下列動作：  
  
1. 其會開始但不會完成 sqlTransaction1，這會使用 SERIALIZABLE 隔離等級來啟動更新交易。 這具有鎖定資料表的效果。  
  
2. 其會開啟第二個連線並使用 SNAPSHOT 隔離等級初始化第二筆交易，以讀取 **TestSnapshot** 資料表中的資料。 因為已啟用快照集隔離，所以此交易可以讀取 sqlTransaction1 開始之前已存在的資料。  
  
3. 其會開啟第三個連線，並使用 READ COMMITTED 隔離等級來起始交易，以嘗試讀取資料表中的資料。 在這種情況下，程式碼無法讀取資料，原因為第一個交易在資料表上設定的鎖定阻止其讀取資料並發生逾時。如果使用 REPEATABLE READ 及 SERIALIZABLE 隔離等級也會導致相同的結果，原因為第一個交易設定的鎖定也會阻止這些隔離等級進行讀取。  
  
4. 其會開啟第四個連線，並使用 READ UNCOMMITTED 隔離等級來起始交易，這會在 sqlTransaction1 中執行未認可值的中途讀取。 如果未認可第一個交易，這個值可能永遠不會實際存在於資料庫中。  
  
5. 其會復原第一筆交易，並藉由刪除 **TestSnapshot** 資料表及停用 **AdventureWorks** 資料庫的快照集隔離來進行清除。  
  
> [!NOTE]
>  下列範例會使用相同的連接字串，但會關閉連線共用。 如果連線已共用，重設其隔離等級並不會重設伺服器的隔離等級。 因此，使用相同共用內部連線的後續連線，會以其設定至共用連線的隔離等級啟動。 關閉連線共用的替代方法是為每個連線明確設定隔離等級。  
  
[!code-csharp[DataWorks Isolation_Snapshot.Demo#1](~/../sqlclient/doc/samples/Isolation_Snapshot.cs#1)]
  
### <a name="example"></a>範例  
下列範例示範修改資料時，快照集隔離的行為。 此程式碼會執行下列動作：  
  
1. 連線至 **AdventureWorks** 範例資料庫並啟用 SNAPSHOT 隔離。  
  
2. 建立名為 **TestSnapshotUpdate** 的資料表並插入三列範例資料。  
  
3. 會使用 SNAPSHOT 隔離來開始 (但不會完成) sqlTransaction1。 已在交易中選取了三個資料列。  
  
4. 為 **AdventureWorks** 建立第二個 **SqlConnection**，並建立第二個使用 READ COMMITTED 隔離等級的交易，其會更新 sqlTransaction1 中所選取其中一個資料列內的值。  
  
5. 認可 sqlTransaction2。  
  
6. 返回 sqlTransaction1，並嘗試更新 sqlTransaction1 已認可的相同資料列。 會引發錯誤 3960，並自動復原 sqlTransaction1。 **SqlException.Number** 及 **SqlException.Message** 顯示在 [主控台] 視窗中。  
  
7. 執行清除程式碼以關閉 **AdventureWorks** 中的快照集隔離，並刪除 **TestSnapshotUpdate** 資料表。  
  
    [!code-csharp[DataWorks Isolation_Snapshot1#1](~/../sqlclient/doc/samples/Isolation_Snapshot1.cs#1)]
  
### <a name="using-lock-hints-with-snapshot-isolation"></a>搭配快照集隔離使用鎖定提示  
在上一個範例中，第一個交易會選取資料，第二個交易可以在第一個交易即將完成之前更新資料，進而導致當第一個交易嘗試更新相同的資料列時發生更新衝突。 您可以透過在交易開始時提供鎖定提示，以減少長時間執行之快照集交易中發生更新衝突的機會。 下列 SELECT 陳述式使用 UPDLOCK 提示來鎖定選取的資料列：  
  
```sql  
SELECT * FROM TestSnapshotUpdate WITH (UPDLOCK)   
  WHERE PriKey BETWEEN 1 AND 3  
```  
  
使用 UPDLOCK 鎖定提示會封鎖在第一個交易完成之前嘗試更新資料列的任何資料列。 這可確保選取的資料列之後在交易中更新時不會發生衝突。 請參閱《SQL Server 線上叢書》中的＜鎖定提示＞。  
  
如果您的應用程式有許多衝突，快照集隔離可能就不是最佳選擇。 提示應該只在真正需要時才使用。 您的應用程式不應該設計成會持續依賴鎖定提示來執行其作業。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)
- [交易鎖定與資料列版本設定指南](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md)
