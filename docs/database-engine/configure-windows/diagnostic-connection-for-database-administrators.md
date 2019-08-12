---
title: 資料庫管理員的診斷連接 | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- server management [SQL Server], connections
- administrator connections [SQL Server]
- ports [SQL Server], DAC
- DAC
- network connections [SQL Server], dedicated administrator
- diagnostic connections [SQL Server]
- connections [SQL Server], dedicated administrator
- ports [SQL Server]
- dedicated administrator connections [SQL Server]
ms.assetid: 993e0820-17f2-4c43-880c-d38290bf7abc
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ee6c63623cc5b88e0cbb9c4a3edd7a78e6137d77
ms.sourcegitcommit: c70a0e2c053c2583311fcfede6ab5f25df364de0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/31/2019
ms.locfileid: "68670474"
---
# <a name="diagnostic-connection-for-database-administrators"></a>資料庫管理員的診斷連接
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 為系統管理員提供了特殊的診斷連接，可在伺服器的標準連接失效時使用。 這個診斷連接可讓系統管理員存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以執行診斷查詢和排解疑難問題，即使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未回應標準連接要求。  
  
 此專用管理員連接 (DAC) 支援加密以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的其他安全性功能。 DAC 只允許將使用者內容變更為其他管理使用者。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將不斷嘗試以便讓 DAC 順利連接，但是在極端的情況下可能無法成功。  
  
**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
## <a name="connecting-with-dac"></a>連接 DAC  
 依預設，只能從執行於伺服器上的用戶端進行連接。 除非使用 sp_configure 預存程序搭配 [remote admin connections 選項](../../database-engine/configure-windows/remote-admin-connections-server-configuration-option.md)來設定網路連接，否則不允許進行網路連接。  
  
 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員 (sysadmin) 角色的成員可以使用 DAC 進行連接。  
  
 DAC 的存取與支援是使用特殊的系統管理員參數 ( **-A** )，透過**sqlcmd**命令提示字元公用程式來執行。 如需使用 **sqlcmd** 的詳細資訊，請參閱[以指令碼變數使用 sqlcmd](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)。 您也可以在執行個體名稱前面加上 **admin:** 來連線，其格式為 **sqlcmd -S admin:<*執行個體名稱*>** 。 您也可以連線到 **admin:\<執行個體名稱  >** ，以便從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器起始 DAC。  
  
## <a name="restrictions"></a>限制  
 由於 DAC 僅在少數的情況下才會為了診斷伺服器問題而建立，因此這項連接有某些限制：  
  
-   若要保證有足夠的資源可供連接使用，每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體只能有一個 DAC。 若已有作用中的 DAC 連接存在，則所有透過 DAC 建立連接的新要求都會遭到拒絕，並產生錯誤 17810。  
  
-   為了節省資源，除非以追蹤旗標 7806 啟動，否則 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 不會接聽 DAC 通訊埠。  
  
-   DAC 最初會嘗試連接到與登入相關聯的預設資料庫。 連接成功後，您就可以連接到 master 資料庫。 如果預設資料庫離線或是無法使用，連接將會傳回錯誤 4060。 但是，若您使用下列命令來覆寫預設資料庫以連接到 master 資料庫，連接就會成功：  
  
     **sqlcmd -A -d master**  
  
     建議您使用 DAC 連接到 master 資料庫，因為只要啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，就一定可以使用 master。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 禁止以 DAC 執行平行查詢或命令。 例如，若您以 DAC 執行下列其中一項陳述式，就會產生錯誤 3637：  
  
    -   RESTORE  
  
    -   BACKUP  
  
-   只有某些限定的資源必定可透過 DAC 來使用。 請勿使用 DAC 來執行需耗用大量資源的查詢 (例如， 大型資料表上的複雜聯結) 或可能會封鎖的查詢。 如此可防止 DAC 在現有的伺服器問題外衍生出其他問題。 為了避免潛在的封鎖情況，若您必須執行可能會封鎖的查詢，請盡可能在快照隔離等級下執行查詢；否則，請將交易隔離等級設為 READ UNCOMMITTED，並將 LOCK_TIMEOUT 值設為 2000 毫秒之類的短數值。 如此可防止 DAC 工作階段產生封鎖的情形。 但依照 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所處的狀態，DAC 工作階段也可能會遭到閂鎖封鎖。 您可以使用 CTRL-C 來結束 DAC 工作階段，但不一定能成功。 在這種情況下，重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可能是唯一的選擇。  
  
-   為了保證 DAC 連接與疑難排解能順利進行， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會保留有限的資源來處理 DAC 所執行的命令。 通常，這些資源僅足夠用來執行簡單的診斷與疑難排解功能，如下表所示。  
  
 雖然，理論上您可以在 DAC 上執行任何不需要以平行方式執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，但我們還是強烈建議您將使用方式限定在下列診斷與疑難排解命令：  
  
-   基本診斷的查詢動態管理檢視，例如 [sys.dm_tran_locks](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md) 可了解封鎖狀態、[sys.dm_os_memory_cache_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md) 可檢查快取的健全狀態，而 [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) 和 [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) 可了解作用中的工作階段與要求。 請避免使用會耗用大量資源 (例如 [sys.dm_tran_version_store](../../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md) 會掃描完整版本存放區而產生大量 I/O) 或使用複雜聯結的動態管理檢視。 如需效能含意的資訊，請參閱特定 [動態管理檢視](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)的文件集。  
  
