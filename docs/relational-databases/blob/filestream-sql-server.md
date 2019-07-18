---
title: FILESTREAM (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server]
- FILESTREAM [SQL Server], about
- FILESTREAM [SQL Server], overview
ms.assetid: 9a5a8166-bcbe-4680-916c-26276253eafa
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
manager: craigg
ms.openlocfilehash: 178068ee909369fa8559bdce284364630b7763f2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65094336"
---
# <a name="filestream-sql-server"></a>FILESTREAM (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

FILESTREAM 可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 架構應用程式在檔案系統上儲存非結構化的資料，例如文件和影像。 應用程式可以利用檔案系統的豐富資料流 API 和效能，並同時維護非結構化資料與對應結構化資料之間的交易一致性。  
  
FILESTREAM 會將 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] varbinary(max) **二進位大型物件 (BLOB) 資料作為檔案儲存在檔案系統上，以整合** 與 NTFS 或 ReFS 檔案系統。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式可以插入、更新、查詢、搜尋和備份 FILESTREAM 資料。 Win32 檔案系統介面提供了資料的資料流方式存取。  
  
FILESTREAM 會使用 NT 系統快取來儲存檔案資料。 如此可減少 FILESTREAM 資料可能對 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 效能產生的任何影響。 並不會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 緩衝集區；因此，此記憶體可用於查詢處理。  
  
當您安裝或升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，並不會自動啟用 FILESTREAM。 您必須使用 SQL Server 組態管理員和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來啟用 FILESTREAM。 若要使用 FILESTREAM，您必須建立或修改資料庫，以便包含特殊類型的檔案群組。 然後，請建立或修改資料表，讓它包含具有 FILESTREAM 屬性的 **varbinary(max)** 資料行。 完成這些工作之後，您就可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 Win32 來管理 FILESTREAM 資料。  

## <a name="when-to-use-filestream"></a>使用 FILESTREAM 的時機

在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，BLOB 可以是將資料儲存在資料表中的標準 **varbinary(max)** 資料，或是將資料儲存在檔案系統中的 FILESTREAM **varbinary(max)** 物件。 資料的大小和使用情況可決定您是應該使用資料庫儲存體還是檔案系統儲存體。 如果下列條件成立，您應該考慮使用 FILESTREAM：  

- 平均來說，儲存的物件大於 1 MB。  
- 快速讀取權非常重要。
- 您正在開發將中介層用於應用程式邏輯的應用程式。  

如果是較小的物件，將 **varbinary(max)** BLOB 儲存在資料庫中通常會提供更好的資料流處理效能。  

## <a name="filestream-storage"></a>FILESTREAM 儲存體

FILESTREAM 儲存體會實作為 **varbinary(max)** 資料行，該資料行中的資料會當做 BLOB 儲存在檔案系統上。 BLOB 的大小只受到檔案系統磁碟區大小的限制。 標準 **varbinary(max)** 限制 (2 GB 檔案大小) 不適用於檔案系統中所儲存的 BLOB。  
  
若要指定資料行應該將資料儲存在檔案系統上，請在 **varbinary(max)** 資料行上指定 FILESTREAM 屬性。 如此會讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 將該資料行的所有資料都儲存在檔案系統上，而不是儲存在資料庫檔案中。  
  
FILESTREAM 資料必須儲存在 FILESTREAM 檔案群組中。 FILESTREAM 檔案群組是包含檔案系統目錄 (而非檔案本身) 的特殊檔案群組， 這些檔案系統目錄稱為「資料容器」  。 資料容器是 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 儲存體與檔案系統儲存體之間的介面。 

當您使用 FILESTREAM 儲存體時，請考慮以下事項：  

- 當資料表包含 FILESTREAM 資料行時，每一個資料列都必須有唯一的非 Null 資料列識別碼。  
- 您可以將多個資料容器加入至 FILESTREAM 檔案群組。  
- FILESTREAM 資料容器無法巢狀化。  
- 當您正在使用容錯移轉叢集時，FILESTREAM 檔案群組必須在共用磁碟資源上。  
- FILESTREAM 檔案群組可以在壓縮的磁碟區上。

