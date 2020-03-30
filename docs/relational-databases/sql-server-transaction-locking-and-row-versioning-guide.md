---
title: 交易鎖定與資料列版本設定指南
ms.custom: seo-dt-2019
ms.date: 03/10/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- guide, transaction locking and row versioning
- transaction locking and row versioning guide
- lock compatibility matrix, [SQL Server]
- lock granularity and hierarchies, [SQL Server]
- deadlocks, [SQL Server]
- lock escalation, [SQL Server]
- lock partitioning, [SQL Server]
ms.assetid: 44fadbee-b5fe-40c0-af8a-11a1eecf6cb7
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7b7341273c36bacdbfd49596df535b9c73ba5049
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "79287172"
---
# <a name="transaction-locking-and-row-versioning-guide"></a>交易鎖定與資料列版本設定指南
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

任何資料庫若交易管理不當，時常會導致多使用者的系統發生競爭與效能問題。 隨著存取資料的使用者數量增加，能夠有效使用交易的應用程式更形重要。 本指南描述 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 用以確保每筆交易實體完整性的鎖定及資料列版本設定機制，並提供有關應用程式如何能夠有效控制交易的資訊。  
  
**適用於**：[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ([!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 至 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]，除非另有註明) 以及 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]。 
  
##  <a name="transaction-basics"></a><a name="Basics"></a> 交易基本概念  
 交易就是以單一工作邏輯單元執行的一連串作業。 工作邏輯單元必須呈現出四種屬性，即不可部份完成性 (Atomicity)、一致性 (Consistency)、隔離性 (Isolation) 與耐久性 (Durability) 屬性，稱為 ACID，才能有資格成為一筆交易。  
  
 **不可部份完成性**  
 交易必須是不可部分完成 (Atomic) 的工作單位；資料的修改若非全部執行，就是全部不執行。  
  
 **一致性**  
 交易完成時，所有資料必須維持一致的狀態。 在關聯式資料庫 (Relational Database) 中，必須將所有的規則 (Rule) 套用於交易的修改，以維護所有的資料整合性 (Integrity)。 所有的內部資料結構，例如 B 型樹狀結構索引 (B-tree Index) 或是雙向連結串列 (Doubly-Linked List)，在交易終止時必須是正確的。  
  
 **隔離**  
 並行交易所做的修改，必須與任何其他並行交易所做的修改隔離。 交易所辨識的資料不是處於另一筆並行的交易修改資料之前的狀態，就是處於第二筆交易完成後的狀態，但是卻無法辨識中繼狀態。 這稱為序列化能力 (Serializability)，因為這樣可以產生重新載入起始資料並重新執行一系列的交易，以便讓資料最終能夠與原始交易執行後的狀態相同的能力。  
  
 **耐久性**  
 完全持久交易完成之後，其作用便永遠存在於系統之中。 即使發生系統失敗仍會保存修改。 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 和更新版本支援延遲的持久交易。 延遲的持久交易會在交易記錄檔記錄永久保存到磁碟之前認可。 如需有關延遲交易持久性的詳細資訊，請參閱[交易持久性](../relational-databases/logs/control-transaction-durability.md)主題。  
  
 SQL 程式設計者負責在強制資料邏輯一致性 (Consistency) 的點上啟動與結束交易。 程式設計者必須定義資料修改順序，讓資料維持在與組織的商業規則有關的一致性狀態。 然後再由程式設計者將這些修改陳述式包含於單一的交易中，這樣 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 便得以強制交易的實體完整性。  
  
 提供可確保每一筆交易實體完整性的機制是企業資料庫系統 (例如 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]的執行個體) 的責任。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 提供：  
  
-   保持交易隔離性 (Isolation) 的鎖定機能 (Locking Facility)。  
  
-   記錄機能可確保交易持久性。 針對完全持久交易，記錄檔記錄會在交易認可之前強行寫入磁碟。 因此，即使伺服器硬體、作業系統或 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 執行個體本身失敗，該執行個體仍會在重新啟動時，使用交易記錄檔來將所有未完成的交易自動復原到系統失敗點。 延遲的持久交易會在交易記錄檔記錄強行寫入磁碟之前認可。 如果在記錄檔記錄先強行寫入磁碟之前發生系統失敗，這類交易可能會遺失。 如需有關延遲交易持久性的詳細資訊，請參閱[交易持久性](../relational-databases/logs/control-transaction-durability.md)主題。  
  
-   強制不可部份完成性 (Atomicity) 與一致性的交易管理功能。 交易在啟動之後必須成功地完成 (認可)，否則 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會將交易啟動後所做的所有資料修改動作復原。 這項作業稱為回復交易，因為資料將恢復為任何變更發生之前的狀態。  
  
### <a name="controlling-transactions"></a>控制交易  
 應用程式主要是透過指定交易何時啟動及結束來控制交易。 這可利用 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式或資料庫應用程式開發介面 (API) 函數來指定。 系統也必須能夠正確地處理交易完成之前便結束交易的錯誤。 如需詳細資訊，請參閱[交易](../t-sql/language-elements/transactions-transact-sql.md)、[ODBC 中的交易](../relational-databases/native-client/odbc/performing-transactions-in-odbc.md) 及 [SQL Server Native Client (OLEDB) 中的交易](../relational-databases/native-client-ole-db-transactions/transactions.md)。  
  
 依照預設，會在連接層級管理交易。 在連接上啟動交易時，連接上執行的所有 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式在交易結束之前都是該交易的一部分。 但是，在 Multiple Active Result Set (MARS) 工作階段下， [!INCLUDE[tsql](../includes/tsql-md.md)] 明確或不明確交易會成為在批次層級管理的批次範圍交易。 當批次完成時，如果未認可或回復批次範圍的交易， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]會自動回復它。 如需詳細資訊，請參閱[使用 Multiple Active Result Sets (MARS)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)。  
  
#### <a name="starting-transactions"></a>啟動交易  
 使用 API 函數和 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式，您可以在 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的執行個體中，以明確、自動認可或隱含來啟動交易。  
  
 **明確交易**  
 外顯交易是透過 API 函數或藉由發出 [!INCLUDE[tsql](../includes/tsql-md.md)] BEGIN TRANSACTION、COMMIT TRANSACTION、COMMIT WORK、ROLLBACK TRANSACTION 或 ROLLBACK WORK [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式，明確定義交易的啟動與結束的一種交易。 當交易結束時，連線便會回到外顯交易啟動之前的交易模式，可能是隱含或自動認可模式。  
  
 您可以在明確的交易中，使用下列陳述式以外的所有 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式：  
  
||||  
|-|-|-|  
|ALTER DATABASE|CREATE DATABASE|DROP FULLTEXT INDEX|  
|ALTER FULLTEXT CATALOG|CREATE FULLTEXT CATALOG|RECONFIGURE|  
|ALTER FULLTEXT INDEX|CREATE FULLTEXT INDEX|RESTORE|  
|備份|DROP DATABASE|全文檢索系統預存程序|  
|CREATE DATABASE|DROP FULLTEXT CATALOG|由 sp_dboption 設定資料庫選項，或於外顯或隱含交易中修改 master 資料庫的任何系統程序。|  
  
> [!NOTE]  
> UPDATE STATISTICS 可於外顯交易內使用。 但是，UPDATE STATISTICS 認可與含括交易無關，而且無法回復。  
  
 **自動認可交易**  
 自動認可模式是 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的預設交易管理模式。 每一個 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式都會在完成時認可或回復。 陳述式如果成功地完成便被認可；若是遇到任何錯誤則被復原。 只要這個預設模式沒有被外顯交易或隱含交易覆寫，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 執行個體的連接都會在自動認可模式下操作。 自動認可模式也是 ADO、OLE DB、ODBC 與資料程式庫的預設模式。  
  
 **隱含交易**  
 在隱含交易模式中操作連接時，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的執行個體會在目前交易完成認可或回復後，自動啟動新的交易。 您不需描述交易的啟動；只要認可或復原每一筆交易即可。 隱含交易模式產生連續的交易鍊。 透過 API 函數或 [!INCLUDE[tsql](../includes/tsql-md.md)] SET IMPLICIT_TRANSACTIONS ON 陳述式，可將隱含交易模式設為開啟。  這種模式也稱為 Autocommit OFF，請參閱 [JDBC 中的 setAutoCommit 方法](../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md) 
  
 當連接的隱含交易模式設定為開啟之後， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的執行個體便會在第一次執行下列任一個陳述式時，自動啟動一筆交易：  
  
||||  
|-|-|-|  
|ALTER TABLE|FETCH|REVOKE|  
|CREATE|GRANT|SELECT|  
|刪除|Insert|TRUNCATE TABLE|  
|DROP|OPEN|UPDATE|  
  
-  **批次範圍交易**  
   僅適用於 Multiple Active Result Sets (MARS)，在 MARS 工作階段下啟動的 [!INCLUDE[tsql](../includes/tsql-md.md)] 外顯或隱含交易會變成批次範圍的交易。 當批次完成時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]會自動回復未認可或回復之批次範圍的交易。  
  
-  **分散式交易**  
   分散式交易跨越二或多個稱為資源管理員的伺服器。 交易的管理必須由一種稱為交易管理員的伺服器元件在資源管理員之間協調。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的每個執行個體在分散式交易中可作為資源管理員來運作，而由交易管理員 (例如 [!INCLUDE[msCoName](../includes/msconame-md.md)] 分散式交易協調器 (MS DTC)) 或其他支援分散式交易處理的 Open Group XA 規格之交易管理員來協調分散式交易。 如需詳細資訊，請參閱 MS DTC 文件集。  
  
   在單一 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 執行個體內部，跨越二或多個資料庫的交易，實際上就是分散式交易。 執行個體是由內部來管理分散式交易；而對於使用者而言則是以本機交易來運作。  
  
   在應用程式中，分散式交易的管理與本機交易大致相同。 交易結束時，應用程式便要求認可或回復交易。 分散式認可必須另由交易管理員來管理，以便將網路失敗可能會造成某些資源管理員成功認可而其他資源管理員卻將交易回復的風險降至最低。 這可藉由在兩個階段 (準備階段與認可階段) 中管理認可過程來達到，稱為兩階段認可交易 (Two-Phase Commit，2PC)。  
  
   -  **準備階段**  
      當交易管理員接收到認可的要求時，便傳送準備命令給所有參與交易的資源管理員。 然後再由每個資源管理員進行可讓交易持續，並把放置交易記錄檔影像的所有緩衝區排清到磁碟上所需的一切動作。 當每個資源管理員完成準備階段時，便將準備的成功或失敗結果傳回交易管理員。 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 導入了延遲的交易持久性。 認可延遲的持久交易會在交易的記錄檔映像排清至磁碟之前認可。 如需有關延遲交易持久性的詳細資訊，請參閱[交易持久性](../relational-databases/logs/control-transaction-durability.md)主題。  
  
   -  **認可階段**  
      如果交易管理員從所有的資源管理員接收到準備成功，便傳送認可命令給每個資源管理員。 然後資源管理員即可完成認可。 如果全部的資源管理員都報告認可成功，交易管理員便傳送成功的通知給應用程式。 若有任何資源管理員報告準備失敗，交易管理員便傳送回復命令給每個資源管理員並告知應用程式認可失敗。  
  
      [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 應用程式可以透過 [!INCLUDE[tsql](../includes/tsql-md.md)] 或資料庫 API 來管理分散式交易。 如需詳細資訊，請參閱 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)。  
  
#### <a name="ending-transactions"></a>結束交易  
 您可以使用 COMMIT 或 ROLLBACK 陳述式，或透過對應的 API 函數來結束交易。  
  
-  **COMMIT**  
   交易如果成功便會認可交易。 COMMIT 陳述式可以保證交易所做的全部修改，都會變成資料庫永久的一部分。 COMMIT 同時也會釋放資源，例如交易所使用的鎖定。  
  
-  **ROLLBACK**  
   如果交易中發生錯誤，或是使用者決定取消交易，便會將交易回復。 ROLLBACK 陳述式藉由將資料帶回到交易啟動時的狀態，來取消交易中進行的所有修改動作。 ROLLBACK 也會釋放交易所佔用的資源。  
  
> [!NOTE]  
> 在啟用支援 Multiple Active Result Set (MARS) 的連線下，當執行有擱置的要求時，無法認可透過 API 函數啟動的明確交易。 仍有未處理作業在執行時，任何嘗試認可此類型的要求將會導致錯誤。  
  