-   查詢目錄檢視。  
  
-   基本 DBCC 命令，例如 [DBCC FREEPROCCACHE](../..//t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)、[DBCC FREESYSTEMCACHE](../../t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md)、[DBCC DROPCLEANBUFFERS](../../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md) 及 [DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)。 請勿執行需要大量資源的命令，例如 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)、[DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md) 或 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] KILL *\<spid>* 命令。 根據 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的狀態而定，KILL 命令可能不會每次都成功，這時只能選擇重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 下面是部分一般方針：  
  
    -   藉由查詢 `SELECT * FROM sys.dm_exec_sessions WHERE session_id = <spid>`，來確認是否已確實清除 SPID。 若未傳回資料列，表示已清除工作階段。  
  
    -   若工作階段仍然存在，請執行 `SELECT * FROM sys.dm_os_tasks WHERE session_id = <spid>`查詢，以確認此工作階段上是否有指定的工作。 若您在工作階段上看到工作，很可能表示工作階段正在清除中。 請注意，此作業可能會耗費大量時間，而且可能完全無法成功。  
  
    -   若在與此工作階段相關聯的 sys.dm_os_tasks 中沒有工作存在，但工作階段在執行 KILL 命令後仍處於 sys.dm_exec_sessions 中，則表示您沒有可用的工作者。 請選取目前正在執行的其中一個工作 (列示於 sys.dm_os_tasks 檢視表中而含有 `sessions_id <> NULL`的工作)，然後清除與此工作相關聯的工作階段以釋放工作者。 請注意，終止單一工作階段可能不夠：您可能必須清除多個工作階段。  
  
## <a name="dac-port"></a>DAC 通訊埠  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果在啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 之後有可用或動態指派的 TCP 通訊埠，會在 TCP 通訊埠 1434 上接聽 DAC。 [錯誤記錄檔](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)包含 DAC 接聽時所使用的通訊埠號碼。 依預設，DAC 接聽程式只接受本機通訊埠上的連接。 如需可啟動遠端管理連接的程式碼範例，請參閱 [remote admin connections 伺服器組態選項](../../database-engine/configure-windows/remote-admin-connections-server-configuration-option.md)。  
  
 一旦設定遠端管理連接之後，即會啟用 DAC 接聽程式而不需重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，而且用戶端可以從遠端連接到 DAC。 您可以先在本機使用 DAC 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然後執行 sp_configure 預存程序以接受遠端的連接，藉以啟用 DAC 接聽程式使其可接受遠端連接，即使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未回應仍可執行。  
  
 在叢集組態中，DAC 預設為關閉。 使用者可執行 sp_configure 的 remote admin connection 選項，啟用 DAC 接聽程式以存取遠端連接。 若 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未回應且 DAC 接聽程式未啟用，您可能必須重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以連接 DAC。 因此，建議您在叢集系統上啟用 remote admin connections 組態選項。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在啟動期間動態指定 DAC 通訊埠。 連接到預設執行個體時，DAC 會在連接時避免對 SQL Server Browser 服務使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 解析通訊協定 (SSRP) 要求。 它會先透過 TCP 通訊埠 1434 連接。 若失敗，則會發出 SSRP 呼叫以取得通訊埠。 若 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 並未接聽 SSRP 要求，則連接要求會傳回錯誤。 請參閱錯誤記錄檔，以了解 DAC 接聽時所使用的通訊埠編號。 若 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的組態可接受遠端管理連接，DAC 就必須以明確的通訊埠編號起始：  
  
 **sqlcmd -S tcp:** _\<server>,\<port>_  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔會列出 DAC 的通訊埠編號，依預設為 1434。 若將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為只接受本機 DAC 連接，請利用下列命令使用回送配接器進行連接：  
  
 **sqlcmd -S 127.0.0.1,1434**  
  
> [!TIP]  
>  當搭配 DAC 連接到 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 時，您也必須使用 -d 選項在連接字串中指定資料庫名稱。  
  
## <a name="example"></a>範例  
 在此範例中，系統管理員注意到伺服器 `URAN123` 並未回應，而要診斷問題。 為了進行這項作業，使用者啟動 `sqlcmd` 命令提示字元公用程式，並使用 `URAN123` 來表示 DAC，連接到伺服器 `-A` 。  
  
 `sqlcmd -S URAN123 -U sa -P <xxx> -A`  
  
 此時，系統管理員可執行查詢以診斷問題，並盡可能結束未回應的工作階段。  
  
 連接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的類似範例是使用下列包含 -d 參數的命令來指定資料庫：  
  
 `sqlcmd -S serverName.database.windows.net,1434 -U sa -P <xxx> -d AdventureWorks`  
  
## <a name="related-content"></a>相關內容  
 [以指令碼變數使用 sqlcmd](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)  
 [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md)  
 [DBCC CHECKALLOC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
 [DBCC OPENTRAN &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)  
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
 [交易相關的動態管理檢視和函數 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
 [追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
  

