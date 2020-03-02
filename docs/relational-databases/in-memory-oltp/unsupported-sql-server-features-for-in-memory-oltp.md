---
title: 不支援的功能 - 記憶體內部 OLTP
ms.custom: ''
ms.date: 02/21/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8464f56274308694ada9e5721ae8e0ceb5ed85ed
ms.sourcegitcommit: 867b7c61ecfa5616e553410ba0eac06dbce1fed3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558328"
---
# <a name="unsupported-sql-server-features-for-in-memory-oltp"></a>記憶體內部 OLTP 不支援的 SQL Server 功能
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

本主題探討在使用記憶體最佳化的物件時不受支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 此外，最後段會列出記憶體內部 OLTP 原先不支援，但未來會支援的功能。
  
## <a name="ssnoversion-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體內部 OLTP 不支援的功能  

擁有記憶體最佳化之物件的資料庫不支援下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能，包括記憶體最佳化的資料檔案群組在內。  

  
|不支援的功能|功能描述|  
|-------------------------|-------------------------|  
|記憶體最佳化之資料表的資料壓縮。|使用資料壓縮功能有助於將資料壓縮在資料庫內及縮小資料庫的大小。 如需詳細資訊，請參閱 [Data Compression](../../relational-databases/data-compression/data-compression.md)。|  
|經記憶體最佳化的資料表和雜湊索引，以及非叢集索引的資料分割。|資料分割資料表和索引的資料，已分成可以在資料庫中的多個檔案群組之間分佈的單位。 如需詳細資訊，請參閱＜ [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)＞。|  
| 複寫 | 複寫組態除了訂閱者端對經記憶體最佳化的資料表的異動複寫以外，與參考記憶體最佳化資料表的資料表或檢視表並不相容。<br /><br />若有經記憶體最佳化的檔案群組，即不支援使用 sync_mode='database snapshot' 的複寫。<br /><br />如需詳細資訊，請參閱[複寫至記憶體最佳化資料表訂閱者](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)。|
|鏡像|具有 MEMORY_OPTIMIZED_DATA 檔案群組的資料庫不支援資料庫鏡像。 如需鏡像的詳細資訊，請參閱[資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。|  
|重建記錄檔|具有 MEMORY_OPTIMIZED_DATA 檔案群組的資料庫不支援透過附加或 ALTER DATABASE 重建記錄檔。|  
|連結的伺服器|在以記憶體最佳化資料表形式的相同查詢或交易中，您無法存取連結的伺服器。 如需詳細資訊，請參閱 [連結的伺服器 &#40;Database Engine&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)。|  
|大量記錄|無論資料庫使用何種復原模式，所有在持久性記憶體最佳化的資料表上的作業，一律會完整記錄。|  
|最低限度記錄|記憶體最佳化資料表不支援最低限度記錄。 如需最低限度記錄的詳細資訊，請參閱[交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) 和[大量匯入採用最低限度記錄的必要條件](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)。|  
|變更追蹤|變更追蹤無法在包含記憶體內部 OLTP 物件的資料庫上啟用。 |
| DDL 觸發程序 | 資料庫層級及伺服器層級的 DLL 觸發程序均不受記憶體內部 OLTP 資料表或原生編譯模組支援。 |  
| 異動資料擷取 (CDC) | SQL Server 2017 CU15 和更新版本支援在具有經記憶體最佳化之資料表的資料庫上啟用 CDC。 這僅適用於資料庫和資料庫中的任何磁碟資料表。 在舊版 SQL Server 中，因為內部 CDC 會針對 DROP TABLE 使用 DDL 觸發程序，所以 CDC 無法搭配具有經記憶體最佳化之資料表的資料庫使用。 |  
| Fiber 模式 | 記憶體最佳化資料表不支援 Fiber 模式：<br /><br />若 Fiber 模式處於使用中的狀態，您就無法建立具有記憶體最佳化檔案群組的資料庫，也無法將記憶體最佳化檔案群組新增至現有的資料庫。<br /><br />如果具有記憶體最佳化檔案群組的資料庫已存在，您可以啟用 Fiber 模式。 不過，啟動 Fiber 模式需要重新啟動伺服器。 在此情況下，無法復原具有記憶體最佳化檔案群組的資料庫。 然後您會看到錯誤訊息，建議您停用 Fiber 模式以使用具有記憶體最佳化檔案群組的資料庫。<br /><br />若 Fiber 模式處於使用中的狀態，將無法附加及還原具有記憶體最佳化檔案群組的資料庫。 資料庫會標記為「可疑」。<br /><br />如需詳細資訊，請參閱 [輕量型共用伺服器組態選項](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)。 |  
|Service Broker 的限制|無法從原生編譯的預存程序存取佇列。<br /><br /> 也無法在存取記憶體最佳化的資料表的交易中存取遠端資料庫內的佇列。|  
|訂閱者的複寫|支援在訂閱者端對經記憶體最佳化的資料表進行異動複寫，但是有部分限制。 如需詳細資訊，請參閱 [複寫至記憶體最佳化資料表訂閱者](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)|  
|||

#### <a name="cross-database-queries-and-transcations"></a>跨資料庫的查詢及交易

有一些例外狀況，不支援跨資料庫的交易。 下表描述支援的案例和對應的限制。 (另請參閱 [跨資料庫查詢](../../relational-databases/in-memory-oltp/cross-database-queries.md))。  


|資料庫|允許|描述|  
|---------------|-------------|-----------------|  
| 使用者資料庫、**model** 及 **msdb**。 | 否 | 在大部分情況下，「不」  支援跨資料庫的查詢及交易。<br /><br />任一查詢如使用了經記憶體最佳化的資料表或者原生編譯的預存程序，該查詢即無法存取其他資料庫。 這項限制適用於交易及查詢。<br /><br />系統資料庫 **tempdb** 及 **master** 則是例外。 在這裡，**master** 資料庫可供唯讀存取。 |
| **Resource** 資料庫、**tempdb** | 是 | 在接觸記憶體內部 OLTP 物件的交易中，可以無限制地使用 **Resource** 及 **tempdb** 系統資料庫。
||||

## <a name="scenarios-not-supported"></a>不支援的案例  
  
- 使用來自 CLR 預存程序內的內容連線，存取經記憶體最佳化的資料表。  
  
- 存取記憶體最佳化資料表之查詢上的索引鍵集與動態資料指標。 這些資料指標會降級為靜態，且為唯讀。  
  
- 不支援使用 **MERGE INTO**_target_ (其中 *target* 是經記憶體最佳化的資料表)。
    - 經記憶體最佳化的資料表支援 **MERGE USING** _source_。  
  
- 不支援 ROWVERSION (TIMESTAMP) 資料類型。 如需詳細資訊，請參閱 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)。
  
- 具有 MEMORY_OPTIMIZED_DATA 檔案群組的資料庫不支援自動關閉。  

- 使用者交易內不支援交易式 DLL，例如內部記憶體 OLTP 物件的 CREATE/ALTER/DROP。  
  
- 事件通知。  
  
- 原則式管理 (PBM)。
    - 不會阻止並只記錄 PBM 的模式。 伺服器上存在這類原則時，可能會使記憶體中 OLTP DDL 無法成功執行。 支援視需要和依排程模式。  

- 記憶體內部 OLTP 不支援資料庫的內含項目 ([自主資料庫](../../relational-databases/databases/contained-databases.md))。
    - 支援自主資料庫驗證。 不過，在動態管理檢視 (DMV) 的 **dm_db_uncontained_entities** 中，會將所有內部記憶體 OLTP 物件標記為「中斷內含項目」。

## <a name="recently-added-supports"></a>最近新增的支援

有時 SQL Server 較新版本會新增支援先前不支援的功能。 此區段列出記憶體內部 OLTP 原先不支援，但會在未來支援記憶體內部 OLTP 的功能。

在下表中，「版本」  值 (例如 `(15.x)`) 代表 Transact-SQL 陳述式 `SELECT @@Version;` 所傳回的值。

| 功能名稱 | SQL Server 的版本 | 註解 |
| :----------- | :-------------------- | :------- |
| 資料庫快照集 | 2019 (15.x) | 具有 MEMORY_OPTIMIZED_DATA 檔案群組的資料庫現在支援資料庫快照集。 |
| &nbsp; | &nbsp; | &nbsp; |

## <a name="see-also"></a>另請參閱

- [記憶體中 OLTP 的 SQL Server 支援](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)