#### <a name="errors-during-transaction-processing"></a>交易處理期間的錯誤  
 如果因為錯誤而讓交易無法順利完成， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會自動回復交易，並釋放交易所佔用的一切資源。 如果用戶端與 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 執行個體之間的網路連接已中斷，該連接尚未處理完畢的交易會在網路通知該執行個體發生中斷時全部回復。 如果用戶端應用程式失敗或是用戶端電腦當機或重新啟動，也會中斷連接， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 執行個體會在網路通知已發生中斷時，回復所有尚未處理完畢的連接。 如果用戶端從應用程式登出，便會復原任何尚未處理完畢的交易。  
  
 如果批次中發生執行階段陳述式錯誤 (例如條件約束違規)， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的預設行為是只回復產生錯誤的陳述式。 您可以使用 `SET XACT_ABORT` 陳述式來變更這個行為。 在執行 `SET XACT_ABORT` ON 之後，任何執行階段陳述式錯誤都會導致自動復原目前的交易。 編譯錯誤 (例如語法錯誤) 並不受 `SET XACT_ABORT` 影響。 如需詳細資訊，請參閱 [SET XACT_ABORT &#40;Transact-SQL&#41;](../t-sql/statements/set-xact-abort-transact-sql.md)。  
  
 發生錯誤時，更正動作 (`COMMIT` 或 `ROLLBACK`) 應該包含在應用程式碼中。 其中一個處理錯誤 (包括交易中的錯誤) 的有效工具是 [!INCLUDE[tsql](../includes/tsql-md.md)] `TRY...CATCH` 建構。 如需有關包括交易之範例的詳細資訊，請參閱 [TRY...CATCH &#40;Transact-SQL&#41;](../t-sql/language-elements/try-catch-transact-sql.md)。 從 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 開始，您可以使用 `THROW` 陳述式來引發例外狀況，然後將執行轉移至 `TRY...CATCH` 建構的 `CATCH` 區塊。 如需詳細資訊，請參閱 [THROW &#40;Transact-SQL&#41;](../t-sql/language-elements/throw-transact-sql.md)。  
  
##### <a name="compile-and-run-time-errors-in-autocommit-mode"></a>自動認可模式下的編譯與執行階段錯誤  
 在自動認可模式中，有時 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 執行個體會好像已將整個批次回復，而非只有一個 SQL 陳述式。 這種情形只有遇到編譯錯誤時才會發生，執行階段錯誤則不會。 編譯錯誤會讓 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 無法建立執行計畫，因此批次中的任何陳述式都不會執行。 雖然產生錯誤的陳述式之前的所有陳述式都會回復，但錯誤會讓批次中的一切都不會執行。 在下列範例中，位於第三個批次的 `INSERT` 陳述式由於編譯錯誤而全部不執行。 前兩個 `INSERT` 陳述式由於並未執行而復原。  
  
```sql  
CREATE TABLE TestBatch (Cola INT PRIMARY KEY, Colb CHAR(3));  
GO  
INSERT INTO TestBatch VALUES (1, 'aaa');  
INSERT INTO TestBatch VALUES (2, 'bbb');  
INSERT INTO TestBatch VALUSE (3, 'ccc');  -- Syntax error.  
GO  
SELECT * FROM TestBatch;  -- Returns no rows.  
GO  
```  
  
 在下列範例中，第三個 `INSERT` 陳述式會產生執行階段重複的主索引鍵錯誤。 前兩個 `INSERT` 陳述式會成功並且受到認可，因此它們在執行階段錯誤之後仍會保留。  
  
```sql  
CREATE TABLE TestBatch (Cola INT PRIMARY KEY, Colb CHAR(3));  
GO  
INSERT INTO TestBatch VALUES (1, 'aaa');  
INSERT INTO TestBatch VALUES (2, 'bbb');  
INSERT INTO TestBatch VALUES (1, 'ccc');  -- Duplicate key error.  
GO  
SELECT * FROM TestBatch;  -- Returns rows 1 and 2.  
GO  
```  
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會使用延遲的名稱解析，直到執行時間才會解析物件名稱。 在下列範例中，前兩個 `INSERT` 陳述式會執行並認可，且這兩個資料列會在參考到不存在的資料表而產生執行階段錯誤的第三個 `TestBatch` 陳述式之後，仍然留在 `INSERT` 資料表。  
  
```sql  
CREATE TABLE TestBatch (Cola INT PRIMARY KEY, Colb CHAR(3));  
GO  
INSERT INTO TestBatch VALUES (1, 'aaa');  
INSERT INTO TestBatch VALUES (2, 'bbb');  
INSERT INTO TestBch VALUES (3, 'ccc');  -- Table name error.  
GO  
SELECT * FROM TestBatch;  -- Returns rows 1 and 2.  
GO  
```   
  
##  <a name="locking-and-row-versioning-basics"></a><a name="Lock_Basics"></a> 鎖定與資料列版本設定基本概念  
 當多個使用者同時存取資料時， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會使用下列機制來確保交易完整性，並維護資料庫一致性：  
  
-  **鎖定**    

   每一個交易會要求資源上不同類型的鎖定，例如交易相依的資料列、頁面或資料表。 鎖定會阻擋其他交易修改資源，以免造成要求鎖定的交易發生問題。 每一個交易對於鎖定的資源不再具有相依性時，就會釋放它的鎖定。  
  
-  **資料列版本設定**    

   啟用以資料列版本設定為基礎的隔離等級之後，「 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 」會維護每一個修改過的資料列的版本。 應用程式可指定交易使用資料列版本，來檢視交易或查詢開始時已存在的資料，而不是以鎖定來保護所有讀取。 透過使用資料列版本設定，讀取作業封鎖其他交易的機會可大幅降低。  
  
 鎖定和資料列版本設定可防止使用者讀取尚未認可的資料，以及防止多個使用者同時變更同一筆資料。 若未使用鎖定或資料列版本設定，則對資料執行查詢時，可能會傳回尚未在資料庫中認可的資料，因而產生非預期的結果。  
  
 應用程式可以選擇交易隔離等級，用於定義交易的保護層級，以免被其他交易修改。 另可對個別 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式指定資料表層級提示，進一步修改行為，以符合應用程式的需求。  
  
### <a name="managing-concurrent-data-access"></a>管理並行資料存取  
 多個使用者同時存取同一個資源可稱為並行存取資源。 並行資料存取需要一些機制，以防止多個使用者同時嘗試修改其他使用者目前正在使用的資源所造成的不利影響。  
  
#### <a name="concurrency-effects"></a>並行效果  
 使用者修改資料會影響到同時正在讀取或修改相同資料的其他使用者。 而我們就稱這些使用者正在並行地存取資料。 若資料儲存系統沒有並行控制功能，使用者會看到下列副作用：  
  
-   **更新遺失** 
  
     如果二或多個交易選取相同資料列，接著又根據原先選取的值來更新資料列時，就會發生更新遺失的情形。 每個交易並不知道有其他的交易存在。 因此最後的更新會覆寫其他交易所做的更新，而造成資料遺失。  
  
     例如，兩位編輯人員對同一份文件製作了電子副本。 這兩位編輯人員各自進行修改並儲存變更後的副本，覆寫了原始文件。 最後儲存已變更副本的編輯人員會覆寫前一位編輯人員所做的變更。 若第一位編輯人員完成和認可交易後才讓第二位編輯人員存取檔案的話，就能避免這個問題。  
  
-   **未認可相依性 (中途讀取)**  
  
     第二筆交易選擇的資料列已經被其他交易更新時，會發生未認可依存性 (Uncommitted Dependency)。 此時，第二筆交易讀取的是尚未認可且可能被更新資料列的交易變更之資料。  
  
     例如，有一位編輯人員正在修改一份電子文件。 進行變更時，第二位編輯人員複製了包含目前所有變更的文件，並將文件散發給預期的讀者。 此時，第一位編輯人員認為截至目前的變更均有誤，所以移除了原先的變更後儲存文件。 散發的文件包含了一些現在已不存在的修改內容，而且這些修改應該視為從未發生過。 如果能在第一位編輯人員儲存最後修改並認可交易後才允許其他人讀取修改過的文件，即可避免這個問題。  
  
-   **不一致分析 (不可重複讀取)**  
  
     第二筆交易存取同一資料列數次，且每次讀取的資料內容都有變動時，就會產生不一致分析 (Inconsistent Analysis)。 不一致分析的情況是第一筆交易在變更資料時，第二筆交易卻在讀取這些資料，其發生原理與未認可依存性類似。 但是在不一致分析中，第二筆交易讀取的資料是由進行變更的交易認可。 此外，不一致分析包括同一資料列的多次讀取 (兩次或以上)，且每次資訊均被其他交易變更，因此稱為不可重複讀取 (Nonrepeatable Read)。  
  
     例如，一位編輯人員兩次都讀取了相同的文件，但是在兩次讀取期間寫作人員重寫了文件。 因此在編輯者第二次讀取文件時，文件已經變更。 而原始讀取是不可重複的。 若能在編輯人員讀完文件後才讓寫作人員變更，就能避免這個問題。  
  
-   **虛設項目讀取**  
  
     虛設項目讀取是指當您執行兩個完全相同的查詢，但第二個查詢所傳回的資料列集合不同時所發生的情況。 下列範例會顯示可能發生這種情況的作業方式。 假設下列兩筆交易都同時執行。 第一筆交易中的兩個 `SELECT` 陳述式可能會傳回不同的結果，因為第二筆交易中的 `INSERT` 陳述式會變更這兩筆交易所使用的資料。  
  
    ```sql  
    --Transaction 1  
    BEGIN TRAN;  
    SELECT ID FROM dbo.employee  
    WHERE ID > 5 and ID < 10;  
    --The INSERT statement from the second transaction occurs here.  
    SELECT ID FROM dbo.employee  
    WHERE ID > 5 and ID < 10;  
    COMMIT;  
    ```  
  
    ```sql  
    --Transaction 2  
    BEGIN TRAN;  
    INSERT INTO dbo.employee  
      (Id, Name) VALUES(6 ,'New');  
    COMMIT;   
    ```  
  
-   **資料列更新造成遺漏讀取和重複讀取**  
  
    -   遺漏更新的資料列或多次看到更新的資料列  
  
         在 `READ UNCOMMITTED` 等級執行的交易不會發出共用鎖定來防止其他交易修改目前交易所讀取的資料。 執行 READ COMMITTED 等級的交易則會發出共用鎖定，但是在讀取資料列後，就會解除資料列或頁面的鎖定。 在以上任一種情況下，當您掃描索引時，如果其他使用者變更了您讀取期間之資料列的索引鍵資料行，在索引鍵變更將資料列移到掃描前的任何位置後，該資料列可能會再次出現。 同樣地，如果索引鍵變更將資料列移到您已經讀取之索引中的位置，該資料列可能就不會出現。 若要避免這種情況，請使用 `SERIALIZABLE` 或 `HOLDLOCK` 提示，或資料列版本設定。 如需詳細資訊，請參閱[資料表提示 &#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-table.md)。  
  
    -   遺失一或多個非更新目標的資料列  
  
         當您使用 `READ UNCOMMITTED` 時，如果您的查詢使用配置順序掃描 (使用 IAM 頁面) 來讀取資料列，則在另一個交易造成頁面分割時，您可能會遺失資料列。 當您使用認可的讀取時，不會發生這個狀況，因為頁面分割期間會將資料表保持在鎖定狀態下，而且，如果資料表沒有叢集索引，也不會發生這個狀況，因為更新不會造成頁面分割。  
  
#### <a name="types-of-concurrency"></a>並行的類型  
 當有許多人會同時嘗試修改資料庫中的資料時，必須實作一個控制系統，這樣某一個人所做的修改才不會嚴重影響到另一個人所做的修改。 這就叫做並行控制。  
  
 並行控制理論將制定並行控制的方法分為二類：  
  
-   **悲觀**並行控制  
  
     鎖定系統可防止使用者以會影響其他使用者的方法來修改資料。 使用者在執行某個動作而造成套用鎖定之後，其他使用者就不能執行會與該鎖定衝突的動作，直到擁有者解除鎖定為止。 這就叫做封閉式並行控制，因為這種方法主要是用在高度競爭資料的環境中，以鎖定方式來保護資料的成本，會低於發生並行衝突時回復交易的成本。  
  
-   **樂觀**並行控制  
  
     在開放式並行控制中，使用者在讀取資料時，不會將資料鎖定。 當使用者更新資料時，系統會查看在讀取資料之後，是否有其他使用者變更了該資料。 若有其他使用者更新了該資料，就會產生錯誤。 一般而言，收到錯誤的使用者會回復交易，並重新開始。 這就叫做開放式並行控制，因為這種方法主要是用在低度競爭資料的環境中，偶爾回復交易的成本會低於讀取時鎖定資料的成本。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支援並行控制的範圍。 使用者可針對連接來選取交易隔離等級，或是在資料指標上選取並行選項，以指定並行控制的類型。 這些屬性可用 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式來定義，或是透過資料庫應用程式開發介面 (API) (例如 ADO、ADO.NET、OLE DB 及 ODBC) 的內容及屬性來定義。  
  
#### <a name="isolation-levels-in-the-ssdenoversion"></a>[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]中的隔離等級  
 交易可指定隔離等級，以定義某個交易必須與其他交易所修改之資源或資料隔離的程度。 隔離等級是以並行副作用來表示，例如，允許中途讀取 (dirty read) 或虛設項目讀取 (phantom read)。  
  
 交易隔離等級控制：  
  
-   在讀取資料時是否採用鎖定，以及要求哪一類型的鎖定。  
-   保留讀取鎖定的時間長度。  
-   讀取作業是否參考另一個交易修改的資料列：  
    -   封鎖資料列上的獨佔鎖定直到釋放它為止。  
    -   擷取在啟動陳述式或交易時即存在的資料列認可版本。  
    -   讀取未認可的資料修改。  
  
> [!IMPORTANT]  
> 選擇交易隔離等級並不會影響為保護資料修改所取得的鎖定。 交易永遠都會取得它所修改之資料的獨佔鎖定，並保留該鎖定直到交易完成為止，不論為該交易所設定的隔離等級為何皆同。 對於讀取作業，交易隔離等級主要是定義對於其他交易所做修改之影響的保謢等級。  
  
 較低的隔離等級將可讓更多的使用者同時存取資料，但也會增加使用者可能遇到並行作用 (例如，中途讀取或遺失的更新) 的數目。 相反的，較高的隔離等級將可減少使用者遇到並行作用的類型，但是將需要更多的系統資源並且會增加一個交易封鎖另一個交易的可能性。 選擇適當的隔離等級需視應用程式的資料完整性需求與每個隔離等級的額外負荷平衡而定。 最高的隔離等級為可序列化，可確保每次交易重複讀取作業時都能擷取相同的資料，但它是透過執行鎖定層級來達成此目的，因此在多使用者系統中有可能會影響其他使用者。 最低隔離等級為讀取未認可，可能會擷取到其他交易已修改但尚未認可的資料。 在讀取未認可中可能會發生所有的並行副作用，但由於沒有讀取鎖定或版本控制，因此可將額外負荷降到最低。  
  
##### <a name="database-engine-isolation-levels"></a>Database Engine 隔離等級  
 ISO 標準會定義以下隔離等級， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]支援所有的這些隔離等級：  
  
|隔離等級|定義|  
|---------------------|----------------|  
|**讀取未認可**|最低隔離等級，隔離交易僅能確保不會讀取已實體損毀的資料。 這種等級下允許中途讀取，所以任何交易可能看得到其他交易所做的尚未認可變更。|  
|**讀取認可**|允許交易對另一筆交易先前讀取 (未修改) 的資料進行讀取，而不必等待前一筆交易完成。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 將維持寫入鎖定 (取自於選取的資料) 直到交易結束，但讀取鎖定會在 SELECT 作業一經執行時即釋放。 這是 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 預設等級。|  
|**可重複讀取**|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 將維持讀取及寫入鎖定 (取自於選取的資料) 直到交易結束。 不過由於範圍鎖定未受管理，便有可能發生虛設項目讀取。|  
|**可序列化**|最高的等級，使交易完全與其他交易隔離。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 將維持讀取及寫入鎖定 (取自於選取的資料) 至交易結束予以釋放為止。 當 SELECT 作業使用界定範圍的 WHERE 子句時，就會取得範圍鎖定以特意避免虛設項目讀取。<br /><br /> **注意：** 當您要求可序列化隔離等級時，複寫資料表上的 DDL 作業和交易可能會失敗。 這是因為複寫查詢所使用的提示可能與可序列化隔離等級不相容。|  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 也支援另外兩種使用資料列版本設定的交易隔離等級。 其一是讀取認可隔離的實作，而另一種交易隔離等級則是快照。  
  
|資料列版本設定隔離等級|定義|  
|------------------------------------|----------------|  
|**讀取認可快照集 (RCSI)**|當 READ_COMMITTED_SNAPSHOT 資料庫選項設為 ON 時，讀取認可隔離會使用資料列版本設定以提供陳述式層級的讀取一致性。 讀取作業只需要 SCH-S 資料表層級的鎖定，並不需要頁面或資料列的鎖定。 也就是說，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]會利用資料列版本設定，依照資料在陳述式開始時的存在狀態，為每個陳述式提供在交易上一致的資料快照集。 鎖定的使用目的不是為了防止其他交易更新資料。 使用者定義的函數可傳回在包含 UDF 的陳述式開始之後所認可的資料。<br /><br /> 當 `READ_COMMITTED_SNAPSHOT` 資料庫選項設定為 OFF (預設設定) 時，讀取認可隔離會在目前交易執行讀取作業的期間，利用共用鎖定來防止其他交易修改資料列。 共用鎖定也會封鎖陳述式，使它們在其他交易完成之前，無法讀取其他交易所修改的資料列。 這兩種實作都符合讀取認可隔離的 ISO 定義。|  
|**快照式**|快照隔離等級使用資料列版本設定來提供交易層級的讀取一致性。 讀取作業並不需要頁面或資料列的鎖定，只需要 SCH-S 資料表鎖定。 當讀取其他交易所修改的資料列時，它們會擷取在啟動交易時就已經存在的資料列版本。 只有當 `ALLOW_SNAPSHOT_ISOLATION` 資料庫選項設定為 ON 時，您才能針對資料庫使用快照集隔離。 根據預設，使用者資料庫的此選項為 OFF。<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不支援中繼資料版本設定。 因此，哪些 DDL 作業可以在快照隔離之下執行的明確交易中執行會有一些限制。 在 BEGIN TRANSACTION 陳述式之後，不允許在快照隔離下執行下列 DDL 陳述式：ALTER TABLE、CREATE INDEX、CREATE XML INDEX、ALTER INDEX、DROP INDEX、DBCC REINDEX、ALTER PARTITION FUNCTION、ALTER PARTITION SCHEME 或是任何通用語言執行平台 (CLR) DDL 陳述式。 在隱含交易內使用快照集隔離時，這些陳述式會受到允許。 就定義而言，隱含交易是一種單一陳述式，可強制使用快照隔離的語意 (即使是 DDL 陳述式)。 違反這個原則可能會造成錯誤 3961：`Snapshot isolation transaction failed in database '%.*ls' because the object accessed by the statement has been modified by a DDL statement in another concurrent transaction since the start of this transaction. It is not allowed because the metadata is not versioned. A concurrent update to metadata could lead to inconsistency if mixed with snapshot isolation.`|  
  
 下表顯示不同隔離等級所啟用的並行副作用。  
  
|隔離等級|中途讀取 (Dirty read)|非可重複讀取|虛設項目 (Phantom)|  
|---------------------|----------------|------------------------|-------------|  
|**讀取未認可**|是|是|是|  
|**讀取認可**|否|是|是|  
|**可重複讀取**|否|否|是|  
|**快照式**|否|否|否|  
|**可序列化**|否|否|否|  
  
 如需詳細了解每個交易隔離等級所控制之特定類型的鎖定或資料列版本設定，請參閱 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../t-sql/statements/set-transaction-isolation-level-transact-sql.md)。  
  
 交易隔離等級可使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 或透過資料庫 API 來設定。  
  
 **[!INCLUDE[tsql](../includes/tsql-md.md)]**                                      
 [!INCLUDE[tsql](../includes/tsql-md.md)] 指令碼使用 `SET TRANSACTION ISOLATION LEVEL` 陳述式。  
  
 **ADO**  
 ADO 應用程式會將 **Connection** 物件的 `IsolationLevel` 屬性設定為 adXactReadUncommitted、adXactReadCommitted、adXactRepeatableRead 或 adXactReadSerializable。  
  
 **ADO.NET**  
 使用 `System.Data.SqlClient` 受控命名空間的 ADO.NET 應用程式可以呼叫 `SqlConnection.BeginTransaction` 方法，並將 *IsolationLevel* 選項設定為 Unspecified、Chaos、ReadUncommitted、ReadCommitted、RepeatableRead、Serializable 及 Snapshot。  
  
 **OLE DB**  
 開始交易時，使用 OLE DB 的應用程式會將 *isoLevel* 會設定為 ISOLATIONLEVEL_READUNCOMMITTED、ISOLATIONLEVEL_READCOMMITTED、ISOLATIONLEVEL_REPEATABLEREAD、ISOLATIONLEVEL_SNAPSHOT 或 ISOLATIONLEVEL_SERIALIZABLE，來呼叫 `ITransactionLocal::StartTransaction`。  
  
 當以自動認可模式指定交易隔離層級時，OLE DB 應用程式可以將 DBPROPSET_SESSION 屬性的 DBPROP_SESS_AUTOCOMMITISOLEVELS 設定成 DBPROPVAL_TI_CHAOS、DBPROPVAL_TI_READUNCOMMITTED、DBPROPVAL_TI_BROWSE、DBPROPVAL_TI_CURSORSTABILITY、DBPROPVAL_TI_READCOMMITTED、DBPROPVAL_TI_REPEATABLEREAD、DBPROPVAL_TI_SERIALIZABLE、DBPROPVAL_TI_ISOLATED 或 DBPROPVAL_TI_SNAPSHOT。  
  
 **ODBC**  
 ODBC 應用程式會將 *Attribute* 設定為 SQL_ATTR_TXN_ISOLATION 並將 *ValuePtr* 設定為 SQL_TXN_READ_UNCOMMITTED、SQL_TXN_READ_COMMITTED、SQL_TXN_REPEATABLE_READ 或 SQL_TXN_SERIALIZABLE，來呼叫 `SQLSetConnectAttr`。  
  
 針對快照集交易，應用程式會將 Attribute 設定為 SQL_COPT_SS_TXN_ISOLATION 並將 ValuePtr 設定為 SQL_TXN_SS_SNAPSHOT，來呼叫 `SQLSetConnectAttr`。 快照集交易可以使用 SQL_COPT_SS_TXN_ISOLATION 或 SQL_ATTR_TXN_ISOLATION 來擷取。  
  
##  <a name="locking-in-the-database-engine"></a><a name="Lock_Engine"></a> 資料庫引擎中的鎖定  
 鎖定是 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的一種機制，用以同步處理多個使用者在同一時間對相同資料的存取。  
  
 在交易取得資料目前狀態的相依性前 (例如讀取或修改資料)，它必須保護自己使其免於受到另一個交易修改相同資料的影響。 交易可以要求資料的鎖定以達到此目的。 鎖定有不同的模式，例如共用或獨佔。 鎖定模式可定義交易在資料上的相依性層級。 若已授與該資料的鎖定模式給某個交易，就不會再授與鎖定給另一個交易，以免造成衝突。 如果交易所要求的鎖定模式，將和已授與相同資料的鎖定造成衝突， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 將停止要求交易，直到釋放第一個鎖定為止。  
  
 當交易修改資料時，它會持有防止修改的鎖定，直到交易結束為止。 交易持有保護讀取作業的鎖定時間長度，需視交易隔離等級設定而定。 交易完成 (認可或復原) 時，會釋放交易所持有的所有鎖定。  
  
 應用程式通常不會直接要求鎖定。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 中的鎖定管理員會在內部管理鎖定。 當 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 執行個體處理 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式時， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 查詢處理器可以決定要存取哪些資源。 查詢處理器根據存取類型以及交易隔離等級設定，決定需要哪些類型的鎖定以保護每個資源。 查詢處理器接著會對鎖定管理員要求適當的鎖定。 如果沒有其他交易持有衝突的鎖定，鎖定管理員就會授與鎖定。  
  
### <a name="lock-granularity-and-hierarchies"></a>鎖定資料粒度和階層  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 具有多資料粒度鎖定 (Multigranular Lock)，允許交易鎖定不同類型的資源。 為了把鎖定的成本降至最低， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 自動依照工作的適當層級來鎖定資源。 鎖定於較小的資料粒度 (Granularity) 如資料列可以提高並行，但如果鎖定許多的資料列則由於必須持有更多的鎖定而造成更高的額外負荷。 鎖定於較大的資料粒度如資料表，從並行的角度來看則由於鎖定整個資料表會限制其他交易對於資料表其他部份的存取因而更費時。 但由於必須維持的鎖定較少因此額外負荷較低。  
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 通常必須在資料粒度的多個層級取得鎖定，以完全保護資源。 在資料粒度的多個層級之鎖定群組稱為鎖定階層。 例如，若要充份地保護索引的讀取， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 可能需要取得資料列的共用鎖定以及頁面和資料表的意圖共用鎖定。  
  
 下表顯示 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 可以鎖定的資源。  
  
|資源|描述|  
|--------------|-----------------|  
|RID|資料列識別碼，用來鎖定堆積內單一資料列。|  
|KEY|索引中的資料列鎖定，用來保護可序列化交易中的索引鍵範圍。|  
|PAGE|資料庫中的 8 KB 頁面，例如資料或索引頁面。|  
|EXTENT|連續八個頁面的群組，例如資料頁或索引頁面。|  
|HoBT|堆積或 B 樹狀目錄。 針對資料表中沒有叢集索引的 B 型樹狀結構 (索引) 或堆積資料頁面進行保護鎖定。|  
|TABLE|一整個資料表，包含所有資料和索引。|  
|FILE|資料庫檔案|  
|APPLICATION|應用程式指定資源。|  
|METADATA|中繼資料鎖定。|  
|ALLOCATION_UNIT|配置單位。|  
|DATABASE|一整個資料庫。|  
  
> [!NOTE]  
> [ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md) 的 LOCK_ESCALATION 選項可影響 HoBT 和 TABLE 鎖定。  
  
### <a name="lock-modes"></a><a name="lock_modes"></a> 鎖定模式  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 使用可決定並行交易如何存取資源的各種鎖定模式來鎖定資源。  
  
 下表顯示 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 使用的資源鎖定模式。  
  
|鎖定模式|描述|  
|---------------|-----------------|  
|**共用 (S)**|用於不變更或更新資料的讀取作業，例如 SELECT 陳述式。|  
|**更新 (U)**|用於可更新的資源上。 防止當多個工作階段正在讀取、鎖定及後來可能更新資源時發生常見的死結。|  
|**獨占 (X)**|用於資料修改動作，例如 INSERT、UPDATE 或 DELETE。 確保不能對相同資源同時進行多重更新。|  
|**意圖**|用來建立鎖定階層。 意圖鎖定的類型為：意圖共用 (IS)、意圖獨佔 (IX) 與共用意圖獨佔 (SIX)。|  
|**結構描述**|執行相依於資料表結構描述的作業時使用。 結構描述鎖定的類型為：結構描述修改 (Sch-M) 與結構描述穩定性 (Sch-S)。|  
|**大量更新 (BU)**|用於大量複製資料到資料表，且已指定 **TABLOCK** 提示時。|  
|**索引鍵範圍**|當使用可序列化交易隔離等級時，保護查詢讀取的資料列範圍。 確定其他交易無法插入資料列，這些資料列在查詢重新執行時可限定可序列化交易的查詢。|  
  
#### <a name="shared-locks"></a><a name="shared"></a> 共用鎖定  
 共用 (S) 鎖定允許並行交易在封閉式 (Pessimistic) 並行控制之下讀取 (SELECT) 資源。 當資源存在共用 (S) 鎖定時，任何交易都無法修改資料。 除非交易隔離等級是設為可重複讀取或更高等級，或是使用鎖定提示來保持交易期間的共用 (S) 鎖定，否則讀取作業一完成就會釋放資源的共用 (S) 鎖定。  
  
#### <a name="update-locks"></a><a name="update"></a> 更新鎖定  
 更新 (U) 鎖定可防止常見的死結。 在可重複讀取或可序列化交易中，交易在讀取資料時取得資源 (頁面或資料列) 的共用 (S) 鎖定，然後修改資料，此過程需要將鎖定轉換為獨佔 (X) 鎖定。 如果兩筆交易取得某個資源的共用模式鎖定，然後嘗試同時更新資料，則其中一筆交易便會嘗試將鎖定轉換為獨佔 (X) 鎖定。 這種「從共用模式到獨佔」的鎖定轉換必須等待，因為某一筆交易的獨佔鎖定與另一筆交易的共用模式鎖定並不相容，所以會發生鎖定等候。 第二筆交易便嘗試取得更新時的獨佔 (X) 鎖定。 由於兩筆交易都轉換成獨佔 (X) 鎖定，且兩者皆等候另一筆交易釋放其共用模式的鎖定，因此便發生死結。  
  
 為了避免這種潛在的死結問題，則使用更新 (U) 鎖定。 一次只有一筆交易可以取得資源的更新 (U) 鎖定。 交易如果修改資源，更新 (U) 鎖定便轉換為獨佔 (X) 鎖定。  
  
#### <a name="exclusive-locks"></a><a name="exclusive"></a> 獨佔鎖定  
 獨佔 (X) 鎖定防止並行交易存取某個資源。 運用獨佔 (X) 鎖定，沒有其他交易可修改資料；只有使用 NOLOCK 提示或讀取未認可隔離等級，才能進行讀取作業。  
  
 資料修改陳述式 (例如 INSERT、UPDATE 和 DELETE) 結合了修改和讀取作業。 陳述式先執行讀取作業來取得資料，再執行必要的修改作業。 因此，資料修改陳述式通常會同時要求共用鎖定和獨佔鎖定。 例如，UPDATE 陳述式可能基於與一個資料表的聯結來修改另一個資料表的資料列。 在這個案例中，除了對已更新的資料列要求獨佔鎖定之外，UPDATE 陳述式還對聯結資料表中讀取的資料列要求共用鎖定。  
  
#### <a name="intent-locks"></a><a name="intent"></a> 意圖鎖定  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 使用意圖鎖定來保護，它把共用 (S) 鎖定或獨佔 (X) 鎖定放在鎖定階層中較低的資源上。 意圖鎖定會稱作意圖鎖定，是因為它們是在較低層級的鎖定之前取得的，因此表示將鎖定放在較低層級的意圖。  
  
 意圖鎖定有兩個用途：  
  
-   防止其他交易修改較高層級的資源，而導致較低層級的鎖定失效。 
-   為了改進 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 偵測資料粒度較高層級的鎖定衝突的效率。  
  
 例如，在資料表內的頁面或資料列要求共用 (S) 鎖定之前，先在資料表層級要求共用意圖鎖定。 在資料表層級上設定意圖鎖定讓另一筆交易無法後續取得包含該分頁之資料表的獨佔 (X) 鎖定。 意圖鎖定可以提昇效能，因為 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 只會在資料表層級上檢查意圖鎖定，來判斷交易是否可安全地取得該資料表的鎖定。 這種方式省略了必須檢查資料表的每個資料列或分頁的鎖定來判斷交易是否可以鎖定整個資料表的需求。  
  