### <a name="integrated-management"></a>整合式管理

由於 FILESTREAM 會實作為 **varbinary(max)** 資料行，並直接整合到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]中，所以大多數的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具和功能不需要修改 FILESTREAM 資料即可運作。 例如，您可以搭配 FILESTREAM 資料使用所有的備份和復原模型，而且 FILESTREAM 資料會與資料庫中的結構化資料一起備份。 如果您不想要將 FILESTREAM 資料與關聯式資料一起備份，您可以使用部分備份來排除 FILESTREAM 檔案群組。  

### <a name="integrated-security"></a>整合式安全性

在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，系統會維護 FILESTREAM 資料的安全性，就像是維護其他資料的安全性一樣：在資料表或資料行層級上授與權限。 如果使用者具有資料表中 FILESTREAM 資料行的權限，該使用者便可開啟關聯的檔案。  

> [!NOTE]
> FILESTREAM 資料上不支援加密。  

只有執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶所使用的帳戶會被授與 FILESTREAM 容器的權限。 我們建議您不要將資料容器的權限授與其他帳戶。

> [!NOTE]
> SQL 登入不會使用 FILESTREAM 容器。 只有 NTFS 或 ReFS 驗證會使用 FILESTREAM 容器。

## <a name="dual"></a> 使用 Transact-SQL 和檔案系統資料流存取來存取 BLOB 資料

在您將資料儲存在 FILESTREAM 資料行中以後，可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 交易或 Win32 API 來存取檔案。  
  
### <a name="transact-sql-access"></a>Transact-SQL 存取

您可以藉由使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]來插入、更新和刪除 FILESTREAM 資料：  

- 您可以使用插入作業，在 FILESTREAM 欄位中預先填入 null 值、空白值，或是相當簡短的內嵌資料。 但是，將大量的資料當做資料流處理成使用 Win32 介面的檔案時，會比較有效率。  
- 當您更新 FILESTREAM 欄位時，您會修改檔案系統中的基礎 BLOB 資料。 當 FILESTREAM 欄位設定為 NULL 時，與此欄位有關聯的 BLOB 資料會遭到刪除。 您無法使用實作為 UPDATE [!INCLUDE[tsql](../../includes/tsql-md.md)] .**Write() 的**區塊更新來執行資料的部分更新。 
- 當您刪除資料列，或是刪除或截斷包含 FILESTREAM 資料的資料表時，您會刪除檔案系統中的基礎 BLOB 資料。

### <a name="file-system-streaming-access"></a>檔案系統資料流存取

Win32 資料流支援可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交易的內容中運作。 在交易內時，您可以使用 FILESTREAM 函數來取得檔案的邏輯 UNC 檔案系統路徑。 然後，您可使用 OpenSqlFilestream API 取得檔案控制代碼。 之後，此控制代碼可由 Win32 檔案資料流介面 (如 ReadFile() 和 WriteFile()) 所使用，以透過檔案系統來存取及更新檔案。  

由於檔案作業是交易式，所以您無法透過檔案系統來刪除或重新命名 FILESTREAM 檔案。  

**陳述式模型**

FILESTREAM 檔案系統存取會使用檔案的開啟和關閉來建立 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的模型。 當檔案控制代碼開啟時，此陳述式便會開始，而當此控制代碼關閉時，此陳述式就會結束。 例如，當寫入控制代碼關閉時，在資料表上註冊之任何可能的 AFTER 觸發程序便會引發，就像是 UPDATE 陳述式已完成一樣。

**儲存體命名空間**

在 FILESTREAM 中， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會控制 BLOB 實體檔案系統命名空間。 有一個新的內建函數 [PathName](../../relational-databases/system-functions/pathname-transact-sql.md)提供了對應至資料表內每一個 FILESTREAM 資料格之 BLOB 的邏輯 UNC 路徑。 應用程式會使用此邏輯路徑來取得 Win32 控制代碼，並在 BLOB 資料上運作 (透過一般 Win32 檔案系統介面)。 如果 FILESTREAM 資料行的值為 NULL，此函數就會傳回 NULL。  