<a name="lock_intent_table"></a> 意圖鎖定包括意圖共用 (IS)、意圖獨佔 (IX) 與以意圖獨佔共用 (SIX)。  
  
|鎖定模式|描述|  
|---------------|-----------------|  
|**意圖共用 (IS)**|保護在階層較低位置的某些 (但不是全部) 資源上要求的或取得的共用鎖定。|  
|**意圖獨佔 (IX)**|保護在階層較低位置的某些 (但不是全部) 資源上要求的或取得的獨佔鎖定。 IX 是 IS 的超集，它也保護在較低層級資源要求的共用鎖定。|  
|**與意圖獨佔共用 (SIX)**|保護對階層較低位置的所有資源要求的或取得的共用鎖定，以及對某些 (但非全部) 較低層級資源的意圖獨佔鎖定。 在最上層的資源中允許同時發生的 IS 鎖定。 例如，在資料表上取得 SIX 鎖定也會取得所修改頁面的意圖獨佔鎖定，以及所修改資料列的獨佔鎖定。 每個資源一次只能有一個 SIX 鎖定以防止其他的交易更新資源，雖然其他的交易可藉由取得資料表層級的 IS 鎖定來讀取階層架構中位於較低層級的資源。|  
|**意圖更新 (IU)**|保護對階層中較低的所有資源要求的或取得的更新鎖定。 IU 鎖定只使用於頁面資源。 如果發生更新作業，IU 鎖定會轉換成 IX 鎖定。|  
|**共用意圖更新 (SIU)**|S 和 IU 鎖定的結合，這是個別取得這些鎖定又同時保留兩種鎖定的結果。 例如，交易執行具有 PAGLOCK 提示的查詢，然後執行更新作業。 具有 PAGLOCK 提示的查詢取得 S 鎖定，而更新作業則取得 IU 鎖定。|  
|**更新意圖獨佔 (UIX)**|U 和 IX 鎖定的結合，這是個別取得這些鎖定又同時保留兩種鎖定的結果。|  
  
#### <a name="schema-locks"></a><a name="schema"></a> 結構描述鎖定  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 是在資料表的資料定義語言 (DDL) 作業 (例如加入資料行或卸除資料表) 期間使用結構描述修改 (Sch-M) 鎖定。 在保留期間，Sch-M 鎖定禁止資料表的並行存取。 這表示 Sch-M 鎖定會封鎖所有外在作業，直到釋放鎖定為止。  
  
 有些資料操作語言 (DML) 作業 (例如資料表截斷) 使用 Sch-M 鎖定來防止並行作業存取受影響的資料表。  
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 在編譯並執行查詢時，會使用結構描述穩定性 (Sch-S) 鎖定。 Sch-S 鎖定並未封鎖任何交易式鎖定，包括獨佔 (X) 鎖定。 因此，其他的交易在查詢編譯期間可以繼續執行，包括對資料表使用 X 鎖定的那些交易。 不過，取得 Sch-M 鎖定的並行 DDL 作業和並行 DML 作業無法在資料表上執行。  
  
#### <a name="bulk-update-locks"></a><a name="bulk_update"></a> 大量更新鎖定  
 大量更新 (BU) 鎖定允許多個執行緒將資料同時大量載入到相同資料表，同時禁止未大量載入資料的其他處理序存取該資料表。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會在下列兩種情況都成立時使用大量更新 (BU) 鎖定。  
  
-   您使用 [!INCLUDE[tsql](../includes/tsql-md.md)] BULK INSERT 陳述式或 OPENROWSET(BULK) 函數，或使用其中一個「大量插入 API」命令 (例如 .NET SqlBulkCopy)、「OLEDB 快速載入 API」或「ODBC 大量複製 API」，將資料大量複製到資料表中。  
-   當已指定 **TABLOCK** 提示，或者使用 **sp_tableoption** 設定了 **table lock on bulk load**資料表選項。  
  
> [!TIP]  
> 與 BULK INSERT 陳述式 (持有較不嚴格的大量更新鎖定) 不同之處在於，具 TABLOCK 提示的 INSERT INTO...SELECT 對資料表持有獨佔 (X) 鎖定。 這代表您無法使用平行插入作業插入資料列。  
  
#### <a name="key-range-locks"></a><a name="key_range"></a> 索引鍵範圍鎖定  
 使用可序列化的交易隔離等級時，索引鍵範圍鎖定可保護由 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式讀取之記錄集內隱含包括的資料列範圍。 索引鍵範圍鎖定可預防虛設項目讀取。 透過保護資料列之間的索引鍵範圍，也可防止某交易存取的記錄集內的虛設項目插入或刪除。  
  
### <a name="lock-compatibility"></a><a name="lock_compatibility"></a> 鎖定相容性  
 鎖定相容性可控制多筆交易是否可同時對相同的資源取得鎖定。 若資源已被其他交易鎖定，則只有在要求的鎖定模式與現有鎖定模式相容時，才能授與新的鎖定要求。 若所要求鎖定的模式與現有鎖定不相容，則要求新鎖定的交易會等候現有鎖定被釋放，或等候鎖定逾時間隔過期。 例如，沒有任何一種鎖定模式與獨佔鎖定相容。 有獨佔 (X) 鎖定存在時，其他的交易都無法取得該資源的任何一種鎖定 (共用、更新或獨佔)，直到獨佔 (X) 鎖定被釋放為止。 此外，如果資源已套用共用 (S) 鎖定，則即使第一筆交易尚未完成，其他的交易仍可取得該項目的共用鎖定或更新 (U) 鎖定。 然而在共用鎖定尚未釋放之前，其他的交易仍然無法取得獨占鎖定。  
  
<a name="lock_compat_table"></a> 下表顯示常見鎖定模式的相容性。  
  
||現有已授與的模式||||||  
|------|---------------------------|------|------|------|------|------|  
|**要求的模式**|**IS**|**S**|**U**|**IX**|**SIX**|**X**|  
|**意圖共用 (IS)**|是|是|是|是|是|否|  
|**共用 (S)**|是|是|是|否|否|否|  
|**更新 (U)**|是|是|否|否|否|否|  
|**意圖獨佔 (IX)**|是|否|否|是|否|否|  
|**與意圖獨佔共用 (SIX)**|是|否|否|否|否|否|  
|**獨占 (X)**|否|否|否|否|否|否|  
  
> [!NOTE]  
> 意圖獨佔 (IX) 鎖定與 IX 鎖定模式相容，因為 IX 表示意圖是僅更新某些資料列而非更新全部。 嘗試讀取或更新某些資料列的其他交易也可獲得許可，只要這些資料列與其他交易所更新的資料列不相同即可。 此外，如果兩筆交易嘗試更新相同的資料列，這兩筆交易都會被授與資料表和頁面層級的 IX 鎖定。 不過，其中一筆交易會被授與資料列層級的 X 鎖定。 另一筆交易則必須等到系統移除資料列層級鎖定為止。  
  
<a name="lock_matrix"></a> 使用下表來判斷 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中所有可用鎖定模式的相容性。  
  
 ![lock_conflicts](../relational-databases/media/LockConflictTable.png)  
  
### <a name="key-range-locking"></a>索引鍵範圍鎖定  
 使用可序列化的交易隔離等級時，索引鍵範圍鎖定可保護由 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式讀取之記錄集內隱含包括的資料列範圍。 可序列化的隔離等級要求在交易期間執行的任何查詢，在交易期間每次執行時都必須取得相同的資料列集。 索引鍵範圍鎖定藉由預防其他交易插入新資料列時，這些資料列的索引鍵落在可序列化交易讀取的索引鍵範圍，來保護此種需求。  
  
 索引鍵範圍鎖定可預防虛設項目讀取。 藉由保護資料列之間的索引鍵範圍，也可以預防虛設項目插入到交易存取的記錄集。  
  
 索引鍵範圍鎖定是放置於索引之上，指定開始和結束的索引鍵值。 因為這些動作會先在索引上取得鎖定，因此這種鎖定可封鎖任何嘗試插入、更新或刪除含有索引鍵值落入範圍的任何資料列。 例如，可序列化的交易可能會發出 `SELECT` 陳述式，其會讀取索引鍵值符合 `BETWEEN 'AAA' AND 'CZZ'` 條件的所有資料列。 從 **'** AAA **'** 到 **'** CZZ **'** 範圍中索引鍵值的索引鍵範圍鎖定，可預防其他交易將含有索引鍵值的資料列插入到該範圍內的任何地方，例如 **'** ADG **'** 、 **'** BBD **'** 或 **'** CAL **'** 。  
  
#### <a name="key-range-lock-modes"></a><a name="key_range_modes"></a> 索引鍵範圍鎖定模式  
 索引鍵範圍鎖定包括範圍以及資料列元件，以範圍-資料列的格式來指定：  
  
-   範圍代表保護兩個連續索引項之間的範圍的鎖定模式。  
-   資料列代表保護索引項的鎖定模式。  
-   模式代表所使用的合併鎖定模式。 索引鍵範圍鎖定模式由兩個部份組成。 第一個部份代表用來鎖定索引鍵範圍的鎖定類型 (Range*T*)，第二個部份代表用來鎖定特定索引鍵的鎖定類型 (*K*)。 這兩個部份使用連字號 (-) 來連接，例如 Range*T*-*K*。  
  
    |範圍|資料列|[模式]|描述|  
    |-----------|---------|----------|-----------------|  
    |RangeS|S|RangeS-S|共用範圍，共用資源鎖定；可序列化範圍掃描。|  
    |RangeS|U|RangeS-U|共用範圍，更新資源鎖定；可序列化更新掃描。|  
    |RangeI|Null|RangeI-N|插入範圍，Null 資源鎖定；在插入新的索引鍵到索引之前用來測試範圍。|  
    |RangeX|X|RangeX-X|獨占範圍，獨占資源鎖定；在範圍內更新索引鍵時使用。|  
  
> [!NOTE]  
> 內部的 Null 鎖定模式與其他所有的鎖定模式皆相容。  
  
 索引鍵範圍鎖定模式的相容性矩陣顯示，哪些鎖定與重疊索引鍵和範圍中取得的其他鎖定相容。  
  
||現有已授與的模式|||||||  
|------|---------------------------|------|------|------|------|------|------|  
|**要求的模式**|**S**|**U**|**X**|**RangeS-S**|**RangeS-U**|**RangeI-N**|**RangeX-X**|  
|**共用 (S)**|是|是|否|是|是|是|否|  
|**更新 (U)**|是|否|否|是|否|是|否|  
|**獨占 (X)**|否|否|否|否|否|是|否|  
|**RangeS-S**|是|是|否|是|是|否|否|  
|**RangeS-U**|是|否|否|是|否|否|否|  
|**RangeI-N**|是|是|是|否|否|是|否|  
|**RangeX-X**|否|否|否|否|否|否|否|  
  
#### <a name="conversion-locks"></a><a name="lock_conversion"></a> 轉換鎖定  
 轉換鎖定是在索引鍵範圍鎖定與另一種鎖定重疊時建立。  
  
|鎖定 1|鎖定 2|轉換鎖定|  
|------------|------------|---------------------|  
|S|RangeI-N|RangeI-S|  
|U|RangeI-N|RangeI-U|  
|X|RangeI-N|RangeI-X|  
|RangeI-N|RangeS-S|RangeX-S|  
|RangeI-N|RangeS-U|RangeX-U|  
  
 在不同的複雜環境下，可以觀察到短期的轉換鎖定，有時是在並行的處理序執行時。  
  
#### <a name="serializable-range-scan-singleton-fetch-delete-and-insert"></a>可序列化範圍掃描、單一擷取、刪除以及插入  
 索引鍵範圍鎖定可確保下列動作是可序列化：  
  
-   範圍掃描查詢  
-   單一擷取不存在的資料列  
-   刪除動作  
-   插入動作  
  
 在索引鍵範圍鎖定發生之前，必須滿足下列條件：  
  
-   交易隔離等級必須設為 SERIALIZABLE。  
-   查詢處理器必須使用索引來實作範圍篩選述詞。 例如，SELECT 陳述式中的 WHERE 子句可利用此述詞建立一個範圍條件：ColumnX BETWEEN N **'** AAA **'** AND N **'** CZZ **'** 。 如果 **ColumnX** 涵蓋在索引鍵中，才會取得索引鍵範圍鎖定。  
  
#### <a name="examples"></a>範例  
 下列資料表和索引是用來作為索引鍵範圍鎖定範例要遵循的基礎。  
  
 ![btree](../relational-databases/media/btree4.png)  
  
##### <a name="range-scan-query"></a>範圍掃描查詢  
 為了確保範圍掃描查詢是可序列化，相同的查詢每次在相同交易內執行時都必須傳回相同的結果。 其他的交易絕不能把新的資料列插入範圍掃描查詢內；否則這些動作將會變成虛設項目插入。 例如，以下的查詢使用上述的資料表與索引：  
  
```sql  
SELECT name  
FROM mytable  
WHERE name BETWEEN 'A' AND 'C';  
```  
  
 放置索引鍵範圍鎖定的索引項對應到名稱介於資料值 Adam 與 Dale 之間的資料列範圍，讓前次查詢中限定的新資料列無法新增或刪除。 雖然此範圍內的第一個名稱是 Adam，但位於此索引項的 RangeS-S 模式的索引鍵範圍鎖定會確保以字母 A 開頭的新名稱無法新增至 Adam 前面，例如 Abigail。 同樣的，位於 Dale 的索引項的 RangeS-S 索引鍵範圍鎖定，則確保以字母 C 開頭的新名稱皆無法新增至 Carlos 後面，例如 Clive。  
  
> [!NOTE]  
> 持有的 RangeS-S 鎖定的數量為 *n*+1，其中 *n* 為符合查詢的資料列數量。  
  
##### <a name="singleton-fetch-of-nonexistent-data"></a>單一擷取不存在的資料  
 如果交易內的查詢嘗試選取不存在的資料列，則在同一筆交易內稍後的某一點所提交的查詢必須傳回相同的結果。 其他的任何交易皆不得插入這個不存在的資料列。 例如，給定以下的查詢：  
  
```sql  
SELECT name  
FROM mytable  
WHERE name = 'Bill';  
```  
  
 將索引鍵範圍鎖定放在與名稱範圍從 `Ben` 到 `Bing` 對應的索引項，因為要把名稱 `Bill` 插入這兩個相鄰的索引項之間。 將 RangeS-S 模式的索引鍵範圍鎖定放在索引項 `Bing`之上。 這可預防其他交易將值 (例如 `Bill`) 插入到索引項 `Ben` 和 `Bing`之間。  
  
##### <a name="delete-operation"></a>刪除作業  
 在交易內刪除某個值時，交易進行刪除動作期間不需鎖定該值所處之範圍。 鎖定欲刪除的索引鍵值直到交易結束，即足以維持可序列化能力。 例如，給定以下的 DELETE 陳述式：  
  
```sql  
DELETE mytable  
WHERE name = 'Bob';  
```  
  
 將獨占 (X) 鎖定放在與名稱 `Bob`對應的索引項。 其他交易可在被刪除的值 `Bob`前後插入或刪除值。 但是，嘗試讀取、插入或是刪除 `Bob` 這個值的任何交易，在進行刪除動作的交易尚未認可或回復之前都會被封鎖。  
  
 可以使用三種基本鎖定模式來執行範圍刪除：資料列、分頁或資料表鎖定。 資料列、分頁或資料表的鎖定策略是由查詢最佳化工具來決定，或者亦可由使用者透過最佳化提示 (如 ROWLOCK、PAGLOCK 或 TABLOCK) 來指定。 使用 PAGLOCK 或 TABLOCK 時，如果所有資料列都會從此分頁刪除， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會立即重新配置索引頁。 相反的，若是使用 ROWLOCK，所有已刪除的資料列則僅標示為已刪除；稍後再使用背景工作將這些資料列從索引頁中移除。  
  
##### <a name="insert-operation"></a>插入動作  
 在交易內插入某個值時，交易進行插入動作期間不需鎖定該值所處之範圍。 鎖定欲插入的索引鍵值直到交易結束，即足以維持可序列化能力。 例如，給定以下的 INSERT 陳述式：  
  
```sql  
INSERT mytable VALUES ('Dan');  
```  
  
 將 RangeI-N 模式的索引鍵範圍鎖定放在與名稱 David 對應的索引項來測試範圍。 如果授與鎖定，便插入 `Dan` 並將獨占 (X) 鎖定放在 `Dan`這個值。 RangeI-N 模式的索引鍵範圍鎖定只有在測試範圍時才需要，且在交易進行插入動作期間不需持有。 其他的交易皆可在插入值 `Dan`的前面或後面插入或刪除值。 但是，嘗試讀取、插入或是刪除 `Dan` 這個值的任何交易在進行插入動作的交易尚未認可或回復之前都會被鎖定。  
  
### <a name="dynamic-locking"></a><a name="dynamic_locks"></a> 動態鎖定  
 使用像資料列鎖定等低層級鎖定，可藉由降低兩個交易同時要求相同片段的資料鎖定之可能性來增加並行。 使用低層級鎖定也會增加鎖定的數目以及需要管理鎖定的資源。 使用高層級的資料表或頁面鎖定可降低額外負荷，但必須花費降低並行的成本。  
  
 ![lockcht](../relational-databases/media/lockcht.png) 
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]使用動態鎖定策略來判斷最具成本效益的鎖定。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 在執行查詢時會依照結構描述與查詢的特性，自動決定最合適的鎖定類型。 例如，為了降低鎖定的額外負荷，最佳化工具在進行索引掃描時可能會選擇頁面層級的鎖定。  
  
 動態鎖定具有下列優點：  
  
-   簡化資料庫的管理。 資料庫管理員並不需要調整鎖定擴大的臨界值。  
-   提升效能。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 藉由使用適合於工作的鎖定，將系統的負擔降至最低。  
-   應用程式開發人員可以專注於開發。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會自動調整鎖定。  
  
 從 [!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)] 開始，鎖定擴大行為已隨著 `LOCK_ESCALATION` 選項的導入而變更。 如需詳細資訊，請參閱 [ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md)的 `LOCK_ESCALATION` 選項。  
  
## <a name="deadlocks"></a><a name="deadlocks"></a> 死結  
 當二或多個工作各自具有某個資源的鎖定，但其他工作嘗試要鎖定此資源，而造成工作永久封鎖彼此時，會發生死結。 例如：  
  
-   交易 A 取得資料列 1 的共用鎖定。  
-   交易 B 取得資料列 2 的共用鎖定。  
-   交易 A 現在要求資料列 2 的獨佔鎖定，但會被封鎖直到交易 B 完成並釋出對資料列 2 的共用鎖定為止。  
-   交易 B 現在要求資料列 1 的獨佔鎖定，但會被封鎖直到交易 A 完成並釋出對資料列 1 的共用鎖定為止。  
  
 等到交易 B 完成後，交易 A 才能完成，但交易 B 卻被交易 A 封鎖了。這個狀況也稱為「循環相依性」：交易 A 相依於交易 B，且交易 B 因為相依於交易 A 而形成封閉式循環。  
  
 在死結中的這兩個交易會一直等下去，除非由外部處理序解除此死結。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 死結監視器會定期檢查是否有工作處於死結狀態。 如果監視器偵測到循環相依性，它會選擇其中一個工作作為犧牲者，以錯誤來結束其交易。 這樣另一個工作便可以完成其交易。 因為錯誤而結束交易的應用程式可以重試交易，通常在另一個死結交易完成之後便會完成。  
  
 死結通常會和一般的封鎖產生混淆。 當交易要求鎖定的資源被另一個交易鎖定時，提出要求的交易會等待鎖定釋出。 依預設，除非設定了 LOCK_TIMEOUT，否則 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 交易不會逾時。 提出要求的交易會被封鎖，但非死結，因為提出要求的交易尚未封鎖目前擁有鎖定的交易。 最後，主控交易會完成並釋出鎖定，然後提出要求的交易會被授與鎖定並繼續進行。  
  
> [!NOTE]
> 死結 (Deadlock) 有時也稱為致命環節 (Deadly Embrace)。  
  
 死結可能發生在任何具有多執行緒的系統上，而不只是在關聯式資料庫管理系統，並且可能發生在資料庫物件鎖定之外的資源。 例如，在多執行緒作業系統中的一個執行緒可能取得一或多個資源，像是記憶體區塊。 若要取得的資源目前為另一個執行緒所擁有，前者的執行緒可能就必須等候擁有資源的執行緒釋放目標資源。 等候的執行緒便是所謂的與擁有該特定資源的執行緒具有依存性。 在 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]的執行個體中，當工作階段取得非資料庫資源 (例如記憶體或執行緒) 時，可能會發生死結。  
  
 ![顯示交易死結的圖表](../relational-databases/media/deadlock.png)  
  
 在上圖中，在 **Part** 資料表鎖定資源上，交易 T1 相依於交易 T2。 同樣的，在 **Supplier** 資料表鎖定資源上，交易 T2 相依於交易 T1。 由於這些相依性形成循環，交易 T1 與 T2 之間便構成死結。  
  
 當資料表已分割，且 `ALTER TABLE` 的 `LOCK_ESCALATION` 設定為 AUTO 時，也可能發生死結。 當 `LOCK_ESCALATION` 設定為 AUTO 時，會藉由讓[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]鎖定 HoBT 層級 (而不是資料表層級) 的資料表資料分割來增加並行。 但是，當個別交易在資料表中保留資料分割鎖定，而且想要鎖定其他交易資料分割上的某個地方時，這就會造成死結。 您可以將 `LOCK_ESCALATION` 設定為 `TABLE` 來避免這類死結；雖然此設定減少並行的方式，是強制資料分割的大量更新等候資料表鎖定。  
  
### <a name="detecting-and-ending-deadlocks"></a>偵測與結束死結  
 當二或多個工作各自具有某個資源的鎖定，但其他工作嘗試要鎖定此資源，而造成工作永久封鎖彼此時，會發生死結。 下圖顯示死結狀態的高階檢視，其中：  
  
-   工作 T1 有資源 R1 的鎖定 (由 R1 到 T1 的箭頭所表示)，並且已要求資源 R2 的鎖定 (由 T1 到 R2 的箭頭所表示)。  
-   工作 T2 有資源 R2 的鎖定 (由 R2 到 T2 的箭頭所表示)，並且已要求資源 R1 的鎖定 (由 T2 到 R1 的箭頭所表示)。  
-   因為在有資源可用之前，沒有一項工作可以繼續，而在有工作繼續之前，沒有一項資源可以釋放，所以會有死結狀態。  
  
 ![顯示處於死結狀態的工作其圖表](../relational-databases/media/Task_Deadlock_State.png)  
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 自動偵測 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中的死結循環。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會選擇其中一個工作階段作為死結犧牲者，讓目前交易終止並產生錯誤，以破除死結。  
  
#### <a name="resources-that-can-deadlock"></a><a name="deadlock_resources"></a> 可能發生死結的資源  
 每個使用者工作階段可能有一或多個工作代表工作階段執行，其中每個工作可能會取得或等待取得各種資源。 下列類型的資源會導致封鎖，而造成死結。  
  
-   **鎖定**。 等待取得像是物件、分頁、資料列、中繼資料和應用程式等資源的鎖定，可能會導致死結。 例如，交易 T1 有資料列 r1 的共用 (S) 鎖定，並且正在等待取得 r2 的獨佔 (X) 鎖定。 交易 T2 有 r2 的共用 (S) 鎖定，並且正在等待取得資料列 r1 的獨佔 (X) 鎖定。 這樣會產生鎖定循環，因為 T1 和 T2 都在等待對方釋放已鎖定的資源。  
  
-   **工作者執行緒**。 等待可用工作者執行緒的佇列工作，可能會導致死結。 如果佇列工作擁有正在封鎖所有工作者執行緒的資源，便會產生死結。 例如，工作階段 S1 啟動交易，並且取得資料列 r1 的共用 (S) 鎖定，然後進入睡眠。 在所有可用工作者執行緒上執行的使用中工作階段，正在嘗試取得資料列 r1 的獨佔 (X) 鎖定。 因為工作階段 S1 無法取得工作者執行緒，所以它無法認可交易並釋放資料列 r1 的鎖定。 這樣會產生死結。  
  
-   **記憶體**。 當並行要求正在等待記憶體授權，但可用記憶體不足而無法滿足授權時，便會發生死結。 例如，兩個並行查詢 Q1 和 Q2 以使用者自訂函數執行，分別取得 10MB 和 20MB 記憶體。 如果每個查詢需要 30MB 而可用的總記憶體是 20MB，則 Q1 和 Q2 必須等待對方釋放記憶體。這樣會產生死結。  
  
-   **與平行查詢執行相關的資源**。 與交換通訊埠建立關聯的協調器、產生器或取用者執行緒，通常在包含至少一個不屬於平行查詢的其他處理序時，可能會彼此封鎖，而導致死結。 而且，當平行查詢開始執行時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會根據目前工作負載來判斷平行程度或工作者執行緒數目。 如果系統工作負載意外變更，例如有新查詢開始在伺服器上執行或系統的工作者執行緒用盡，此時會發生死結。  
  
-   **Multiple Active Result Set (MARS) 資源**。 這些資源在 MARS 下是用來控制多個使用中要求的交錯情形。 如需詳細資訊，請參閱[使用 Multiple Active Result Sets (MARS)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)。  
  
    -   **使用者資源**。 當執行緒正在等待的資源可能受使用者應用程式控制時，此資源會視為外部或使用者資源，並且如同鎖定處理。  
  
    -   **工作階段 Mutex**。 工作階段中執行的工作為交錯的，這表示同時只能有一個工作在此工作階段執行。 工作必須具有對工作階段 Mutex 的獨佔存取權才能執行。  
  
    -   **交易 Mutex**。 交易中執行的所有工作為交錯的，這表示同時只能有一個工作在此交易執行。 工作必須具有對交易 Mutex 的獨佔存取權才能執行。  
  
     工作必須取得工作階段 Mutex，才能在 MARS 下執行。 如果工作在交易下執行，則它必須接著取得交易 Mutex。 這可保證在給定工作階段和給定交易中，同時只有一個工作使用中。 一旦取得所需的 Mutex，工作即可執行。 當工作完成或在要求中途退出時，會以取得 Mutex 的相反順序，先釋放交易 Mutex，接著再釋放工作階段 Mutex。 不過，這些資源可能會發生死結。 在下列程式碼範例中，同一個工作階段中執行了兩個工作 (使用者要求 U1 和使用者要求 U2)。  
  
    ```  
    U1:    Rs1=Command1.Execute("insert sometable EXEC usp_someproc");  
    U2:    Rs2=Command2.Execute("select colA from sometable");  
    ```  
  
     從使用者要求 U1 執行的預存程序已取得工作階段 Mutex。 如果預存程序花很長的時間執行，則 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會假設此預存程序正在等待使用者輸入。 當使用者正在等待 U2 的結果集時，使用者要求 U2 正在等待工作階段 Mutex，而 U1 正在等待使用者資源。 這就是死結狀態，邏輯上可用下圖說明：  
  
 ![LogicFlowExamplec](../relational-databases/media/udb9_LogicFlowExamplec.png)  
  
### <a name="deadlock-detection"></a><a name="deadlock_detection"></a> 死結偵測  
 上節列出的所有資源都參與 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 死結偵測配置。 死結偵測由鎖定監視器執行緒所執行，它會定期在 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]執行個體的所有工作中啟動搜尋。 下列幾點描述搜尋程序：  
  
-   預設間隔是 5 秒。  
-   如果鎖定監視器執行緒發現死結，死結偵測間隔會從 5 秒降低，最低降至 100 毫秒，視死結頻率而定。  
-   如果鎖定監視器執行緒停止尋找死結， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會增加搜尋間隔為 5 秒。  
-   如果剛偵測到死結，則會假設後續還有必須等待鎖定的執行緒進入死結循環。 在偵測到死結之後，前面幾個鎖定等待會立即觸發死結搜尋，而不需等到下個死結偵測間隔。 例如，如果目前間隔是 5 秒，並且剛偵測到死結，則下個鎖定等待會立即啟動死結偵測設定。 如果這個鎖定等待是死結的一部分，則會立即偵測到它，而不需等到下個死結搜尋期間。  
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 通常僅執行定期的死結偵測。 由於系統會遇到的死結數量通常很少，週期的死結偵測即可協助將系統在死結偵測上的額外負荷降低。  
  
 當鎖定監視執行緒為特定的執行緒啟動死結搜尋時，便對執行緒正在等候的資源進行識別。 而後再由鎖定監視找出該特定資源的擁有者執行緒，並繼續為這些執行緒進行遞迴的死結搜尋直到找出循環為止。 以此方式識別到的循環即構成死結。  
  
 在偵測到死結之後， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會選擇其中一個執行緒作為死結犧牲者，結束死結。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會結束目前為此執行緒所執行的批次、回復死結犧牲者的交易，並且傳回 1205 錯誤至應用程式。 回復死結犧牲者的交易，將會釋放交易所持有的所有鎖定。 這可讓其他執行緒的交易變成解除封鎖的狀態並繼續進行。 1205 死結犧牲者錯誤會將與死結相關的執行緒和資源資訊記錄在錯誤記錄檔中。  
  
 依預設， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會選擇執行回復成本最低之交易的工作階段作為死結犧牲者。 或者，使用者也可以使用 SET DEADLOCK_PRIORITY 陳述式，指定死結情況下工作階段的優先權。 DEADLOCK_PRIORITY 可以設為 LOW、NORMAL 或 HIGH，或設為 -10 到 10 範圍內的任何整數值。 死結優先權預設為 NORMAL。 如果兩個工作階段有不同的死結優先權，優先權較低的工作階段會被選為死結犧牲者。 如果兩個工作階段有相同的死結優先權，則會選擇回復成本最低之交易的工作階段。 如果死結循環中相關的工作階段具有相同的死結優先權和相同成本，則會隨機選擇犧牲者。  
  
 使用 CLR 時，死結監視器會為 Managed 程序內所存取的同步處理資源 (監視器、讀取器/寫入器鎖定和執行緒聯結) 自動偵測是否有死結。 不過，死結是透過在選為死結犧牲者的程序中擲回例外狀況來解決。 例外狀況並不會自動釋放犧牲者目前所擁有的資源；您必須明確釋放資源，了解這點很重要。 與例外狀況行為一致，用來識別死結犧牲者的例外狀況可以在發生後解除。  
  
### <a name="deadlock-information-tools"></a><a name="deadlock_tools"></a> 死結資訊工具  
 為了檢視死結資訊，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]以 system\_health xEvent 工作階段、兩個追蹤旗標及 SQL Profiler 中 Deadlock Graph 事件的形式，提供監視工具。  

#### <a name="deadlock-extended-event"></a><a name="deadlock_xevent"></a> 死結擴充事件
從 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 開始，應使用 `xml_deadlock_report` 擴充事件 (xEvent)，以取代 SQL 追蹤或 SQL Profiler 中的死結圖表事件類別。

從 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 開始，發生死結時，system\_health 工作階段會擷取所有 `xml_deadlock_report` xEvent (其包含死結圖表)。 因為依預設會啟用 system\_health 工作階段，所以不需要設定個別的 xEvent 工作階段來擷取死結資訊。 

所擷取的 Deadlock Graph 通常有三個不同的節點：
-   **victim-list**。 死結犧牲者處理序識別碼。
-   **process-list**。 涉及死結之所有處理序的相關資訊。
-   **resource-list**。 涉及死結之資源的相關資訊。

開啟 system\_health 工作階段檔案或信號緩衝區，如果已記錄 `xml_deadlock_report` xEvent，[!INCLUDE[ssManStudio](../includes/ssManStudio-md.md)] 就會顯示涉及死結之工作和資源的圖形化描述，如以下範例所示： 

![xEvent 死結圖表](../relational-databases/media/udb9_xEventDeadlockGraphc.png)

下列查詢可以檢視 system\_health 工作階段信號緩衝區所擷取的所有死結事件：

```sql
SELECT xdr.value('@timestamp', 'datetime') AS [Date],
    xdr.query('.') AS [Event_Data]
FROM (SELECT CAST([target_data] AS XML) AS Target_Data
            FROM sys.dm_xe_session_targets AS xt
            INNER JOIN sys.dm_xe_sessions AS xs ON xs.address = xt.event_session_address
            WHERE xs.name = N'system_health'
              AND xt.target_name = N'ring_buffer'
    ) AS XML_Data
CROSS APPLY Target_Data.nodes('RingBufferTarget/event[@name="xml_deadlock_report"]') AS XEventData(xdr)
ORDER BY [Date] DESC
```

[!INCLUDE[ssResult](../includes/ssresult-md.md)]

![system_health_qry](../relational-databases/media/system_health_qry.png)

下列範例顯示按一下上方結果之第一個連結後的輸出：

```xml
<event name="xml_deadlock_report" package="sqlserver" timestamp="2018-02-18T08:26:24.698Z">
  <data name="xml_report">
    <type name="xml" package="package0" />
    <value>
      <deadlock>
        <victim-list>
          <victimProcess id="process27b9b0b9848" />
        </victim-list>
        <process-list>
          <process id="process27b9b0b9848" taskpriority="0" logused="0" waitresource="KEY: 5:72057594214350848 (1a39e6095155)" waittime="1631" ownerId="11088595" transactionname="SELECT" lasttranstarted="2018-02-18T00:26:23.073" XDES="0x27b9f79fac0" lockMode="S" schedulerid="9" kpid="15336" status="suspended" spid="62" sbid="0" ecid="0" priority="0" trancount="0" lastbatchstarted="2018-02-18T00:26:22.893" lastbatchcompleted="2018-02-18T00:26:22.890" lastattention="1900-01-01T00:00:00.890" clientapp="SQLCMD" hostname="ContosoServer" hostpid="7908" loginname="CONTOSO\user" isolationlevel="read committed (2)" xactid="11088595" currentdb="5" lockTimeout="4294967295" clientoption1="538968096" clientoption2="128056">
            <executionStack>
              <frame procname="AdventureWorks2016CTP3.dbo.p1" line="3" stmtstart="78" stmtend="180" sqlhandle="0x0300050020766505ca3e07008ba8000001000000000000000000000000000000000000000000000000000000">
SELECT c2, c3 FROM t1 WHERE c2 BETWEEN @p1 AND @p1+    </frame>
              <frame procname="adhoc" line="4" stmtstart="82" stmtend="98" sqlhandle="0x020000006263ec01ebb919c335024a072a2699958d3fcce60000000000000000000000000000000000000000">
unknown    </frame>
            </executionStack>
            <inputbuf>
SET NOCOUNT ON
WHILE (1=1) 
BEGIN
    EXEC p1 4
END
   </inputbuf>
          </process>
          <process id="process27b9ee33c28" taskpriority="0" logused="252" waitresource="KEY: 5:72057594214416384 (e5b3d7e750dd)" waittime="1631" ownerId="11088593" transactionname="UPDATE" lasttranstarted="2018-02-18T00:26:23.073" XDES="0x27ba15a4490" lockMode="X" schedulerid="6" kpid="5584" status="suspended" spid="58" sbid="0" ecid="0" priority="0" trancount="2" lastbatchstarted="2018-02-18T00:26:22.890" lastbatchcompleted="2018-02-18T00:26:22.890" lastattention="1900-01-01T00:00:00.890" clientapp="SQLCMD" hostname="ContosoServer" hostpid="15316" loginname="CONTOSO\user" isolationlevel="read committed (2)" xactid="11088593" currentdb="5" lockTimeout="4294967295" clientoption1="538968096" clientoption2="128056">
            <executionStack>
              <frame procname="AdventureWorks2016CTP3.dbo.p2" line="3" stmtstart="76" stmtend="150" sqlhandle="0x03000500599a5906ce3e07008ba8000001000000000000000000000000000000000000000000000000000000">
UPDATE t1 SET c2 = c2+1 WHERE c1 = @p    </frame>
              <frame procname="adhoc" line="4" stmtstart="82" stmtend="98" sqlhandle="0x02000000008fe521e5fb1099410048c5743ff7da04b2047b0000000000000000000000000000000000000000">
unknown    </frame>
            </executionStack>
            <inputbuf>
SET NOCOUNT ON
WHILE (1=1) 
BEGIN
    EXEC p2 4
END
   </inputbuf>
          </process>
        </process-list>
        <resource-list>
          <keylock hobtid="72057594214350848" dbid="5" objectname="AdventureWorks2016CTP3.dbo.t1" indexname="cidx" id="lock27b9dd26a00" mode="X" associatedObjectId="72057594214350848">
            <owner-list>
              <owner id="process27b9ee33c28" mode="X" />
            </owner-list>
            <waiter-list>
              <waiter id="process27b9b0b9848" mode="S" requestType="wait" />
            </waiter-list>
          </keylock>
          <keylock hobtid="72057594214416384" dbid="5" objectname="AdventureWorks2016CTP3.dbo.t1" indexname="idx1" id="lock27afa392600" mode="S" associatedObjectId="72057594214416384">
            <owner-list>
              <owner id="process27b9b0b9848" mode="S" />
            </owner-list>
            <waiter-list>
              <waiter id="process27b9ee33c28" mode="X" requestType="wait" />
            </waiter-list>
          </keylock>
        </resource-list>
      </deadlock>
    </value>
  </data>
</event>
```

如需詳細資訊，請參閱[使用 system_health 工作階段](../relational-databases/extended-events/use-the-system-health-session.md)

#### <a name="trace-flag-1204-and-trace-flag-1222"></a><a name="deadlock_traceflags"></a> 追蹤旗標 1204 和追蹤旗標 1222  
 發生死結時，追蹤旗標 1204 和追蹤旗標 1222 會傳回在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 錯誤記錄檔中擷取到的資訊。 追蹤旗標 1204 報告死結所涉及的每一個節點格式化的死結資訊。 追蹤旗標 1222 先按處理序再按資源來格式化死結資訊。 可同時啟用兩種追蹤旗標來取得相同死結事件的兩種表示法。  

> [!IMPORTANT]
> 請避免在會導致死結的大工作負載系統上使用追蹤旗標 1204 與 1222。 使用這些追蹤旗標可能會導致效能問題。 請改為使用死結擴充事件 (#deadlock_xevent)。
  
 除了定義追蹤旗標 1204 和 1222 的屬性之外，下表還顯示其相似性和差異。  
  
|屬性|追蹤旗標 1204 和追蹤旗標 1222|僅追蹤旗標 1204|僅追蹤旗標 1222|  
|--------------|-----------------------------------------|--------------------------|--------------------------|  
|輸出格式|輸出是擷取到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 錯誤記錄檔中。|聚焦於死結所涉及的節點。 每一個節點有一個專用區段，最後區段描述死結犧牲者。|以類似 XML 格式傳回不符合 XML 結構描述定義 (XSD) 結構描述的資訊。 此格式有三大區段。 第一個區段宣告死結犧牲者。 第二個區段描述死結所涉及的每一個處理序。 第三個區段描述與追蹤旗標 1204 中的節點同義的資源。|  
|識別屬性|**SPID:<x\> ECID:<x\>。** 識別平行處理序中的系統處理序識別碼執行緒。 `SPID:<x> ECID:0` 項目代表主執行緒，其中 <x\> 會被 SPID 值取代。 `SPID:<x> ECID:<y>` 項目代表相同 SPID 的子執行緒，其中<x\> 會被 SPID 值取代，而 <y\> 會大於 0。<br /><br /> **BatchID** (追蹤旗標 1222 的**sbid** )。 識別程式碼執行從中要求或保留鎖定的批次。 停用 Multiple Active Result Sets (MARS) 時，BatchID 值為 0。 啟用 MARS 時，作用中批次的值為 1 到 *n*。 如果工作階段中沒有作用中批次，BatchID 為 0。<br /><br /> **模式**。 指定執行緒所要求、授與或等待之特定資源的鎖定類型。 模式可為 IS (意圖共用)、S (共用)、U (更新)、IX (意圖獨佔)、SIX (共用意圖獨佔) 和 X (獨佔)。<br /><br /> **Line #** (追蹤旗標 1222 的**line** )。 列出發生死結時正在執行之目前陳述式批次中的行號。<br /><br /> **Input Buf** (追蹤旗標 1222 的**inputbuf** )。 列出目前批次中的所有陳述式。|**節點**。 代表死結鏈結中的項目號碼。<br /><br /> **清單**。 鎖定擁有者可以是這些清單的一部分：<br /><br /> **授與清單**。 列舉資源的目前擁有者。<br /><br /> **轉換清單**。 列舉嘗試將其鎖定轉換為更高層的目前擁有者。<br /><br /> **等待清單**。 列舉資源的目前最新鎖定要求。<br /><br /> **陳述式類型**。 描述執行緒有權限的 DML 陳述式的類型 (SELECT、INSERT、UPDATE 或 DELETE)。<br /><br /> **犧牲者資源擁有者**。 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 選擇作為犧牲者來中斷死結循環的參與執行緒。 選擇的執行緒和所有現存的子執行緒會終止。<br /><br /> **下一分支**。 代表相同 SPID 中兩個以上涉及死結循環的子執行緒。|**deadlock victim**。 代表被選為死結犧牲者之工作的實體記憶位址 (請參閱 [sys.dm_os_tasks &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md))。 在未解決的死結案例中，它可能會是 0 (零)。 回復中的工作不可選為死結犧牲者。<br /><br /> **executionstack**。 代表發生死結時正在執行的 [!INCLUDE[tsql](../includes/tsql-md.md)] 程式碼。<br /><br /> **priority**。 代表死結優先權。 在特定案例中， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 可能會選擇在短時間內變更死結優先權，以達到更佳的並行效果。<br /><br /> **logused**。 工作所使用的記錄檔空間。<br /><br /> **owner id**。具有要求控制權之交易的識別碼。<br /><br /> **status**。 工作的狀態。 它是下列其中一值：<br /><br /> >> **pending**。 等待工作者執行緒。<br /><br /> >> **runnable**。 可開始執行但等待配量。<br /><br /> >> **running**。 目前在排程器上執行。<br /><br /> >> **suspended**。 執行已暫停。<br /><br /> >> **done**。 工作已完成。<br /><br /> >> **spinloop**。 等待單一執行緒存取鎖變成可用。<br /><br /> **waitresource**。 工作所需的資源。<br /><br /> **waittime**。 等待資源的時間 (以毫秒為單位)。<br /><br /> **schedulerid**。 與這個工作相關聯的排程器。 請參閱 [sys.dm_os_schedulers &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)。<br /><br /> **hostname**。 工作站的名稱。<br /><br /> **isolationlevel**。 目前交易隔離等級。<br /><br /> **Xactid**。 具有要求控制權之交易的識別碼。<br /><br /> **currentdb**。 資料庫的識別碼。<br /><br /> **lastbatchstarted**。 用戶端處理序上次啟動批次執行的時間。<br /><br /> **lastbatchcompleted**。 用戶端處理序上次完成批次執行的時間。<br /><br /> **clientoption1 和 clientoption2**。 此用戶端連接上的設定選項。 這是位元遮罩，其中包含通常由 SET 陳述式 (例如 SET NOCOUNT 和 SET XACTABORT) 所控制之選項的資訊。<br /><br /> **associatedObjectId**。 代表 HoBT (堆積或 B 型樹狀目錄) 識別碼。|  
|資源屬性|**RID**。 識別在資料表內保留或要求鎖定的單一資料列。 RID 是以 RID: *db_id:file_id:page_no:row_no*表示。 例如： `RID: 6:1:20789:0` 。<br /><br /> **OBJECT**。 識別保留或要求鎖定的資料表。 OBJECT 是以 OBJECT: *db_id:object_id*表示。 例如： `TAB: 6:2009058193` 。<br /><br /> **KEY**。 識別在索引內保留或要求鎖定的索引鍵範圍。 KEY 是以 KEY: *db_id:hobt_id* (*index key hash value*) 表示。 例如： `KEY: 6:72057594057457664 (350007a4d329)` 。<br /><br /> **PAG**。 識別保留或要求鎖定的頁面資源。 PAG 是以 PAG: *db_id:file_id:page_no*表示。 例如： `PAG: 6:1:20789` 。<br /><br /> **EXT**。 識別範圍結構。 EXT 是以 EXT: *db_id:file_id:extent_no*表示。 例如： `EXT: 6:1:9` 。<br /><br /> **DB**。 識別資料庫鎖定。 **DB 會以下列其中一種方式表示：**<br /><br /> DB: *db_id*<br /><br /> DB: *db_id*[BULK-OP-DB]，識別備份資料庫使用的資料庫鎖定。<br /><br /> DB: *db_id*[BULK-OP-LOG]，識別該特定資料庫的備份記錄檔所使用的鎖定。<br /><br /> **APP**。 識別應用程式資源使用的鎖定。 APP 是以 APP: *lock_resource*表示。 例如： `APP: Formf370f478` 。<br /><br /> **METADATA**。 代表死結所涉及的中繼資料資源。 因為 METADATA 有許多子資源，所以傳回的值視含有死結的子資源而定。 例如，METADATA.USER_TYPE 會傳回 `user_type_id =` <*integer_value*>。 如需有關 METADATA 資源和子資源的詳細資訊，請參閱 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)。<br /><br /> **HOBT**。 代表死結所涉及的堆積或 B 型樹狀目錄。|None 與此追蹤旗標互斥。|None 與此追蹤旗標互斥。|  
  