**交易檔案系統存取**

有一個新的內建函數 [GET_FILESTREAM_TRANSACTION_CONTEXT()](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md)提供了一個 Token，它代表與工作階段有關聯的目前交易。 此交易必須已經開始，而且尚未中止或認可。 應用程式會藉由取得 Token，將 FILESTREAM 檔案系統資料流作業與開始的交易繫結。 如果沒有任何明確開始的交易，此函數就會傳回 NULL。  

在認可或中止此交易之前，所有的檔案控制代碼都必須先關閉。 如果有控制代碼在交易範圍之外仍然為開啟狀態，針對此控制代碼的其他讀取將會造成失敗；對此控制代碼的其他寫入將會成功，因為實際資料將不會寫入磁碟中。 同樣地，如果關閉了 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的資料庫或執行個體，則所有開啟的控制代碼都將會失效。  

**交易持久性**

使用 FILESTREAM 時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會在交易認可之後確保從檔案系統資料流存取修改之 FILESTREAM BLOB 資料的交易持續性。  

**隔離語意**

隔離語意受到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 交易隔離等級的管制。 讀取認可的隔離等級支援 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和檔案系統存取。 可重複的讀取作業以及可序列化和快照集隔離均受到支援。 中途讀取則不受到支援。  

檔案系統存取的開啟作業不會等候任何鎖定。 如果開啟作業因為交易隔離而無法存取資料，開啟作業就會立即失敗。 如果開啟作業因為隔離違規而無法繼續，則資料流 API 呼叫會因為 ERROR_SHARING_VIOLATION 而失敗。  

若要允許進行部分更新，應用程式可以發出裝置 FS 控制項 (FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT)，以便將舊的內容提取到開啟之控制代碼所參考的檔案。 如此將會觸發伺服器端的舊內容複本。 為了在處理極大型的檔案時取得更好的應用程式效能及避免可能的逾時，我們建議您使用非同步 I/O。  

如果在寫入此控制代碼之後發出 FSCTL，則最後一個寫入作業將會保存下來，而之前對此控制代碼的寫入將會遺失。

**檔案系統 API 和支援的隔離等級**

當檔案系統 API 由於隔離違規而無法開啟檔案時，系統就會傳回 ERROR_SHARING_VIOLATION 例外狀況。 當兩筆交易嘗試存取相同的檔案時，就會發生這種隔離違規。 存取作業的結果主要取決於用來開啟檔案的模式，以及執行交易的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 下表概述了兩筆存取相同檔案之交易的可能結果。