##### <a name="trace-flag-1204-example"></a>追蹤旗標 1204 範例  
 下列範例顯示追蹤旗標 1204 開啟時的輸出。 在此案例中，節點 1 中的資料表是一個不含索引的堆積，節點 2 中的資料表是一個含非叢集索引的堆積。 當發生死結時，正在更新節點 2 中的索引鍵。  
  
```  
Deadlock encountered .... Printing deadlock information  
Wait-for graph  
  
Node:1  
  
RID: 6:1:20789:0               CleanCnt:3 Mode:X Flags: 0x2  
 Grant List 0:  
   Owner:0x0315D6A0 Mode: X          
     Flg:0x0 Ref:0 Life:02000000 SPID:55 ECID:0 XactLockInfo: 0x04D9E27C  
   SPID: 55 ECID: 0 Statement Type: UPDATE Line #: 6  
   Input Buf: Language Event:   
BEGIN TRANSACTION  
   EXEC usp_p2  
 Requested By:   
   ResType:LockOwner Stype:'OR'Xdes:0x03A3DAD0   
     Mode: U SPID:54 BatchID:0 ECID:0 TaskProxy:(0x04976374) Value:0x315d200 Cost:(0/868)  
  
Node:2  
  
KEY: 6:72057594057457664 (350007a4d329) CleanCnt:2 Mode:X Flags: 0x0  
 Grant List 0:  
   Owner:0x0315D140 Mode: X          
     Flg:0x0 Ref:0 Life:02000000 SPID:54 ECID:0 XactLockInfo: 0x03A3DAF4  
   SPID: 54 ECID: 0 Statement Type: UPDATE Line #: 6  
   Input Buf: Language Event:   
     BEGIN TRANSACTION  
       EXEC usp_p1  
 Requested By:   
   ResType:LockOwner Stype:'OR'Xdes:0x04D9E258   
     Mode: U SPID:55 BatchID:0 ECID:0 TaskProxy:(0x0475E374) Value:0x315d4a0 Cost:(0/380)  
  
Victim Resource Owner:  
 ResType:LockOwner Stype:'OR'Xdes:0x04D9E258   
     Mode: U SPID:55 BatchID:0 ECID:0 TaskProxy:(0x0475E374) Value:0x315d4a0 Cost:(0/380)  
```  
  
##### <a name="trace-flag-1222-example"></a>追蹤旗標 1222 範例  
 下列範例顯示追蹤旗標 1222 開啟時的輸出。 在此案例中，有一個資料表是不含索引的堆積，另一個資料表是含非叢集索引的堆積。 在第二份資料表中，當發生死結時，正在更新索引鍵。  
  
```  
deadlock-list  
 deadlock victim=process689978  
  process-list  
   process id=process6891f8 taskpriority=0 logused=868   
   waitresource=RID: 6:1:20789:0 waittime=1359 ownerId=310444   
   transactionname=user_transaction   
   lasttranstarted=2005-09-05T11:22:42.733 XDES=0x3a3dad0   
   lockMode=U schedulerid=1 kpid=1952 status=suspended spid=54   
   sbid=0 ecid=0 priority=0 transcount=2   
   lastbatchstarted=2005-09-05T11:22:42.733   
   lastbatchcompleted=2005-09-05T11:22:42.733   
   clientapp=Microsoft SQL Server Management Studio - Query   
   hostname=TEST_SERVER hostpid=2216 loginname=DOMAIN\user   
   isolationlevel=read committed (2) xactid=310444 currentdb=6   
   lockTimeout=4294967295 clientoption1=671090784 clientoption2=390200  
    executionStack  
     frame procname=AdventureWorks2016.dbo.usp_p1 line=6 stmtstart=202   
     sqlhandle=0x0300060013e6446b027cbb00c69600000100000000000000  
     UPDATE T2 SET COL1 = 3 WHERE COL1 = 1;       
     frame procname=adhoc line=3 stmtstart=44   
     sqlhandle=0x01000600856aa70f503b8104000000000000000000000000  
     EXEC usp_p1       
    inputbuf  
      BEGIN TRANSACTION  
       EXEC usp_p1  
   process id=process689978 taskpriority=0 logused=380   
   waitresource=KEY: 6:72057594057457664 (350007a4d329)     
   waittime=5015 ownerId=310462 transactionname=user_transaction   
   lasttranstarted=2005-09-05T11:22:44.077 XDES=0x4d9e258 lockMode=U   
   schedulerid=1 kpid=3024 status=suspended spid=55 sbid=0 ecid=0   
   priority=0 transcount=2 lastbatchstarted=2005-09-05T11:22:44.077   
   lastbatchcompleted=2005-09-05T11:22:44.077   
   clientapp=Microsoft SQL Server Management Studio - Query   
   hostname=TEST_SERVER hostpid=2216 loginname=DOMAIN\user   
   isolationlevel=read committed (2) xactid=310462 currentdb=6   
   lockTimeout=4294967295 clientoption1=671090784 clientoption2=390200  
    executionStack  
     frame procname=AdventureWorks2016.dbo.usp_p2 line=6 stmtstart=200   
     sqlhandle=0x030006004c0a396c027cbb00c69600000100000000000000  
     UPDATE T1 SET COL1 = 4 WHERE COL1 = 1;       
     frame procname=adhoc line=3 stmtstart=44   
     sqlhandle=0x01000600d688e709b85f8904000000000000000000000000  
     EXEC usp_p2       
    inputbuf  
      BEGIN TRANSACTION  
        EXEC usp_p2      
  resource-list  
   ridlock fileid=1 pageid=20789 dbid=6 objectname=AdventureWorks2016.dbo.T2   
   id=lock3136940 mode=X associatedObjectId=72057594057392128  
    owner-list  
     owner id=process689978 mode=X  
    waiter-list  
     waiter id=process6891f8 mode=U requestType=wait  
   keylock hobtid=72057594057457664 dbid=6 objectname=AdventureWorks2016.dbo.T1   
   indexname=nci_T1_COL1 id=lock3136fc0 mode=X   
   associatedObjectId=72057594057457664  
    owner-list  
     owner id=process6891f8 mode=X  
    waiter-list  
     waiter id=process689978 mode=U requestType=wait  
```  
  
#### <a name="profiler-deadlock-graph-event"></a>Profiler 死結圖形事件  
這是 SQL Profiler 中的一個事件，SQL Profiler 會顯示涉及死結之工作和資源的圖形化描述。 下列範例顯示開啟 Deadlock Graph 事件時 SQL Profiler 的輸出。  
  
 ![ProfilerDeadlockGraphc](../relational-databases/media/udb9_ProfilerDeadlockGraphc.png)  
  
如需有關死結事件的詳細資訊，請參閱 [Lock:Deadlock 事件類別](../relational-databases/event-classes/lock-deadlock-event-class.md)。

如需有關執行 SQL Profiler Deadlock Graph 的詳細資訊，請參閱[儲存 Deadlock Graph &#40;SQL Server Profiler&#41;](../relational-databases/performance/save-deadlock-graphs-sql-server-profiler.md)。  
  
### <a name="handling-deadlocks"></a>處理死結  
 當 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]執行個體選擇某個交易作為死結犧牲者時，會終止目前的批次、復原交易，然後將錯誤訊息 1205 傳回給應用程式。  
  
 `Your transaction (process ID #52) was deadlocked on {lock | communication buffer | thread} resources with another process and has been chosen as the deadlock victim. Rerun your transaction.`  
  
 由於任何提交 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢的應用程式都可能被選為死結的犧牲者，應用程式應該要有錯誤處理常式來攔截錯誤訊息 1205。 如果應用程式不捕捉此錯誤，就不知道其交易已經復原而繼續執行，此時就會發生錯誤。  
  
 實作捕捉錯誤訊息 1205 的錯誤處理常式，讓應用程式得以處理死結的狀況並採取補救措施 (例如，將陷入死結的查詢自動重新送出)。 藉由自動重新送出查詢，使用者就不需要知道死結曾經發生。  
  
 應用程式應該在重新送出查詢之前稍做停頓。 這可讓死結中的另一筆交易有機會完成動作，並釋放它讓死結循環形成的鎖定。 這樣一來，當重新送出的查詢要求鎖定時，就比較不會再度發生死結的情形。  
  
### <a name="minimizing-deadlocks"></a><a name="deadlock_minimizing"></a> 將死結數目降至最低  
 雖然死結無法完全避免，但是遵守某些程式碼撰寫的慣例可以將死結產生的機會降到最低。 將死結降至最低可以提高交易的產能並降低系統額外負荷，因為較少的交易需要：  
  
-   回復，將交易所進行的工作全部恢復。  
-   由應用程式重新送出，因為發生死結時已將交易回復。  
  
 若要協助將死結降至最低：  
  
-   以相同的順序來存取物件。  
-   在交易中避免使用者互動。  
-   將交易維持在單一批次中且愈短愈好。  
-   使用較低的隔離等級。  
-   使用資料列版本設定基礎的隔離等級。  
    -   將 `READ_COMMITTED_SNAPSHOT` 資料庫選項設為 ON，以允許讀取認可交易使用資料列版本設定。  
    -   使用快照隔離。  
-   使用繫結連接。  
  
#### <a name="access-objects-in-the-same-order"></a>以相同的順序存取物件  
 如果所有同時發生的交易都以相同的順序來存取物件，就比較不會發生死結。 例如，如果同時發生的兩筆交易都取得 **Supplier** 資料表的鎖定，再取得 **Part** 資料表的鎖定，其中一筆交易便被封鎖於 **Supplier** 資料表直到另一筆交易完成為止。 第一筆交易認可或回復之後，第二筆才會繼續，這樣就不會發生死結。 使用預存程序來進行所有的資料修改動作可將物件的存取順序標準化。  
  
 ![deadlock2](../relational-databases/media/dedlck2.png)  
  
#### <a name="avoid-user-interaction-in-transactions"></a>在交易中避免使用者互動  
 避免撰寫包含使用者互動的交易，因為沒有使用者介入的批次執行速度比使用者必須對查詢做出手動回應的批次更快，例如對應用程式所要求的參數提示做出回覆。 例如，交易如果正在等候使用者輸入，而使用者去用餐，或甚至回家渡假，交易就會被使用者延遲而無法完成。 如此便會降低系統產能，因為交易所持有的任何鎖定只有在交易被認可或回復之後才會釋放。 即使並未發生死結的狀況，要存取相同資源的其他交易還是會被封鎖而等待交易完成。  
  
#### <a name="keep-transactions-short-and-in-one-batch"></a>將交易維持在單一批次中且愈短愈好  
 死結通常會在許多長時間執行的交易同時執行於相同的資料庫時發生。 交易的時間愈久，持有的獨占或更新鎖定就愈久，因而封鎖了其他的活動並導致發生死結狀況的可能性。  
  
 將交易維持在單一批次中可降低交易期間的網路來回次數，因而降低了完成交易以及釋放鎖定的延遲可能性。  
  
#### <a name="use-a-lower-isolation-level"></a>使用較低的隔離等級  
 判斷是否可以較低的隔離等級執行交易。 實作讀取認可讓交易可以對另一筆交易先前讀取 (未修改) 的資料進行讀取，而不必等待前一筆交易完成。 使用較低的隔離等級 (如讀取認可)，則持有共用鎖定的期間比使用較高的隔離等級(如序列化) 更短。 如此就可減少鎖定競爭。  
  
#### <a name="use-a-row-versioning-based-isolation-level"></a>使用資料列版本設定基礎的隔離等級  
 當 `READ_COMMITTED_SNAPSHOT` 資料庫選項設定為 ON 時，在讀取認可隔離等級下執行的交易在讀取作業期間，會使用資料列版本設定，而不是使用共用鎖定。  
  
> [!NOTE]  
> 部份應用程式則依靠讀取認可隔離的鎖定和鎖定行為。 對於這些應用程式，在啟用選項之前，需要進行部份變更。  
  
 快照隔離也使用資料列版本設定，不使用讀取作業期間的共用鎖定。 `ALLOW_SNAPSHOT_ISOLATION` 資料庫選項必須設定為 ON，交易才能在快照集隔離下執行。  
  
 實作這些隔離等級可將讀取和寫入作業之間發生的死結降到最低。  
  
#### <a name="use-bound-connections"></a>使用繫結連接  
 使用繫結連接，則同一個應用程式所開啟的二或多個連接可以互相合作。 如果先前由主要連接獲得鎖定，則會讓次要連接持有獲得的鎖定，反之亦然。 所以它們不會互相鎖定。  
  
## <a name="lock-partitioning"></a><a name="lock_partitioning"></a> 鎖定資料分割  
 對於大型電腦系統而言，鎖定經常參考的物件將會形成效能瓶頸，這是因為鎖定的取得與釋放，將會在內部鎖定資源上引發競爭問題。 鎖定資料分割可將單一鎖定資源分割成多個鎖定資源，進而增強鎖定效能。 這項功能僅適用於擁有 16 顆以上 CPU 的系統，而且它會自動啟用，而不能停用。 只有物件鎖定可以被分割。具有子類型的物件鎖定不能被分割。 如需詳細資訊，請參閱 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)。  
  
### <a name="understanding-lock-partitioning"></a>認識鎖定資料分割  
 鎖定工作會存取數項共用資源，其中兩項資源會因鎖定資料分割而最佳化：  
  
-   **單一執行緒存取鎖**。 這個資源控制對鎖定資源 (例如資料列或資料表) 的存取。  
  
     若沒有鎖定資料分割，便會由單一執行緒存取鎖，管理所有鎖定要求的單一鎖定資源。 在經歷大量活動的系統上，因為有許多鎖定要求等候單一執行緒存取鎖變成可用狀態，所以會發生競爭問題。 在這種情況下，取得鎖定將會形成瓶頸，進而對效能產生負面的影響。  
  
     為了減少單一鎖定資源上的競爭問題，鎖定資料分割會把單一鎖定資源分割成多個鎖定資源，以將負載分散到多個單一執行緒存取鎖。  
  
-   **記憶體**。 這個資源用來儲存鎖定資源結構。  
  
     取得單一執行緒存取鎖之後，鎖定結構就會儲存在記憶體中以待存取，甚至修改。 將鎖定存取分散到多個資源，有助於省去在 CPU 之間傳輸記憶體區塊的需要，而這有利於改善效能。  
  
### <a name="implementing-and-monitoring-lock-partitioning"></a>實作與監視鎖定資料分割  
 在擁有 16 顆以上 CPU 的系統中，鎖定資料分割預設會開啟。 啟用鎖定資料分割時，會在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 錯誤記錄檔中記錄參考用訊息。  
  
 在資料分割資源上取得鎖定時：  
  
-   只有 NL、SCH-S、IS、IU 和 IX 鎖定模式是在單一資料分割上取得。  
  
-   在非 NL、SCH-S、IS、IU 和 IX 的模式下，所有資料分割上都必須取得共用 (S)、獨佔 (X) 和其他鎖定，順序為先在資料分割識別碼為 0 的資料分割上開始取得，接著再依照識別碼順序在其他資料分割上取得。 這些在資料分割資源上的鎖定將比相同模式下的非資料分割資源上的鎖定，佔用更多的記憶體，這是因為每個資料分割實際上都是一個不同的鎖定。 記憶體的增加取決於資料分割的數目。 「Windows 效能監視器」中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 鎖定計數器將會顯示有關資料分割鎖定和非資料分割鎖定所佔用記憶體的資訊。  
  
 啟動交易時，系統會將交易指派給資料分割。 對於交易而言，所有可以分割的鎖定要求都會使用指派給該交易的資料分割。 使用這個方法，不同交易對同一個物件的鎖定資源的存取，都會分散到不同的資料分割。  
  
 `sys.dm_tran_locks` 動態管理檢視中的 `resource_lock_partition` 資料行會提供鎖定資料分割資源的鎖定資料分割識別碼。 如需詳細資訊，請參閱 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)。  
  
### <a name="working-with-lock-partitioning"></a>使用鎖定資料分割  
 下列程式碼範例說明了鎖定資料分割。 在這些範例中，會在兩個不同的工作階段中各執行一個交易，以便顯示在具有 16 顆 CPU 之電腦系統上的鎖定資料分割行為。  
  
 下列 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式會建立稍後範例中將會使用的測試物件。  
  
```sql  
-- Create a test table.  
CREATE TABLE TestTable  (col1 int);  
GO  
  
-- Create a clustered index on the table.  
CREATE CLUSTERED INDEX ci_TestTable   
    ON TestTable (col1);  
GO  
  
-- Populate the table.  
INSERT INTO TestTable VALUES (1);  
GO  
```  
  
#### <a name="example-a"></a>範例 A  
 工作階段 1：  
  
 `SELECT` 陳述式會在交易之下執行。 因為有 `HOLDLOCK` 鎖定提示，所以這個陳述式將在資料表上取得及保留意圖共用 (IS) 鎖定 (在這個範例中，將忽略資料列和頁面鎖定)。 只有在指派給交易的資料分割上能取得 IS 鎖定。 在這個範例中，假設是在分割區 ID 7 上取得 IS 鎖定。  
  
```sql  
-- Start a transaction.  
BEGIN TRANSACTION  
    -- This SELECT statement will acquire an IS lock on the table.  
    SELECT col1  
    FROM TestTable  
    WITH (HOLDLOCK);  
```  
  
 工作階段 2：  
  
 啟動交易，在這個交易之下執行的 `SELECT` 陳述式將在資料表上取得及保留共用 (S) 鎖定。 所有資料分割上都能取得 S 鎖定，而這會造成多個資料表鎖定，每一個都是針對一個資料分割。 例如在 16 個 CPU 的系統上，將會橫跨鎖定資料分割識別碼 0-15 來發出 16 S 鎖定。 因為 S 鎖定與資料分割識別碼 7 上由工作階段 1 中之交易所持有的 IS 鎖定相容，所以交易之間不會發生封鎖現象。  
  
```sql  
BEGIN TRANSACTION  
    SELECT col1  
    FROM TestTable  
    WITH (TABLOCK, HOLDLOCK);  
```  
  
 工作階段 1：  
  
 下列 `SELECT` 陳述式會在工作階段 1 中仍在使用中的交易下執行。 因為有獨佔 (X) 資料表鎖定提示，所以交易將會嘗試取得資料表上的 X 鎖定。 不過，由工作階段 2 中之交易所持有的 S 鎖定，將會封鎖資料分割識別碼 0 的 X 鎖定。  
  
```sql  
SELECT col1  
FROM TestTable  
WITH (TABLOCKX);  
```  
  
#### <a name="example-b"></a>範例 B  
 工作階段 1：  
  
 `SELECT` 陳述式會在交易之下執行。 因為有 `HOLDLOCK` 鎖定提示，所以這個陳述式將在資料表上取得及保留意圖共用 (IS) 鎖定 (在這個範例中，將忽略資料列和頁面鎖定)。 只有在指派給交易的資料分割上能取得 IS 鎖定。 在這個範例中，假設是在資料分割識別碼 6 上取得 IS 鎖定。  
  
```sql  
-- Start a transaction.  
BEGIN TRANSACTION  
    -- This SELECT statement will acquire an IS lock on the table.  
    SELECT col1  
    FROM TestTable  
    WITH (HOLDLOCK);  
```  
  
 工作階段 2：  
  
 `SELECT` 陳述式會在交易之下執行。 因為有 `TABLOCKX` 封鎖提示，所以交易會嘗試在資料表上取得獨佔 (X) 鎖定。 請記住，必須在資料分割識別碼 0 開頭的所有資料分割上取得 X 鎖定。 從資料分割識別碼 0 到 5 的所有資料分割上都會取得 X 鎖定，但是在資料分割識別碼 6 上取得的鎖定將會遭到 IS 鎖定封鎖。  
  
 其他交易可以在 X 鎖定還沒到達的資料分割識別碼 7 到 15 上繼續取得鎖定。  
  
```sql  
BEGIN TRANSACTION  
    SELECT col1  
    FROM TestTable  
    WITH (TABLOCKX, HOLDLOCK);  
```   
  
##  <a name="row-versioning-based-isolation-levels-in-the-ssdenoversion"></a><a name="Row_versioning"></a>[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]中的資料列版本設定型隔離等級  
 從 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 開始，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]便提供現有之讀取認可交易隔離等級的實作，這可使用資料列版本設定來提供陳述式層級的快照集。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]也提供快照交易隔離等級，這同樣是使用資料列版本設定，但提供交易層級的快照集。  
  
 資料列版本設定是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的一般架構，會在資料列遭修改或刪除的情況下叫用寫入時複製機制。 為此，當交易正在執行時，舊版本的資料列務必可供仍需要早先交易一致狀態的交易使用。 資料列版本設定用於執行下列事項：  
  
-   在觸發程序中建立 **inserted** 及 **deleted** 資料表。 經由觸發程序修改過的任何資料列都會被建立版本。 這包括啟動觸發程序之陳述式所修改的資料列，以及觸發程序所做的任何資料修改。  
-   支援 Multiple Active Result Sets (MARS)。 如果 MARS 工作階段在有作用中結果集的情況下，發出資料修改陳述式 (例如 `INSERT``UPDATE`或 `DELETE`)，就會為修改陳述式所影響的資料列建立版本。  
-   支援指定 ONLINE 選項的索引作業。  
-   支援以資料列版本設定為基礎的交易隔離等級：  
    -   新的讀取認可隔離等級實作方式，其使用資料列版本設定來提供陳述式層級的讀取一致性。  
    -   新的隔離等級 (快照集)，可以提供交易等級的讀取一致性。  
  
 `tempdb` 資料庫必須要有足夠的空間供版本存放區使用。 當 `tempdb` 已滿時，更新作業會停止產生版本並繼續執行成功，但讀取作業可能會失敗，因為所需的特定資料列版本已不存在。 這會影響到像是觸發程序、MARS 及線上檢索索引之類的作業。  
  
 針對讀取認可及快照交易，使用資料列版本設定的方法是兩個步驟的程序：  
  
1.  將 `READ_COMMITTED_SNAPSHOT` 和 `ALLOW_SNAPSHOT_ISOLATION` 資料庫選項其中之一或兩者都設定為 ON。  
2.  在應用程式中設定適當的交易隔離等級：  

    -   當 `READ_COMMITTED_SNAPSHOT` 資料庫選項為 ON 時，設定讀取認可隔離等級的交易就會使用資料列版本設定。  
    -   當 `ALLOW_SNAPSHOT_ISOLATION` 資料庫選項為 ON 時，交易便可設定快照隔離等級。  
  
 當 `READ_COMMITTED_SNAPSHOT` 或 `ALLOW_SNAPSHOT_ISOLATION` 資料庫選項設定為 ON 時，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]會使用資料列版本設定，為每個操作資料的交易都指派一個交易序號 (XSN)。 交易會在執行 `BEGIN TRANSACTION` 陳述式時開始。 但是交易序號會從 BEGIN TRANSACTION 陳述式之後的第一個讀取或寫入作業開始。 每指定一個交易序號，就會累加一個號碼。  
  
 當 `READ_COMMITTED_SNAPSHOT` 或 `ALLOW_SNAPSHOT_ISOLATION` 其中一個資料庫選項為 ON 時，就會針對在資料庫中執行的所有資料修改來維護邏輯複本 (版本)。 每次特定交易修改資料列時，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]執行個體都會在 `tempdb` 中儲存先前認可的資料列映像版本。 每個版本都會標示執行變更之交易的交易序號。 修改過的資料列版本會以連結清單鏈結起來。 最新的資料列值一律儲存在目前的資料庫中，並鏈結到儲存在 `tempdb` 中已設定版本的資料列。  
  
> [!NOTE]  
> 針對大型物件 (LOB) 修改，只會將變更過的片段複製到 `tempdb` 中的版本存放區。  
  
 資料列版本會被保存夠久的時間，可滿足以資料列版本設定為基礎之隔離等級來執行的交易需求。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會追蹤最早的有用交易序號，並定期刪除交易序號低於最早有用交易序號的所有資料列版本。  
  
 當兩個資料庫選項都設為 OFF 時，就只會針對由觸發程序或 MARS 工作階段所修改的資料列，或是由 ONLINE (線上) 索引作業所讀取的資料列來建立版本。 不再需要那些資料列版本時，就會將其釋出。 背景執行緒會定期執行，以移除過時的資料列版本。  
  
> [!NOTE]  
> 針對短期交易，可能會將修改過的資料列版本快取至緩衝集區，而不會寫入至 `tempdb` 資料庫的磁碟檔案。 如果已建立版本的資料列不需要存在很長的時間，就會直接將它從緩衝集區中卸除，而且不一定會引起 I/O 額外負荷。  
  
### <a name="behavior-when-reading-data"></a>讀取資料時的行為  
 在以資料列版本設定為基礎之隔離下執行的交易要讀取資料時，讀取作業不會在所讀取的資料上取得共用 (S) 鎖定，因此不會阻礙正在修改資料的交易。 此外，隨著所取得的鎖定數量減少，鎖定資源的額外負荷也會降低。 使用資料列版本設定及快照隔離的讀取認可隔離作業，目的就是要提供已建立版本之資料的陳述式層級或交易等級讀取一致性。  
  
 所有的查詢，包括在資料列版本設定式隔離等級下執行的交易，都會在編譯和執行期間取得 Sch-S (結構描述穩定性) 鎖定。 因此，當並行交易在資料表上保有 Sch-M (結構描述修改) 鎖定時，查詢將會遭到封鎖。 例如，資料定義語言 (DDL) 作業會在修改資料表的結構描述資訊之前先取得 Sch-M 鎖定。 查詢交易，包括在資料列版本設定式隔離等級下執行的交易，在嘗試取得 Sch-S 鎖定時都會遭到封鎖。 相反地，保有 Sch-S 鎖定的查詢將會封鎖嘗試取得 Sch-M 鎖定的並行交易。  
  
 當使用快照隔離等級的交易開始時， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的執行個體會記錄目前所有的使用中交易。 當快照交易讀取具有版本鏈結的資料列時， [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會依循該鏈結，並擷取下列交易序號的資料列：  
  
-   最接近但小於讀取該資料列之快照交易的序號。  
  
-   當快照交易開始時，不在使用中交易清單裡的序號。  
  
 快照集交易所執行的讀取作業會在快照集交易開始時，擷取已認可之每個資料列的最新版本。 這樣可以讓資料快照集在交易期間保持一致，就像交易一開始的資料一樣。  
  
 使用資料列版本設定的讀取認可交易運作的方式也相當類似。 不同的地方在於，讀取認可交易在選擇資料列版本時，不會使用自己的交易序號。 每當有陳述式開始時，讀取認可交易就會讀取針對該 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]執行個體所發出的最新交易序號。 這個交易序號可用來為該陳述式選取正確的資料列版本。 這樣可以讓讀取認可交易看到與每個陳述式開始時相同的資料快照。  
  
> [!NOTE]  
> 即使使用資料列版本設定的讀取認可交易可以提供陳述式層級資料的交易一致性檢視，這種類型的交易所產生或存取的資料列版本還是會保留到交易完成為止。  
  
### <a name="behavior-when-modifying-data"></a>修改資料時的行為  
 在使用資料列版本設定的讀取認可交易中，會使用封鎖掃描來選取要更新的資料列，在封鎖掃描中，當資料值被讀取時，就會在資料列上進行更新 (U) 鎖定。 這與不使用資料列版本設定的讀取認可交易是一樣的。 如果資料列不符合更新條件，就會解除該資料列的更新鎖定，並且會鎖定及掃描下一個資料列。  
  
 在快照集隔離下執行的交易會使用開放式的方法來修改資料，在修改資料之前，會在資料上取得鎖定，只強制執行條件約束。 否則，在修改資料之前，不會在資料上取得鎖定。 當資料列符合更新條件，快照交易會確認資料列尚未被快照交易開始之後認可的並行交易所修改。 如果資料列已在快照交易外被修改，就會發生更新衝突，並終止快照交易。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會處理更新衝突，而且沒有可以停用更新衝突偵測的方法。  
  
> [!NOTE]  
> 當快照交易存取以下任一項時，在快照隔離下執行的更新作業，會在讀取認可隔離之下於內部執行：  
>  
> 具有 FOREIGN KEY 條件約束的資料表。  
>  
> 被另一個資料表的 FOREIGN KEY 條件約束所參考的資料表。  
>  
> 參照多個資料表的索引檢視。  
>  
> 然而，即使有這些條件限制，更新作業仍會繼續確認資料尚未被其他交易所修改。 如果資料已被其他交易所修改，快照交易會發生更新衝突，並終止作業。  
  
### <a name="behavior-in-summary"></a>行為摘要  
 下表摘要說明使用資料列版本設定之快照隔離與讀取認可隔離之間的差異。  
  
|屬性|使用資料列版本設定的讀取認可隔離等級|快照隔離等級|  
|--------------|----------------------------------------------------------|------------------------------|  
|資料庫選項必須設為 ON，才能啟用必要的支援。|READ_COMMITTED_SNAPSHOT|ALLOW_SNAPSHOT_ISOLATION|  
|工作階段如何要求特定類型的資料列版本設定。|使用預設的讀取認可隔離等級，或是執行 SET TRANSACTION ISOLATION LEVEL 陳述式來指定 READ COMMITTED 隔離等級。 您可以在交易開始後完成此作業。|需要執行 SET TRANSACTION ISOLATION LEVEL，以在交易開始之前指定 SNAPSHOT 隔離等級。|  
|陳述式所讀取的資料版本。|在每個陳述式開始之前認可的所有資料。|在每個交易開始之前認可的所有資料。|  
|如何處理更新。|從資料列版本還原成實際的資料，以選取要更新的資料列，並且在所選取的資料列上使用更新鎖定。 在所要修改的實際資料列上取得獨佔鎖定。 無更新衝突偵測。|使用資料列版本來選取要更新的資料列。 嘗試在所要修改的實際資料列上取得獨佔鎖定，若該資料已被其他交易所修改，就會發生更新衝突，且快照交易會終止進行。|  
|更新衝突偵測。|無。|整合支援。 無法停用。|  
  
### <a name="row-versioning-resource-usage"></a>資料列版本設定資源的使用方式  
 資料列版本設定架構支援 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中提供的下列功能：  
  
-   觸發程序  
-   Multiple Active Result Set (MARS)  
-   線上檢索索引  
  
 資料列版本設定架構也支援下列資料列版本設定式的交易隔離等級 (預設不會啟用)：  
  
-   當 `READ_COMMITTED_SNAPSHOT` 資料庫選項為 ON 時，`READ_COMMITTED` 交易會使用資料列版本設定，來提供陳述式層級讀取一致性。  
-   當 `ALLOW_SNAPSHOT_ISOLATION` 資料庫選項為 ON 時，`SNAPSHOT` 交易會使用資料列版本設定，來提供交易層級讀取一致性。  
  
 資料列版本設定式的隔離等級因為不需對讀取作業使用共用鎖定，因而減少交易所取得的鎖定數。 如此可減少用來管理鎖定的資源，進而增加系統效能。 減少交易被其他交易所取得的鎖定封鎖的次數，也可以增加效能。  
  
 資料列版本設定式的隔離等級會增加資料修改所需的資源。 啟用這些選項會使資料庫的所有資料修改建立版本。 即使沒有使用資料列版本設定式的隔離之使用中交易，也會將修改前的資料副本儲存在 tempdb 中。 修改後的資料包括 tempdb 所儲存的版本化資料的指標。 若為大型物件，則所變更的物件只有一部分會複製到 tempdb 中。  
  
#### <a name="space-used-in-tempdb"></a>TempDB 中使用的空間  
 對於 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的每一個執行個體，tempdb 必須有足夠空間來保存該執行個體中每一個資料庫所產生的資料列版本。 資料庫管理員必須確定 TempDB 有很大的空間可支援版本存放區。 TempDB 中有兩個版本存放區：  
  
-   線上索引組建版本存放區會用於所有資料庫的線上索引組建。  
-   一般版本存放區，用於所有資料庫的所有其他資料修改作業。  
  
 資料列版本儲存的時間必須夠久，讓使用中交易可以存取它。 每隔一分鐘，背景執行緒就會移除不再需要的資料列版本，並釋放 TempDB 中的版本空間。 長時間執行的交易如果符合下列任何條件，就可以阻止釋放版本存放區的空間。  
  
-   它使用資料列版本設定式的隔離。  
-   它使用觸發程序、MARS 或線上索引組建作業。  
-   它產生資料列版本。  
  
> [!NOTE]  
> 在交易內叫用觸發程序時，會維護觸發程序建立的資料列版本，直到交易結束為止，即使在觸發程序完成之後不再需要資料列版本也一樣。 這也適用於使用資料列版本設定的讀取認可交易。 以此交易類型而言，只有在交易中的每一個陳述式才需要資料庫的交易一致檢視。 這表示當交易中的陳述式完成之後，就不再需要為該陳述式建立的資料列版本。 不過，仍會維護交易中每一個陳述式所建立的資料列版本，直到交易完成為止。  
  
 當 TempDB 空間不夠時，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會強制版本存放區壓縮。 在壓縮處理期間，執行最久但尚未產生資料列版本的交易會標示為犧牲者。 在錯誤記錄檔中會針對每一筆犧牲者交易產生訊息 3967。 如果交易已標示為犧牲者，它就不能再讀取版本存放區中的資料列版本。 當它嘗試讀取資料列版本時，會產生訊息 3966 而且會回復交易。 如果壓縮處理成功，tempdb 中的空間就會變成可用。 否則，tempdb 的空間會不足，而且會發生下列情況：  
  
-   寫入作業繼續執行，但不產生版本。 在錯誤記錄檔中會出現資訊訊息 (3959)，但寫入資料的交易不受影響。  
  
-   交易嘗試存取的資料列版本若因為 tempdb 完全回復而未產生，則交易會終止，並出現錯誤 3958。  
  
#### <a name="space-used-in-data-rows"></a>資料列中使用的空間  
 每個資料庫的資料列在資料列結尾可使用最多 14 個位元組，以存放資料列版本設定資訊。 資料列版本設定資訊包含認可版本之交易的交易序號，以及版本化資料列的指標。 這 14 個位元組會在第一次修改資料列或插入新的資料列時，而且符合下列任一情況時加入：  
  
-   `READ_COMMITTED_SNAPSHOT` 或 `ALLOW_SNAPSHOT_ISOLATION` 選項為 ON。  
-   資料表有觸發程序。  
-   使用 Multiple Active Result Set (MARS)。  
-   目前正在資料表執行線上索引組建作業。  
  
 在下列這些情況下，第一次修改資料列時會從資料庫中移除這 14 個位元組：  
  
-   `READ_COMMITTED_SNAPSHOT` 或 `ALLOW_SNAPSHOT_ISOLATION` 選項為 OFF。  
-   觸發程序已不在資料表上。  
-   不使用 MARS。  
-   目前沒有執行中的線上索引建立作業。  
  
 如果您使用任何資料列版本設定功能，您可能需要配置額外的磁碟空間給資料庫，以容納每個資料庫資料列的 14 個位元組。 如果目前頁面沒有足夠的可用空間，則加入資料列版本設定資訊會造成索引頁面分割或需要配置新的資料頁。 例如，如果平均資料列長度是 100 個位元組，則額外的 14 個位元組會造成現有資料表成長高達百分之 14。  
  
 降低[填滿因數](../relational-databases/indexes/specify-fill-factor-for-an-index.md)可能有助於防止或減少索引頁片段。 若要檢視資料表或檢視表之資料與索引的片段資訊，您可以使用 [sys.dm_db_index_physical_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)。  
  
#### <a name="space-used-in-large-objects"></a>大型物件中使用的空間  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 支援 6 種資料類型，可保留長度多達 2 GB 的大型字串：`nvarchar(max)`、`varchar(max)`、`varbinary(max)`、`ntext`、`text` 和 `image`。 使用這些資料類型儲存的大型字串是儲存在一系列資料片段中，而這些片段是連結到資料列。 資料列版本設定資訊是儲存在用來儲存這些大型字串的每一個片段中。 資料片段是專供資料表中大型物件使用的頁面集合。  
  
 當新的大型值加入至資料庫時，會使用每個片段最多 8040 個位元組的資料來配置它們。 舊版的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 中，每個片段儲存最多 8080 個位元組的 `ntext`、`text` 或 `image` 資料。  
  
 當資料庫從舊版的 `ntext` 升級到 `text` 時，並不會更新現有的 `image`、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 大型物件 (LOB) 資料來提供存放資料列版本設定資訊的空間。 不過，第一次修改 LOB 資料時，它會動態升級，以啟用版本控制資訊的儲存。 即使未產生資料列版本也會發生此情況。 當 LOB 資料升級之後，每個片段儲存的最大位元組數會從 8080 個位元組降到 8040 個位元組。 升級程序相當於刪除 LOB 值及重新插入相同值。 即使只修改一個位元組，也會升級 LOB 資料。 每一個 `ntext`、`text` 或 `image` 資料行只有一次作業，但每一個作業可產生大量頁面配置和 I/O 活動，視 LOB 資料大小而定。 如果有完整記錄各項修改，則它也可能產生大量記錄活動。 如果資料庫復原模式未設為 FULL，則會為 WRITETEXT 和 UPDATETEXT 作業做最少的記錄。  
  
 舊版的 `nvarchar(max)` 並沒有提供 `varchar(max)`、`varbinary(max)` 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料類型。 因此，它們沒有升級問題。  
  
 應該配置足夠的磁碟空間來配合這項需求。  
  
#### <a name="monitoring-row-versioning-and-the-version-store"></a>監視資料列版本設定和版本存放區  
 為了效能和問題而監視資料列版本設定、版本存放區和快照集隔離程序， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 以動態管理檢視 (DMV) 的形式提供工具，以及在 Windows 系統監視器中提供效能計數器。  
  
##### <a name="dmvs"></a>DMV  
 下列 DMV 提供關於 tempdb 和版本存放區的目前系統狀態，以及使用資料版本控制的交易之資訊。  
  
 sys.dm_db_file_space_usage。 傳回資料庫中每一個檔案的空間使用方式資訊。 如需詳細資訊，請參閱 [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)。  
  
 sys.dm_db_session_space_usage。 由資料庫的工作階段傳回頁面配置和取消配置活動。 如需詳細資訊，請參閱 [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)。  
  
 sys.dm_db_task_space_usage。 傳回資料庫工作的頁面配置及取消配置活動。 如需詳細資訊，請參閱 [sys.dm_db_task_space_usage &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)。  
  
 sys.dm_tran_top_version_generators。 針對產生版本存放區中大部分版本的物件，傳回一份虛擬資料表。 它按 database_id 和 rowset_id 來分組前 256 個彙總記錄長度。 使用此函數可尋找版本存放區的最大取用者。 如需詳細資訊，請參閱 [sys.dm_tran_top_version_generators &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-top-version-generators-transact-sql.md)。  
  
 sys.dm_tran_version_store。 傳回虛擬資料表來顯示一般版本存放區中的所有版本記錄。 如需詳細資訊，請參閱 [sys.dm_tran_version_store &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md)。  

 sys.dm_tran_version_store_space_usage。 傳回一個虛擬資料表，其中顯示每個資料庫之版本存放區記錄在 tempdb 中所使用的總空間。 如需詳細資訊，請參閱 [sys.dm_tran_version_store_space_usage &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md)。  

> [!NOTE]  
> sys.dm_tran_top_version_generators 和 sys.dm_tran_version_store 可能是執行代價很高的函數，因為兩者會查詢有可能是非常龐大的整個版本存放區。  
> sys.dm_tran_version_store_space_usage 相當有效率且執行成本不高，因為它不會瀏覽個別的版本存放區記錄，而是會傳回每個資料庫在 tempdb 中所使用的已彙總版本存放區空間
  
 sys.dm_tran_active_snapshot_database_transactions。 在使用資料列版本設定的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體內，傳回所有資料庫的所有使用中交易的虛擬資料表。 系統交易不會出現在這個 DMV 中。 如需詳細資訊，請參閱 [sys.dm_tran_active_snapshot_database_transactions &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md)。  
  
 sys.dm_tran_transactions_snapshot。 傳回虛擬資料表，以顯示每一筆交易所產生的快照集。 快照集包含使用了資料列版本設定之使用中交易的序號。 如需詳細資訊，請參閱 [sys.dm_tran_transactions_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-transactions-snapshot-transact-sql.md)。  
  
 sys.dm_tran_current_transaction。 傳回單一資料列，顯示目前工作階段中交易的資料列版本設定相關之狀態資訊。 如需詳細資訊，請參閱 [sys.dm_tran_current_transaction &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-current-transaction-transact-sql.md)。  
  
 sys.dm_tran_current_snapshot。 傳回虛擬資料表，以顯示目前快照集隔離交易啟動時的所有使用中交易。 如果目前的交易使用快照隔離，此函數不會傳回任何資料列。 sys.dm_tran_current_snapshot 類似於 sys.dm_tran_transactions_snapshot，唯一差別在於它只會傳回目前快照集的作用中交易。 如需詳細資訊，請參閱 [sys.dm_tran_current_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-current-snapshot-transact-sql.md)。  
  