|交易 1|交易 2|在 SQL Server 2008 上的結果|在 SQL Server 2008 R2 和更新版本上的結果|  
|-------------------|-------------------|--------------------------------|------------------------------------------------------|  
|開啟以便讀取。|開啟以便讀取。|兩筆交易都成功。|兩筆交易都成功。|  
|開啟以便讀取。|開啟以便寫入。|兩筆交易都成功。 交易 2 底下的寫入作業不會影響在交易 1 中執行的讀取作業。|兩筆交易都成功。 交易 2 底下的寫入作業不會影響在交易 1 中執行的讀取作業。|  
|開啟以便寫入。|開啟以便讀取。|交易 2 的開啟作業失敗，並傳回 ERROR_SHARING_VIOLATION 例外狀況。|兩筆交易都成功。|  
|開啟以便寫入。|開啟以便寫入。|交易 2 的開啟作業失敗，並傳回 ERROR_SHARING_VIOLATION 例外狀況。|交易 2 的開啟作業失敗，並傳回 ERROR_SHARING_VIOLATION 例外狀況。|  
|開啟以便讀取。|開啟以便進行 SELECT。|兩筆交易都成功。|兩筆交易都成功。|  
|開啟以便讀取。|開啟以便進行 UPDATE 或 DELETE。|兩筆交易都成功。 交易 2 底下的寫入作業不會影響在交易 1 中執行的讀取作業。|兩筆交易都成功。 交易 2 底下的寫入作業不會影響在交易 1 中執行的讀取作業。|  
|開啟以便寫入。|開啟以便進行 SELECT。|交易 2 會封鎖直到交易 1 認可或結束交易，或者交易鎖定逾時為止。|兩筆交易都成功。|  
|開啟以便寫入。|開啟以便進行 UPDATE 或 DELETE。|交易 2 會封鎖直到交易 1 認可或結束交易，或者交易鎖定逾時為止。|交易 2 會封鎖直到交易 1 認可或結束交易，或者交易鎖定逾時為止。|  
|開啟以便進行 SELECT。|開啟以便讀取。|兩筆交易都成功。|兩筆交易都成功。|  
|開啟以便進行 SELECT。|開啟以便寫入。|兩筆交易都成功。 交易 2 底下的寫入作業不會影響交易 1。|兩筆交易都成功。 交易 2 底下的寫入作業不會影響交易 1。|  
|開啟以便進行 UPDATE 或 DELETE。|開啟以便讀取。|交易 2 的開啟作業失敗，並傳回 ERROR_SHARING_VIOLATION 例外狀況。|兩筆交易都成功。|  
|開啟以便進行 UPDATE 或 DELETE。|開啟以便寫入。|交易 2 的開啟作業失敗，並傳回 ERROR_SHARING_VIOLATION 例外狀況。|交易 2 的開啟作業失敗，並傳回 ERROR_SHARING_VIOLATION 例外狀況。|  
|開啟以便進行可重複讀取的 SELECT。|開啟以便讀取。|兩筆交易都成功。|兩筆交易都成功。|  
|開啟以便進行可重複讀取的 SELECT。|開啟以便寫入。|交易 2 的開啟作業失敗，並傳回 ERROR_SHARING_VIOLATION 例外狀況。|交易 2 的開啟作業失敗，並傳回 ERROR_SHARING_VIOLATION 例外狀況。|

**從遠端用戶端寫出**

遠端檔案系統對 FILESTREAM 資料的存取，是透過伺服器訊息區塊 (SMB) 通訊協定來啟用。 如果用戶端在遠端，則用戶端不會快取任何寫入作業。 寫入作業一定會傳送給伺服器， 資料可以在伺服器端快取。 我們建議您將在遠端用戶端上執行的應用程式合併小型寫入作業，以便使用較多的資料來減少寫入作業。  

使用 FILESTREAM 控制代碼來建立記憶體對應檢視 (記憶體對應 I/O) 不受到支援。 如果將記憶體對應用於 FILESTREAM 資料， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 將無法保證資料的一致性與持續性或是資料庫的完整性。  

## <a name="related-tasks"></a>相關工作

[啟用及設定 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
[建立啟用 FILESTREAM 的資料庫](../../relational-databases/blob/create-a-filestream-enabled-database.md)  
[建立儲存 FILESTREAM 資料的資料表](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md)  
[使用 Transact-SQL 存取 FILESTREAM 資料](../../relational-databases/blob/access-filestream-data-with-transact-sql.md) [建立 FILESTREAM 資料的用戶端應用程式](../../relational-databases/blob/create-client-applications-for-filestream-data.md)  
[使用 OpenSqlFilestream 存取 FILESTREAM 資料](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
[對 FILESTREAM 資料進行部分更新](../../relational-databases/blob/make-partial-updates-to-filestream-data.md)  
[避免與 FILESTREAM 應用程式中的資料庫作業相衝突](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)  
[移動啟用 FILESTREAM 功能的資料庫](../../relational-databases/blob/move-a-filestream-enabled-database.md)  
[設定容錯移轉叢集上的 FILESTREAM](../../relational-databases/blob/set-up-filestream-on-a-failover-cluster.md)  
[為 FILESTREAM 存取設定防火牆](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)

## <a name="related-content"></a>相關內容

[FILESTREAM 與其他 SQL Server 功能的相容性](../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)
<br>[Filestream 及 FileTable 動態管理檢視 (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 和 FileTable 目錄檢視 (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[Filestream 和 FileTable 系統預存程序 (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)