##### <a name="performance-counters"></a>效能計數器  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 效能計數器可提供受到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 程序影響的系統效能相關資訊。 下列效能計數器會監視 tempdb、版本存放區以及使用資料列版本設定的交易。 效能計數器包含在 SQLServer:Transactions 效能物件中。  
  
 **Free Space in tempdb (KB)** 。 監視 tempdb 資料庫的可用空間量，以 KB 為單位。 tempdb 要有足夠的可用空間，才能處理支援快照集隔離的版本存放區。  
  
 下列公式提供版本存放區大小的概估。 若為長時間執行的交易，則監視產生速率和清除速率以評估版本存放區的大小上限，可能會有幫助。  
  
 [一般版本存放區的大小] = 2 * [每分鐘產生的版本存放區資料] \* [交易的最長執行時間 (分鐘數)]  
  
 交易的最長執行時間不應包括線上索引組建。 由於這些作業在非常大的資料表上會花很長的時間，線上索引組建會使用不同的版本存放區。 線上索引組建版本存放區的近似大小，等於啟動線上索引組建時資料表中修改的資料量，包括所有索引。  
  
 **Version Store Size (KB)** 。 監視所有版本存放區的大小，以 KB 為單位。 此資訊有助於決定版本存放區的 tempdb 資料庫所需要的空間量。 持續監視這個計數器一段時間，可對 tempdb 所需的其他空間提供有用的評估。  
  
 第 1 課：建立 Windows Azure 儲存體物件`Version Generation rate (KB/s)`。 監視所有版本存放區的版本產生速率 (以每秒 KB 數為單位)。  
  
 第 1 課：建立 Windows Azure 儲存體物件`Version Cleanup rate (KB/s)`。 監視所有版本存放區的版本清除速率 (以每秒 KB 數為單位)。  
  
> [!NOTE]  
> Version Generation rate (KB/s) 和 Version Cleanup rate (KB/s) 的資訊可用來預測 tempdb 的空間需求。  
  
 **Version Store unit count**。 監視版本存放區單元的計數。  
  
 **Version Store unit creation**。 監視自執行個體啟動之後，為了儲存資料列版本而建立之版本存放區單元的總數。  
  
 **Version Store unit truncation**。 監視自執行個體啟動之後，被截斷之版本存放區單元的總數。 當 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 判斷執行使用中交易時不再需要版本存放區單元中所儲存的任何版本資料列時，就會截斷版本存放區單元。  
  
 **Update conflict ratio**。 監視有更新衝突的更新快照集交易與更新快照集交易總數的比例。  
  
 **Longest Transaction Running Time**。 監視使用資料列版本設定的任何交易的最長執行時間，以秒數為單位。 這可用來判斷是否有任何交易執行的時間量不合理。  
  
 **Transactions**。 監視使用中交易的總數。 這不包括系統交易。  
  
 第 1 課：建立 Windows Azure 儲存體物件`Snapshot Transactions`。 監視使用中快照集交易的總數。  
  
 第 1 課：建立 Windows Azure 儲存體物件`Update Snapshot Transactions`。 監視執行更新作業的使用中快照集交易的總數。  
  
 第 1 課：建立 Windows Azure 儲存體物件`NonSnapshot Version Transactions`。 監視產生版本記錄的使用中非快照集交易的總數。  
  
> [!NOTE]  
> Update Snapshot Transactions 和 NonSnapshot Version Transactions 的總和代表參與版本產生的交易總數。 Snapshot Transactions 和 Update Snapshot Transactions 的差異可報告唯讀快照集交易的數目。  
  
### <a name="row-versioning-based-isolation-level-example"></a>資料列版本設定隔離等級範例  
 下列範例將示範快照隔離交易與使用資料列版本設定之讀取認可交易之間的行為差異。  
  
#### <a name="a-working-with-snapshot-isolation"></a>A. 示範快照隔離  
 此範例中，在快照隔離下執行的交易會讀取接著由另一個交易修改的資料。 快照交易不會封鎖另一個交易執行的更新作業，而會繼續從版本控制資料列中讀取資料，忽略資料的修改。 不過，當快照交易嘗試修改意見由另一個交易修改過的資料時，快照交易會產生錯誤且結束。  
  
 在工作階段 1 上：  
  
```sql  
USE AdventureWorks2016;  
GO  
  
-- Enable snapshot isolation on the database.  
ALTER DATABASE AdventureWorks2016  
    SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
  
-- Start a snapshot transaction  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
  
BEGIN TRANSACTION;  
    -- This SELECT statement will return  
    -- 48 vacation hours for the employee.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 在工作階段 2 上：  
  
```sql  
USE AdventureWorks2016;  
GO  
  
-- Start a transaction.  
BEGIN TRANSACTION;  
    -- Subtract a vacation day from employee 4.  
    -- Update is not blocked by session 1 since  
    -- under snapshot isolation shared locks are  
    -- not requested.  
    UPDATE HumanResources.Employee  
        SET VacationHours = VacationHours - 8  
        WHERE BusinessEntityID = 4;  
  
    -- Verify that the employee now has 40 vacation hours.  
    SELECT VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 在工作階段 1 上：  
  
```sql  
    -- Reissue the SELECT statement - this shows  
    -- the employee having 48 vacation hours.  The  
    -- snapshot transaction is still reading data from  
    -- the versioned row.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 在工作階段 2 上：  
  
```sql  
-- Commit the transaction; this commits the data  
-- modification.  
COMMIT TRANSACTION;  
GO  
```  
  
 在工作階段 1 上：  
  
```sql  
    -- Reissue the SELECT statement - this still   
    -- shows the employee having 48 vacation hours  
    -- even after the other transaction has committed  
    -- the data modification.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
  
    -- Because the data has been modified outside of the  
    -- snapshot transaction, any further data changes to   
    -- that data by the snapshot transaction will cause   
    -- the snapshot transaction to fail. This statement   
    -- will generate a 3960 error and the transaction will   
    -- terminate.  
    UPDATE HumanResources.Employee  
        SET SickLeaveHours = SickLeaveHours - 8  
        WHERE BusinessEntityID = 4;  
  
-- Undo the changes to the database from session 1.   
-- This will not undo the change from session 2.  
ROLLBACK TRANSACTION  
GO  
```  
  
#### <a name="b-working-with-read-committed-using-row-versioning"></a>B. 示範使用資料列版本設定的讀取認可  
 在此範例中，使用資料列版本設定的讀取認可交易與另一個交易同時執行。 讀取認可交易的運作方式和快照交易不同。 與快照交易類似的是，讀取認可交易即使在其他交易修改資料後還是會讀取版本控制資料列。 不過，與快照交易不同的是，讀取認可交易將會：  
  
-   在其他交易認可資料變更後，會讀取已修改的資料  
-   可以更新由其他交易修改的資料，但是快照交易無法做到。  
  
 在工作階段 1 上：  
  
```sql  
USE AdventureWorks2016;  -- Or any earlier version of the AdventureWorks database.  
GO  
  
-- Enable READ_COMMITTED_SNAPSHOT on the database.  
-- For this statement to succeed, this session  
-- must be the only connection to the AdventureWorks2016  
-- database.  
ALTER DATABASE AdventureWorks2016  
    SET READ_COMMITTED_SNAPSHOT ON;  
GO  
  
-- Start a read-committed transaction  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
GO  
  
BEGIN TRANSACTION;  
    -- This SELECT statement will return  
    -- 48 vacation hours for the employee.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 在工作階段 2 上：  
  
```sql  
USE AdventureWorks2016;  
GO  
  
-- Start a transaction.  
BEGIN TRANSACTION;  
    -- Subtract a vacation day from employee 4.  
    -- Update is not blocked by session 1 since  
    -- under read-committed using row versioning shared locks are  
    -- not requested.  
    UPDATE HumanResources.Employee  
        SET VacationHours = VacationHours - 8  
        WHERE BusinessEntityID = 4;  
  
    -- Verify that the employee now has 40 vacation hours.  
    SELECT VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 在工作階段 1 上：  
  
```sql  
    -- Reissue the SELECT statement - this still shows  
    -- the employee having 48 vacation hours.  The  
    -- read-committed transaction is still reading data   
    -- from the versioned row and the other transaction   
    -- has not committed the data changes yet.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 在工作階段 2 上：  
  
```sql  
-- Commit the transaction.  
COMMIT TRANSACTION;  
GO  
```  
  
 在工作階段 1 上：  
  
```sql  
    -- Reissue the SELECT statement which now shows the   
    -- employee having 40 vacation hours.  Being   
    -- read-committed, this transaction is reading the   
    -- committed data. This is different from snapshot  
    -- isolation which reads from the versioned row.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
  
    -- This statement, which caused the snapshot transaction   
    -- to fail, will succeed with read-committed using row versioning.  
    UPDATE HumanResources.Employee  
        SET SickLeaveHours = SickLeaveHours - 8  
        WHERE BusinessEntityID = 4;  
  
-- Undo the changes to the database from session 1.   
-- This will not undo the change from session 2.  
ROLLBACK TRANSACTION;  
GO  
```  
  
### <a name="enabling-row-versioning-based-isolation-levels"></a>啟用資料列版本設定式的隔離等級  
 資料庫管理員可藉由在 ALTER DATABASE 陳述式中使用 `READ_COMMITTED_SNAPSHOT` 和 `ALLOW_SNAPSHOT_ISOLATION` 資料庫選項，來控制資料列版本設定的資料庫層級設定。  
  
 當 `READ_COMMITTED_SNAPSHOT` 資料庫選項設定為 ON 時，就會立即啟用用來支援此選項的機制。 設定 READ_COMMITTED_SNAPSHOT 選項時，資料庫中只會允許使用執行 `ALTER DATABASE` 命令的連線。 在 ALTER DATABASE 完成以前，資料庫中不可以有其他開啟的連接。 資料庫不一定要處於單一使用者模式。  
  
 下列 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式會啟用 `READ_COMMITTED_SNAPSHOT`：  
  
```sql  
ALTER DATABASE AdventureWorks2016  
    SET READ_COMMITTED_SNAPSHOT ON;  
```  
  
 當 `ALLOW_SNAPSHOT_ISOLATION` 資料庫選項設定為 ON 時，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]執行個體會等到所有在資料庫中已修改資料的作用中交易完成之後，才會為已修改的資料產生資料列版本。 如果有作用中的修改交易，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 就會將選項的狀態設定為 `PENDING_ON`。 在所有修改交易完成之後，選項的狀態會變更為 ON。 在選項完全成為 ON 之前，使用者無法啟動該資料庫中的快照集交易。 當資料庫管理員將 `ALLOW_SNAPSHOT_ISOLATION` 選項設定為 OFF 時，資料庫就會經歷 PENDING_OFF 狀態。  
  
 下列 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式可啟用 ALLOW_SNAPSHOT_ISOLATION：  
  
```sql  
ALTER DATABASE AdventureWorks2016  
    SET ALLOW_SNAPSHOT_ISOLATION ON;  
```  
  
 下表列出並說明 ALLOW_SNAPSHOT_ISOLATION 選項的狀態。 將 ALTER DATABASE 與 ALLOW_SNAPSHOT_ISOLATION 選項搭配使用，不會影響到目前存取資料庫資料的使用者。  
  
|現行資料庫的快照隔離架構狀態|描述|  
|----------------------------------------------------------------|-----------------|  
|OFF|未啟動快照隔離交易的支援。 不允許任何快照隔離交易。|  
|PENDING_ON|快照隔離交易的支援處於轉換狀態 (從 OFF 到 ON)。 開啟的交易必須完成。<br /><br /> 不允許任何快照隔離交易。|  
|開啟|已啟動快照隔離交易的支援。<br /><br /> 允許快照集交易。|  
|PENDING_OFF|快照隔離交易的支援處於轉換狀態 (從 ON 到 OFF)。<br /><br /> 在此時間之後所啟動的快照集交易，無法存取此資料庫。 更新交易仍需花費成本進行此資料庫中的版本控制。 現有的快照集交易仍可存取此資料庫，而不會產生任何問題。 必須等到所有在資料庫快照隔離狀態為 ON 時，且處於使用中的快照集交易完成之後，PENDING_OFF 狀態才會變成 OFF。|  
  
 使用 `sys.databases` 目錄檢視，可判定兩個資料列版本設定資料庫選項的狀態。  
  
 對使用者資料表的所有更新，以及儲存在 master 與 msdb 中的一些系統資料表，都會產生資料列版本。  
  
 在 master 與 msdb 資料庫中會自動將 `ALLOW_SNAPSHOT_ISOLATION` 選項設定為 ON，且無法停用。  
  
 使用者無法在 master、tempdb 或 msdb 中將 `READ_COMMITTED_SNAPSHOT` 選項設定為 ON。  
  
### <a name="using-row-versioning-based-isolation-levels"></a>使用資料列版本設定式的隔離等級  
 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中永遠會啟用資料列版本設定架構，並且有多個功能會使用此架構。 除了提供資料列版本設定式的隔離等級之外，它也用來支援觸發程序中所做的修改以及 Multiple Active Result Set (MARS) 工作階段中所做的修改，還支援 ONLINE 索引作業的資料讀取。  
  
 資料列版本設定式的隔離等級是在資料庫層級啟用。 從已啟用之資料庫存取物件的應用程式，可以使用下列隔離等級執行查詢：  
  
-   透過將 `READ_COMMITTED_SNAPSHOT` 資料庫選項設為 `ON` ，進而使用資料列版本設定的讀取認可，如下列程式碼範例所示：  
  
    ```sql  
    ALTER DATABASE AdventureWorks2016  
        SET READ_COMMITTED_SNAPSHOT ON;  
    ```  
  
     為資料庫啟用 `READ_COMMITTED_SNAPSHOT` 時，所有在讀取認可隔離等級下執行的查詢都會使用資料列版本設定，這意謂著讀取作業不會封鎖更新作業。  
  
-   將 `ALLOW_SNAPSHOT_ISOLATION` 資料庫選項設定為 `ON` 來隔離快照集，如下列程式碼範例所示：  
  
    ```sql  
    ALTER DATABASE AdventureWorks2016  
        SET ALLOW_SNAPSHOT_ISOLATION ON;  
    ```  
  
     在快照隔離下執行的交易可以存取在資料庫中已針對快照啟用的資料表。 若要存取尚未針對快照啟用的資料表，您必須變更隔離等級。 例如，下列程式碼範例會顯示 `SELECT` 陳述式，該陳述式會在執行快照集交易的同時聯結兩個資料表。 其中一個資料表屬於未啟用快照隔離的資料庫。 當 `SELECT` 陳述式在快照隔離下執行時，將無法順利執行。  
  
    ```sql  
    SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
    BEGIN TRAN  
        SELECT t1.col5, t2.col5  
            FROM Table1 as t1  
            INNER JOIN SecondDB.dbo.Table2 as t2  
                ON t1.col1 = t2.col2;  
    ```  
  
     下列程式碼範例所示的是經過修改的同一個 `SELECT` 陳述式，可將交易隔離等級變更為讀取認可。 由於此項變更，就可以順利執行 `SELECT` 陳述式。  
  
    ```sql  
    SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
    BEGIN TRAN  
        SELECT t1.col5, t2.col5  
            FROM Table1 as t1  
            WITH (READCOMMITTED)  
            INNER JOIN SecondDB.dbo.Table2 as t2  
                ON t1.col1 = t2.col2;  
    ```  
  
#### <a name="limitations-of-transactions-using-row-versioning-based-isolation-levels"></a>使用資料列版本設定式的隔離等級的交易限制  
 使用資料列版本設定式的隔離等級時，請考慮下列限制：  
  
-   無法在 tempdb、msdb 或 master 中啟用 `READ_COMMITTED_SNAPSHOT`。  
-   全域暫存資料表會儲存在 tempdb 中。 存取快照集交易內的全域暫存資料表時，必須符合下列其中一項：  
    -   在 tempdb 中，將 `ALLOW_SNAPSHOT_ISOLATION` 資料庫選項設定為 ON。  
    -   使用隔離提示來變更陳述式的隔離等級。  
-   發生下列情形時，快照集交易會失敗：  
    -   啟動快照集交易之後，且於快照集交易存取資料庫之前，資料庫都是唯讀的。  
    -   如果從多重資料庫存取物件，在快照集交易啟動之後，但在快照集交易存取資料庫之前，會以發生資料庫復原的方式變更資料庫狀態。 例如：資料庫設為 OFFLINE 然後設為 ONLINE、自動關閉及開啟資料庫，或者卸離和附加資料庫。  
-   快照隔離中不支援分散式交易，包括在分散式資料分割資料庫中的查詢。  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不會保留多個版本的系統中繼資料。 資料表上的資料定義語言 (DDL) 陳述式和其他資料庫物件 (索引、檢視、資料類型、預存程序和 Common Language Runtime 函數) 會變更中繼資料。 如果 DDL 陳述式修改了物件，則對快照隔離下的物件進行任何並行參考都會導致快照集交易失敗。 當 READ_COMMITTED_SNAPSHOT 資料庫選項為 ON 時，讀取認可交易就沒有這項限制。  
  
     例如，資料庫管理員會執行下列 `ALTER INDEX` 陳述式。  
  
    ```sql  
    USE AdventureWorks2016;  
    GO  
    ALTER INDEX AK_Employee_LoginID  
        ON HumanResources.Employee REBUILD;  
    GO  
    ```  
  
     執行 `ALTER INDEX` 陳述式時，任何使用中的快照集交易都會出現錯誤 (如果快照集交易嘗試在執行 `HumanResources.Employee` 陳述式之後參考 `ALTER INDEX` 資料表)。 使用資料列版本設定的讀取認可交易將不受影響。  
  
    > [!NOTE]  
    > BULK INSERT 作業可能會造成變更目標資料表中繼資料 (例如，停用條件約束檢查時)。 如果發生這種狀況，存取大量插入資料表的並行快照隔離交易會失敗。  
  
   
## <a name="customizing-locking-and-row-versioning"></a>自訂鎖定及資料列版本設定  
  
### <a name="customizing-the-lock-time-out"></a>自訂鎖定逾時  
 如果當另一個交易已經擁有該資源的衝突鎖定使得 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 執行個體無法將鎖定授與一個交易時，系統就會封鎖第一個交易，以等待現有的鎖定釋出。 依預設，除非嘗試存取資料 (且可能會永遠被封鎖)，否則並沒有強制的逾時期限，且無法在鎖定資源之前測試資源是否已經鎖定。  
  
> [!NOTE]  
> 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，請使用 **sys.dm_os_waiting_tasks** 動態管理檢視來判斷處理序是否已被封鎖，以及其封鎖者是誰。 在舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，請使用 **sp_who** 系統預存程序。  
  
 `LOCK_TIMEOUT` 設定值可讓應用程式設定陳述式等待已封鎖之資源的時間上限。 當陳述式等待的時間超過 LOCK_TIMEOUT 設定值時，會自動取消封鎖的陳述式，然後將錯誤訊息 1222 (`Lock request time-out period exceeded`) 傳回應用程式。 但 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]不會回復或取消包含此陳述式的任何交易。 因此，應用程式必須具有能捕捉錯誤訊息 1222 的錯誤處理常式。 如果應用程式沒有捕捉此錯誤，就會繼續進行而不知道交易中的個別陳述式已取消了，並且因為交易中後面的陳述式可能相依於這個從未執行過的陳述式，此時就會發生錯誤。  
  
 實作會捕捉錯誤訊息 1222 的錯誤處理常式，可讓應用程式處理逾時狀況並採取補救措施，例如自動重新送出先前被封鎖的陳述式，或是回復整筆交易。  
  
 若要判斷目前的 `LOCK_TIMEOUT` 設定，請執行 `@@LOCK_TIMEOUT` 函數：  
  
```sql  
SELECT @@lock_timeout;  
GO  
```  
  
### <a name="customizing-transaction-isolation-level"></a>自訂交易隔離等級  
 READ COMMITTED 是 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的預設隔離等級。 如果應用程式必須在不同隔離等級操作，可以使用下列方法來設定隔離等級：  
  
-   執行 [SET TRANSACTION ISOLATION LEVEL](../t-sql/statements/set-transaction-isolation-level-transact-sql.md) 陳述式。  
-   使用 System.Data.SqlClient 受控命名空間的 ADO.NET 應用程式可以使用 SqlConnection.BeginTransaction 方法來指定 *IsolationLevel* 選項。  
-   使用 ADO 的應用程式可以設定`Autocommit Isolation Levels`屬性。  
-   啟動交易時，使用 OLE DB 的應用程式可以將 *isoLevel* 設定為所需的交易隔離等級來呼叫 ITransactionLocal::StartTransaction。 當在自動認可模式中指定隔離等級時，使用 OLE DB 的應用程式可以將 DBPROPSET_SESSION 屬性 DBPROP_SESS_AUTOCOMMITISOLEVELS 設為所要的交易隔離等級。  
-   使用 ODBC 的應用程式可以使用 SQLSetConnectAttr 來設定 SQL_COPT_SS_TXN_ISOLATION 屬性。  
  
已指定隔離等級時，在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工作階段中，所有查詢和資料操作語言 (DML) 陳述式的鎖定行為都會在此隔離等級運作。 此隔離等級會維持有效，直到工作階段結束或隔離等級設為另一個等級為止。  
  
下列範例會設定 `SERIALIZABLE` 隔離等級：  
  
```sql  
USE AdventureWorks2016;  
GO  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;  
GO  
BEGIN TRANSACTION;  
SELECT BusinessEntityID  
    FROM HumanResources.Employee;  
GO  
```  
  
如果有必要，藉由指定資料表層級的提示，可以覆寫個別查詢或 DML 陳述式的隔離等級。 指定資料表層級的提示不會影響到工作階段的其他陳述式。 建議您只有在絕對必要時，才使用資料表層級的提示來變更預設的行為。  
  
[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 讀取中繼資料時可能必須取得鎖定，即使隔離等級設為讀取資料時不要求共用鎖定。 例如，在讀取未認可之隔離等級執行的交易，讀取資料時不會取得共用鎖定，但在讀取系統目錄檢視時，有時可能會要求鎖定。 這表示，當並行交易正在修改資料表的中繼資料，而讀取未認可的交易同時查詢此資料表時，可能會造成鎖定。  
  
若要判斷目前設定的交易隔離等級，可使用下例所示的 `DBCC USEROPTIONS` 陳述式。 結果集和您系統上的結果集可能不盡相同。  
  
```sql  
USE AdventureWorks2016;  
GO  
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;  
GO  
DBCC USEROPTIONS;  
GO  
```  
  
[!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
```
Set Option                   Value  
---------------------------- -------------------------------------------  
textsize                     2147483647  
language                     us_english  
dateformat                   mdy  
datefirst                    7  
...                          ...  
Isolation level              repeatable read  
 
(14 row(s) affected)   
 
DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```  
  
### <a name="locking-hints"></a>鎖定提示  
 在 SELECT、INSERT、UPDATE 以及 DELETE 陳述式中的個別資料表參考可以指定鎖定提示。 此提示可指定鎖定的類型或是資料表資料所使用之 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 執行個體的資料列版本設定。 需要取得物件的較細緻鎖定類型的控制時可以使用資料表層級的鎖定提示。 這些鎖定提示覆寫 (Override) 工作階段目前的交易隔離等級 (Isolation Level)。  
  
 如需有關特定鎖定提示及其行為的詳細資訊，請參閱[資料表提示 &#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-table.md)。  
  
> [!NOTE]  
> [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 查詢最佳化工具幾乎永遠都會選擇正確的鎖定層級。 建議您只有在必要時才使用資料表層級的鎖定提示來變更預設的鎖定行為。 不允許鎖定層級可能會嚴重影響並行。  
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 在讀取中繼資料時可能必須取得鎖定，即使在處理具有鎖定提示的選取，而該鎖定是防止讀取資料時要求共用鎖定時也是如此。 例如，使用 `NOLOCK` 提示的 `SELECT` 在讀取資料時並不會取得共用鎖定，但在讀取系統目錄檢視時有時會要求鎖定。 這意謂著使用 `NOLOCK` 的 `SELECT` 陳述式有可能被封鎖。  
  
 如下列範例所顯示，如果交易隔離等級設定為 `SERIALIZABLE`，並使用 `NOLOCK` 陳述式來指定資料表層級的鎖定提示 `SELECT` ，則就不採用通常用來維護序列化交易的索引鍵範圍鎖定。  
  
```sql  
USE AdventureWorks2016;  
GO  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;  
GO  
BEGIN TRANSACTION;  
GO  
SELECT JobTitle  
    FROM HumanResources.Employee WITH (NOLOCK);  
GO  
  
-- Get information about the locks held by   
-- the transaction.  
SELECT    
        resource_type,   
        resource_subtype,   
        request_mode  
    FROM sys.dm_tran_locks  
    WHERE request_session_id = @@spid;  
  
-- End the transaction.  
ROLLBACK;  
GO  
```  
  
 所採用的鎖定中，唯一參考 *HumanResources.Employee* 的鎖定是結構描述穩定性 (Sch-S) 鎖定。 這種情況下不保證有序列化能力。  
  
 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中，`ALTER TABLE` 的 `LOCK_ESCALATION` 選項可能不偏好使用資料表鎖定，而會在資料分割資料表上啟用 HoBT 鎖定。 這個選項不是鎖定提示，但是可用來減少鎖定擴大。 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md)。  
  
###  <a name="customizing-locking-for-an-index"></a><a name="Customize"></a> 自訂索引的鎖定  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的動態鎖定策略在大部分的情況下都會自動為查詢選擇最佳的鎖定資料粒度。 除非資料表或索引存取模式都容易理解且維持一致，而且存在待解決的資源競爭問題，否則我們建議您不要覆寫預設鎖定層級 (開啟頁面和資料列鎖定)。 覆寫鎖定層級可能會嚴重妨礙資料表或索引的並行存取。 例如，針對使用者經常存取的大型資料表指定僅限資料表層級鎖定可能會導致效能瓶頸，因為使用者必須等候資料表層級鎖定釋放，才能存取資料表。  
  
 如果存取模式容易理解且維持一致，在少數情況下，不允許頁面或資料列鎖定可能會很有用。 例如，資料庫應用程式使用的查閱資料表以批次處理序每週更新一次。 並行讀取器會存取具有共用 (S) 鎖定的資料表，而且每週批次更新會存取具有獨佔 (X) 鎖定的資料表。 針對資料表關閉頁面和資料列鎖定會允許讀取器透過共用資料表鎖定以並行方式存取資料表，藉以減少整週的鎖定額外負荷。 當批次作業執行時，它就可以有效率地完成更新，因為它會取得獨佔資料表鎖定。  
  
 關閉頁面和資料列鎖定不一定是可接受的作法，因為每週批次更新將會封鎖並行讀取器，使其無法在更新執行時存取資料表。 如果批次作業只變更少數資料列或頁面，您就可以變更鎖定層級來允許資料列或頁面層級鎖定，進而讓其他工作階段讀取資料表而不封鎖。 如果批次作業具有大量更新，取得資料表的獨佔鎖定可能是確保批次作業有效完成的最佳方式。  
  
 有時候，當兩個並行作業取得同一份資料表的資料列鎖定，然後封鎖時，就會發生死結，因為它們都需要鎖定頁面。 不允許資料列鎖定會強制其中一項作業等候，避免發生死結。  
  
 您可以使用 `CREATE INDEX` 和 `ALTER INDEX` 陳述式來設定索引上所使用的鎖定資料粒度。 這個鎖定設定會同時套用至索引頁面和資料表頁面。 此外，還可以使用 `CREATE TABLE` 和 `ALTER TABLE` 陳述式來設定 `PRIMARY KEY` 和 `UNIQUE` 條件約束上的鎖定資料粒度。 為了提供回溯相容性，`sp_indexoption` 系統預存程序也可以設定資料粒度。 若要顯示指定之索引的目前鎖定選項，請使用 `INDEXPROPERTY` 函數。 分頁層級鎖定、資料列層級鎖定、或是分頁層級與資料列層級鎖定的組合可不允許特定索引採用。  
  
|不允許的鎖定|存取索引者|  
|----------------------|-----------------------|  
|分頁層級|資料列層級與資料表層級鎖定|  
|資料列層級|分頁層級與資料表層級鎖定|  
|分頁層級與資料列層級|資料表層級鎖定|  
  
##  <a name="advanced-transaction-information"></a><a name="Advanced"></a> 進階交易資訊  
  
### <a name="nesting-transactions"></a>巢狀交易  
 外顯交易可以是巢狀的。 其主要目的是要支援預存程序中的交易，讓交易可以被已經在交易中的處理序呼叫，或沒有動作的交易內的處理序呼叫。  
  
 下列範例顯示巢狀交易的使用意圖。 *TransProc* 程序會強制執行其交易，而不論執行此程序之任何處理序的交易模式為何。 如果在交易處於作用中時呼叫 *TransProc*，系統將會忽略 *TransProc* 中的大部分巢狀交易，並根據針對外部交易採取的最後動作，來認可或復原其 `INSERT` 陳述式。 如果執行 `TransProc` 的處理序沒有尚未處理的交易，在程序結尾的 `COMMIT TRANSACTION`便會有效地認可 `INSERT` 陳述式。  
  
```sql  
SET QUOTED_IDENTIFIER OFF;  
GO  
SET NOCOUNT OFF;  
GO  
CREATE TABLE TestTrans(Cola INT PRIMARY KEY,  
               Colb CHAR(3) NOT NULL);  
GO  
CREATE PROCEDURE TransProc @PriKey INT, @CharCol CHAR(3) AS  
BEGIN TRANSACTION InProc  
INSERT INTO TestTrans VALUES (@PriKey, @CharCol)  
INSERT INTO TestTrans VALUES (@PriKey + 1, @CharCol)  
COMMIT TRANSACTION InProc;  
GO  
/* Start a transaction and execute TransProc. */  
BEGIN TRANSACTION OutOfProc;  
GO  
EXEC TransProc 1, 'aaa';  
GO  
/* Roll back the outer transaction, this will  
   roll back TransProc's nested transaction. */  
ROLLBACK TRANSACTION OutOfProc;  
GO  
EXECUTE TransProc 3,'bbb';  
GO  
/* The following SELECT statement shows only rows 3 and 4 are   
   still in the table. This indicates that the commit  
   of the inner transaction from the first EXECUTE statement of  
   TransProc was overridden by the subsequent rollback. */  
SELECT * FROM TestTrans;  
GO  
```  
  
 「 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]」會忽略認可內部交易。 交易的認可或復原是依照最外層的交易在最後所執行的動作而定。 若是認可外部交易，則內部的巢狀交易也會被認可。 若是復原外部交易，便會復原所有的內部交易，而不論內部交易是否個別被認可。  
  
 對 `COMMIT TRANSACTION` 或 `COMMIT WORK` 發出的每個呼叫都會套用至最後一個執行的 `BEGIN TRANSACTION`。 如果 `BEGIN TRANSACTION` 陳述式位於巢狀結構中，則 `COMMIT` 陳述式只會套用至最後一個巢狀交易，亦即最內層的交易。 即使巢狀交易中 `COMMIT TRANSACTION` *transaction_name* 陳述式參考外部交易的交易名稱，則仍只會認可最內層的交易。  
  
 `ROLLBACK TRANSACTION` 陳述式的 *transaction_name* 參數如果參考一組具名巢狀交易的內部交易，是不合法的情況。 *transaction_name* 只能參考最外層交易的交易名稱。 如果使用外部交易名稱的 ROLLBACK TRANSACTION *transaction_name* 陳述式，是在一組巢狀交易的任何層級執行，將會回復所有的巢狀交易。 如果是在一組巢狀交易的任何層級執行不含 *transaction_name* 參數的 `ROLLBACK WORK` 或 `ROLLBACK TRANSACTION` 陳述式，則會復原所有巢狀交易，包括最外層的交易。  
  
 `@@TRANCOUNT` 函數會記錄目前的交易巢狀層級。 每個 `BEGIN TRANSACTION` 陳述式會以 1 為單位來遞增 `@@TRANCOUNT`。 每個 `COMMIT TRANSACTION` 或 `COMMIT WORK` 陳述式會以 1 為單位來遞減 `@@TRANCOUNT`。 `ROLLBACK WORK` 或 `ROLLBACK TRANSACTION` 陳述式如果沒有交易名稱，就會復原所有巢狀交易並將 `@@TRANCOUNT` 遞減至 0。 `ROLLBACK TRANSACTION` 如果使用一組巢狀交易中最外層交易的交易名稱，就會復原所有巢狀交易並將 `@@TRANCOUNT` 遞減至 0。 當您不確定您是否已經處於交易中時，請使用 `SELECT @@TRANCOUNT` 來判斷是否為 1 或更大的數字。 如果 `@@TRANCOUNT` 是 0，則表示您未處於交易中。  
  
### <a name="using-bound-sessions"></a>使用繫結工作階段  
 繫結工作階段可簡化相同伺服器上多個工作階段之間動作的協調作業。 繫結工作階段允許兩個以上的工作階段共用相同的交易和鎖定，並且可以使用相同的資料，而不會發生鎖定衝突。 繫結工作階段可以從同一個應用程式中的多個工作階段來建立，也可以從擁有個別工作階段的多個應用程式來建立。  
  
 若要參與繫結工作階段，工作階段需呼叫 `sp_getbindtoken` 或 `srv_getbindtoken` (透過「開放式資料服務」) 來取得繫結 Token。 繫結 Token 是唯一識別每筆繫結交易的字元字串。 然後再將繫結 Token 傳送給其他工作階段，以便與目前的工作階段繫結。 其他工作階段藉由呼叫 **sp_bindsession**，並使用從第一個工作階段接收到的繫結 Token，來繫結到交易。  
  
> [!NOTE]  
> 工作階段必須要有作用中的使用者交易，`sp_getbindtoken` 或 `srv_getbindtoken` 才會成功。  
  
 繫結 Token 必須從建立第一個工作階段的應用程式程式碼，傳送給其他應用程式程式碼，以供後續的應用程式將其工作階段繫結至第一個工作階段。 應用程式無法使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式或 API 函數，來取得另一個處理序所啟動之交易的繫結 Token。 可用來傳送繫結 Token 的部分方法如下：  
  
-   如果工作階段全部都是由相同的應用程式處理序來初始化，則繫結 Token 可以儲存在全域記憶體，或是作為參數傳遞至函數中。  
  
-   如果工作階段是由個別的應用程式處理序建立，則可使用處理序間通訊 (IPC) 來傳送繫結 Token，例如遠端程序呼叫 (RPC) 或動態資料交換 (DDE)。  
  
-   繫結 Token 可以儲存在 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 執行個體的資料表中，而這個資料表可由要繫結至第一個工作階段的處理序所讀取。  
  
 在一組繫結工作階段中，任何時間只能有一個使用中的工作階段。 如果某個工作階段正在執行個體上執行陳述式或等待執行個體的暫止結果，則繫結至此工作階段的其他工作階段都無法存取執行個體，直到目前工作階段完成處理或取消目前陳述式為止。 如果執行個體忙著處理來自另一個繫結工作階段的陳述式，則會發生錯誤，指出交易空間正在使用中，工作階段應稍後重試。  
  
 當您繫結工作階段時，每個工作階段都會保留其隔離等級設定。 使用 SET TRANSACTION ISOLATION LEVEL 來變更一個工作階段的隔離等級設定，並不會影響與它繫結的任何其他工作階段的設定。  
  
#### <a name="types-of-bound-sessions"></a>繫結工作階段的類型  
 繫結工作階段有兩種類型：本機與分散式。  
  
-   **本機繫結工作階段**  
    允許繫結工作階段共用 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]單一執行個體中單一交易的交易空間。  
  
-   **分散式繫結工作階段**  
    允許繫結工作階段跨二或多個執行個體共用同一筆交易，直到使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 認可或回復整筆交易為止。  
  
 分散式繫結工作階段不是由字元字串的繫結 Token 識別，而是由分散式交易識別碼來識別。 如果繫結工作階段涉及本機交易，並使用 `SET REMOTE_PROC_TRANSACTIONS ON` 在遠端伺服器上執行 RPC，MS DTC 就會自動將本機繫結交易升階成分散式繫結交易，並啟動 MS DTC 工作階段。  
  
#### <a name="when-to-use-bound-sessions"></a>使用繫結工作階段的時機  
 在舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中，繫結工作階段主要用於開發擴充預存程序，而這些擴充預存程序必須代表呼叫它們的處理序來執行 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式。 讓呼叫處理序傳入繫結 Token 作為擴充預存程序的一個參數，以允許程序加入呼叫處理序的交易空間之中，因此可整合擴充預存程序與呼叫處理序。  
  
 在 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]中，使用 CLR 撰寫的預存程序比起擴充預存程序，更安全、更具擴充性也更穩定。 CLR 預存程序會使用 **SqlContext** 物件 (而不是 `sp_bindsession`) 來聯結呼叫工作階段的內容。  
  
 繫結工作階段可以用來開發三層式應用程式，其中商務邏輯可加入個別程式，而這些程式可協同處理單筆商務交易。 這些程式必須予以編碼，以便能謹慎協調它們對資料庫的存取。 因為兩個工作階段共用相同的鎖定，所以這兩個程式絕不能同時嘗試修改相同的資料。 在交易過程的任何時候，只能有一個工作階段執行工作，不允許平行執行。 只有在妥善定義的產生點 (例如所有 DML 陳述式都已完成，且也已擷取結果時)，才能於工作階段之間切換交易。  
  
### <a name="coding-efficient-transactions"></a>撰寫有效率的交易  
 儘可能讓交易越短越好相當重要。 開始交易時，資料庫管理系統 (DBMS) 在交易結束之前必須保存許多資源，以保護交易的不可部份完成特性、一致性、隔離和持久性 (ACID) 屬性。 如果已修改資料，必須以獨佔鎖定 (防止其他交易讀取資料列) 保護修改的資料列，並且在認可或回復交易之前必須保持獨佔鎖定。 視交易隔離等級設定而定，`SELECT` 陳述式可能會取得在認可或復原交易之前必須保持的鎖定。 尤其是在擁有許多使用者的系統上，必須盡可能讓交易越短越好，以降低鎖定競爭並行連接之間的資源。 在少數使用者的情況下，沒有效率的長時間執行交易不會造成問題，但在擁有上千個使用者的系統中則無法忍受這種交易。 從 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 開始，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 即可支援延遲的持久交易。 延遲的持久交易不保證持久性。 如需詳細資訊，請參閱[交易持久性](../relational-databases/logs/control-transaction-durability.md)主題。  
  
#### <a name="coding-guidelines"></a><a name="guidelines"></a> 撰寫指引  
 以下為撰寫有效交易的指引：  
  
-   交易期間毋需使用者輸入。  
    啟動交易前，先取得必要的使用者所有輸入內容。 如果交易期間需要額外的使用者輸入，則復原目前的交易，並於使用者提供輸入之後重新啟動交易。 即使使用者立即回應，人類的反應時間還是比電腦的速度慢很多。 交易佔用所有資源的時間非常久，這是造成封鎖問題的潛在因素。 如果使用者並未回應，交易便維持作用中，並鎖定重要的資源直到使用者回應為止，這種情形可能會維持數分鐘，或甚至幾小時。  
  
-   如果位在全部皆可行，不要在瀏覽資料時開啟交易。  
    交易應該等到所有的初步資料分析完成之後再啟動。  
  
-   盡可能讓交易越短越好。  
    在您知道必須進行的修改之後，請啟動交易、執行修改陳述式，然後立即進行認可或回復。 除非必要，否則請勿開啟交易。  
  
-   若要減少封鎖問題，請考慮使用以資料列版本設定為基礎的隔離層級來進行唯讀查詢。  
  
-   善用較低的交易隔離等級。  
    許多應用程式可輕易地撰寫成使用讀取 - 認可式的交易隔離等級。 並非所有交易都需要可序列化的交易隔離等級。  
  
-   善用較低的資料指標並行選項，例如樂觀並行 (Optimistic Concurrency) 選項。  
    在並行更新的可能性較低的系統中，處理偶發的「有人在您讀取資料之後變更過資料」錯誤的額外負荷，可能比讀取時一直鎖定資料列的額外負荷更低。  
  
-   在交易中儘可能存取最少的資料量。  
    這會減少鎖定的資料列數量，因而降低了交易之間的競爭。  
  
#### <a name="avoiding-concurrency-and-resource-problems"></a>避免並行與資源問題  
 若要避免並行與資源的問題，請小心管理隱含交易。 使用隱含交易時，`COMMIT` 或 `ROLLBACK`之後的下一個 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式會自動啟動一個新的交易。 這可能造成交易在應用程式瀏覽資料時，或甚至在需要使用者輸入時被開啟。 保護資料修改所需的最後一筆交易完成之後，請關閉隱含交易，直到交易再度需要保護資料修改為止。 這個程序讓「 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 」在應用程式瀏覽資料及取得使用者輸入時使用自動認可模式。  
  
 此外，啟用快照隔離等級時，雖然新交易不會佔用鎖定，但長時間執行的交易仍然會阻礙從 `tempdb`移除舊版本。  
  
### <a name="managing-long-running-transactions"></a>管理長時間執行的交易  
 *「長時間執行的交易」* (Long-Running Transaction) 是指未及時認可的使用中交易或未及時回復的交易。 例如，如果交易的開始和結束是由使用者控制，長時間執行之交易的常見原因就是使用者開始進行交易，然後在交易等候使用者回應時離開。  
  
 長時間執行的交易可能會對資料庫造成以下幾個嚴重的問題：  
  
-   伺服器執行個體若是在作用中交易已執行許多未認可的修改之後關閉，後續重新啟動之復原階段所花費的時間，可能會遠超過**復原間隔**伺服器組態選項或 `ALTER DATABASE ... SET TARGET_RECOVERY_TIME` 選項所指定的時間。 這些選項分別控制著使用中檢查點與間接檢查點的頻率。 如需有關檢查點類型的詳細資訊，請參閱[資料庫檢查點 &#40;SQL Server&#41;](../relational-databases/logs/database-checkpoints-sql-server.md)。  
  
-   更重要的是，等候中交易儘管產生的記錄可能很少，卻會永久阻礙記錄截斷動作，而導致交易記錄逐漸增大乃至填滿。 一旦交易記錄填滿，資料庫就不再能夠執行任何更新。 如需詳細資訊，請參閱 [SQL Server 交易記錄架構與管理指南](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md), [寫滿交易記錄疑難排解 &#40;SQL Server 錯誤 9002&#41;](../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)及[交易記錄 &#40;SQL Server&#41;](../relational-databases/logs/the-transaction-log-sql-server.md)。  
  
#### <a name="discovering-long-running-transactions"></a>探索長時間執行的交易  
 若要尋找長時間執行的交易，請使用下列其中一種方式：  
  
-   **sys.dm_tran_database_transactions**  
  
    這個動態管理檢視傳回有關資料庫層級之交易的資訊。 對於長時間執行的交易，較重要的資料行包括第一筆記錄檔記錄的時間 (**database_transaction_begin_time**)、交易的目前狀態 (**database_transaction_state**) 和交易記錄之開始記錄的記錄序號 (LSN) (**database_transaction_begin_lsn**)。  
  
    如需詳細資訊，請參閱 [sys.dm_tran_database_transactions &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)。  
  
-   `DBCC OPENTRAN`  
  
    此陳述式可讓您識別交易擁有者的使用者識別碼，如此就可以追蹤交易來源，以便更有條理地終止交易 (進行認可而非回復)。 如需詳細資訊，請參閱 [DBCC OPENTRAN &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)。  
  
#### <a name="stopping-a-transaction"></a>停止交易  
 您可能必須使用 KILL 陳述式。 但是，請小心使用此陳述式，尤其是執行重要處理序時。 如需詳細資訊，請參閱 [KILL &#40;Transact-SQL&#41;](../t-sql/language-elements/kill-transact-sql.md)。  
  
##  <a name="additional-reading"></a><a name="Additional_Reading"></a> 其他閱讀資料   
[資料列版本設定的額外負荷](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2008/03/30/overhead-of-row-versioning.aspx)   
[擴充事件](../relational-databases/extended-events/extended-events.md)   
[sys.dm_tran_locks &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)     
[動態管理檢視與函數 &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)      
[交易相關的動態管理檢視和函數 &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)     
