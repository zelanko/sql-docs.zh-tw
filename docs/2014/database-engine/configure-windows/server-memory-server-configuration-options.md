---
title: 伺服器記憶體設定選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Virtual Memory Manager
- max server memory option
- virtual memory [SQL Server]
- VMM
- server memory options [SQL Server]
- servers [SQL Server], memory
- buffer pools [SQL Server]
- min server memory option
- manual memory options [SQL Server]
- memory [SQL Server], servers
ms.assetid: 29ce373e-18f8-46ff-aea6-15bbb10fb9c2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d4f7302da7be80038478c887a01bb32037503fc0
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028695"
---
# <a name="server-memory-configuration-options"></a>伺服器記憶體設定選項
  您可以使用 [最小伺服器記憶體] 和 [最大伺服器記憶體] 這兩個伺服器記憶體選項，針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所使用的 SQL Server 處理序重新設定 SQL Server Memory Manager 所管理的記憶體數量 (以 MB 為單位)。  
  
 [最小伺服器記憶體] 的預設值是 0，而 [最大伺服器記憶體] 的預設值是 2147483647 MB。 根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以根據可用的系統資源，動態變更其記憶體需求。  
  
> [!NOTE]  
> 將 [最大伺服器記憶體] 設定為最小值可能會大幅降低 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 效能，甚至讓伺服器無法啟動。 如果您變更此選項後無法啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請使用 **-f** 啟動選項啟動它，並將 [最大伺服器記憶體] 重設為先前的值。 如需詳細資訊，請參閱 [Database Engine Service Startup Options](database-engine-service-startup-options.md)。  
  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 動態使用記憶體時，它會定期查詢系統以判定可用的記憶體量。 維持這個可用記憶體數量可避免作業系統 (OS) 進行分頁。 如果可用記憶體少於這個數量， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將記憶體釋出給 OS。 如果可用記憶體多於這個數量， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會配置更多記憶體。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只有當工作負載需要更多的記憶體時，它才會增加記憶體。休息中的伺服器不會增加其虛擬位址空間的大小。  
  
 請參閱範例 B，以取得傳回目前使用之記憶體的查詢。 [最大伺服器記憶體] 控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體配置，包括緩衝集區、編譯記憶體、所有快取、qe 記憶體授權、鎖定管理員記憶體及 clr 記憶體 (基本上任何在 **sys.dm_os_memory_clerks** 中找到的記憶體 Clerk 皆是)。 執行緒堆疊的記憶體、記憶體堆積、連結的伺服器提供者 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除外)，以及任何由非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DLL 所配置的記憶體，皆不受伺服器記憶體上限的控制。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用記憶體通知 API **QueryMemoryResourceNotification** ，判定 SQL Server Memory Manager 何時要配置記憶體和釋放記憶體。  
  
 建議允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 動態使用記憶體。不過，您可以手動設定記憶體選項和限制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可存取的記憶體數量。 在您設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的記憶體數量之前，要先決定適當的記憶體設定，請將實體記憶體總數減去 OS 以及任何其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 (以及當電腦不專用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，其他的系統用途) 需要的記憶體。 這個差額是可指派給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的最大記憶體數量。  
  
## <a name="setting-the-memory-options-manually"></a>手動設定記憶體選項  
您可以將伺服器選項 [最小伺服器記憶體] 與 [最大伺服器記憶體] 設定成跨某範圍的記憶體值。 這樣的做法有助於讓系統或資料庫管理員，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體配合同一部電腦上執行的其他應用程式或其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的記憶體需求，一併設定。

> [!NOTE]
> [最小伺服器記憶體] 和 [最大伺服器記憶體] 選項屬於進階選項。 如果您要使用 **sp_configure** 系統預存程序來變更這些設定，只有當 **show advanced options** 設為 1 時，才能變更它們。 這些設定會立即生效，不需要重新啟動伺服器。  
  
<a name="min_server_memory"></a> 您可使用 **min_server_memory** 確保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體管理員，能有最少的記憶體數量可用。 啟動時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會立即配置 [最小伺服器記憶體] 中指定的記憶體數量。 不過，由於用戶端負載使記憶體使用量達到這個值後，除非降低 [最小伺服器記憶體] 的值，否則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法釋出記憶體。 例如，當多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體可以同時存在於相同的主機上時，設定 min_server_memory 參數而非 max_server_memory 可為執行個體保留記憶體。 此外，也需要設定虛擬環境中的 min_server_memory 值，以確保基礎主機的記憶體壓力不會為了得到可接受的效能，而嘗試從客體 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 虛擬機器 (VM) 的緩衝集區，解除超過所需的記憶體。
 
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不保證能夠配置 [最小伺服器記憶體] 中指定的記憶體數量。 如果伺服器的負載從不需要配置 [最小伺服器記憶體] 中指定的記憶體大小，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會以較少的記憶體執行。  
  
<a name="max_server_memory"></a> 您可使用 **max_server_memory** 確保 OS 不會遇到有害的記憶體壓力。 若要設定最大伺服器記憶體設定，請監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序的整體取用量，以判斷記憶體需求。 若要為單一執行個體進行更準確的計算：
 -  從 OS 總記憶體中保留 1GB - 4GB 的記憶體給 OS 本身。
 -  然後減去等於不受 [最大伺服器記憶體] 控制的潛在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體配置，該配置的算法為**堆疊大小 <sup>1</sup> \* 計算得出的最大背景工作執行緒數 <sup>2</sup> + -g 啟動參數 <sup>3</sup>** (若未設定 *-g*，則預設為 256MB)。 餘數即為單一執行個體安裝的 max_server_memory 設定。
 
<sup>1</sup> 如需每個架構之執行緒堆疊大小的資訊，請參閱[記憶體管理架構指南](https://docs.microsoft.com/sql/relational-databases/memory-management-architecture-guide#stacksizes)。

<sup>2</sup> 如需在目前主機中，為指定數量之親和 CPU 而計算出的預設背景工作執行緒數目相關資訊，請參閱如何[設定最大背景工作執行緒伺服器設定選項](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)的文件頁面。

<sup>3</sup> 如需 *-g* 啟動參數的資訊，請參閱[資料庫引擎服務啟動選項](https://docs.microsoft.com/sql/database-engine/configure-windows/database-engine-service-startup-options?view=sql-server-2014)的文件頁面。 僅適用於 32 位元 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 至 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])。

|OS 類型|最**大伺服器記憶體**允許的最小記憶體數量|  
|-------------|----------------------------------------------------------------|  
|32 位元|64 MB|  
|64 位元|128 MB| 

## <a name="how-to-configure-memory-options-using-sql-server-management-studio"></a>如何使用 SQL Server Management Studio 設定記憶體選項  
 您可以使用 [最小伺服器記憶體] 與 [最大伺服器記憶體] 這兩個伺服器記憶體選項，針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體重新設定 SQL Server Memory Manager 所管理的記憶體數量 (以 MB 為單位)。 根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以根據可用的系統資源，動態變更其記憶體需求。  
  
### <a name="procedure-for-configuring-a-fixed-amount-of-memory"></a>設定固定記憶體數量的程序  
 **若要設定固定的記憶體數量:**  
  
1.  在物件總管中，請以滑鼠右鍵按一下伺服器，然後選取 [屬性]。  
  
2.  按一下 **[記憶體]** 節點。  
  
3.  在 [伺服器記憶體選項] 底下，輸入 [最小伺服器記憶體] 和 [最大伺服器記憶體] 所要的數量。  
  
     使用預設值可允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 根據可用的系統資源來動態變更它的記憶體需求。 [最小伺服器記憶體] 的預設值是 0，[最大伺服器記憶體] 的預設值是 2147483647 MB。  
  
## <a name="maximize-data-throughput-for-network-applications"></a>網路應用程式的資料輸送量最大化  
 若要最佳化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的系統記憶體使用量，您應該限制系統用於檔案快取的記憶體數量。 若要限制檔案系統快取，請確定沒有選取 [檔案共用的資料輸送量最大化]。 您可以選取 [記憶體使用最小化] 或 [平衡]，藉以指定最小的檔案系統快取。  
  
#### <a name="to-check-the-current-setting-on-your-operating-system"></a>若要檢查作業系統的現有設定  
  
1.  按一下 [開始]及 [控制台]、按兩下 [網路連線]，然後按兩下 [區域連線]。  
  
2.  在 [一般] 索引標籤上按一下 [內容]，選取 [File and Printer Sharing Microsoft Networks]，然後按一下 [內容]。  
  
3.  如果已選取 [網路應用程式的資料輸送量最大化]，請選擇其他任何選項，按一下 [確定]，然後關閉其餘的對話方塊。  
  
## <a name="lock-pages-in-memory"></a>鎖定記憶體分頁  
 此 Windows 原則決定哪些帳戶可以使用處理序將資料保留在實體記憶體中，以防止系統將資料傳送到磁碟上的虛擬記憶體。 將記憶體分頁到磁碟時，鎖定記憶體分頁可能會讓伺服器保持回應狀態。 當具有執行 sqlservr.exe 許可權的帳戶已被授與 Windows [已鎖定記憶體中的分頁] ( [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] LPIM) 使用者權限時, 在32位和64位 Standard edition 和更新版本的實例中, [SQL Server**鎖定記憶體分頁**] 選項會設定為 ON。 在舊版 SQL Server 中，設定 32 位元 SQL Server 執行個體的 [鎖定分頁] 選項時，需要具有 sqlservr.exe 執行權限的帳戶具有 LPIM 使用者權限，而且 'awe_enabled' 組態選項設定為 ON。  
  
 若要停**用 [鎖定記憶體中**的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]分頁] 選項, 請移除 SQL Server 啟動帳戶的 [鎖定記憶體中的分頁] 使用者權限。  
  
### <a name="to-disable-lock-pages-in-memory"></a>停用鎖定記憶體中的分頁  
 **若要停用 [鎖定記憶體中的分頁] 選項:**  
  
1.  在 **[開始]** 功能表上，按一下 **[執行]** 。 在 [**開啟**] 方塊中`gpedit.msc`, 輸入。  
  
     [群組原則] 對話方塊隨即開啟。  
  
2.  在 [群組原則] 主控台上，依序展開 [電腦組態] 和 [Windows 設定]。  
  
3.  依序展開 [安全性設定]和 [本機原則]。  
  
4.  選取 [使用者權限指派] 資料夾。  
  
     這些原則會顯示在詳細資料窗格中。  
  
5.  在窗格中按兩下 [鎖定記憶體中的分頁]。  
  
6.  在 [本機安全性原則設定] 對話方塊中，選取具有 sqlservr.exe 執行權限的帳戶，然後按一下 [移除]。  
  
## <a name="virtual-memory-manager"></a>虛擬記憶體管理員  
 32 位元作業系統可存取 4 GB 的虛擬位址空間。 其中 2 GB 的虛擬記憶體專供各個處理序使用，而且可供應用程式使用。 另外 2 GB 是保留給作業系統使用的。 所有作業系統版本都包括可提供應用程式存取 3 GB 虛擬位址空間的參數，並將作業系統限制成 1 GB。 如需有關如何使用參數記憶體組態的詳細資訊，請參閱有關 4 GB 微調 (4GT) 的 Windows 文件集。 在 64 位元作業系統上執行 32 位元 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，其使用者可用的虛擬位址空間是完整的 4 GB。  
  
 此位址空間的認可區域是由「Windows 虛擬記憶體管理員 (VMM)」對應到可用的實體記憶體。  
  
 如需有關不同作業系統所支援之實體記憶體數量的詳細資訊，請參閱 Windows 文件集：＜Windows 版本的記憶體限制＞。  
  
 虛擬記憶體系統會允許超額認可實體記憶體，所以虛擬記憶體與實體記憶體的比率可超過 1:1。 因此，大型程式可以在各種實體記憶體組態的電腦上執行。 然而，使用的虛擬記憶體若遠大於所有處理序的平均工作集組合，可能會導致效能降低。  
  
 [最小伺服器記憶體] 和 [最大伺服器記憶體] 選項屬於進階選項。 如果您要使用 **sp_configure** 系統預存程序來變更這些設定，只有當 **show advanced options** 設為 1 時，才能變更它們。 這些設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="running-multiple-instances-of-sql-server"></a>執行 SQL Server 的多個執行個體  
 當您執行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的多個執行個體時，您有三個方式可以用來管理記憶體：  
  
-   使用 [最大伺服器記憶體] 來控制記憶體使用量。 建立每一個執行個體的最大設定值，注意，扣除總額不大於機器的總實體記憶體。 您想要提供與執行個體的預期工作負載或資料庫大小成比例的記憶體給每一個執行個體。 此方式的優點是當新的處理序或執行個體啟動時，立刻有記憶體可用。 缺點是，如果您不是執行所有執行個體，則任何執行中執行個體都不能利用剩餘可用的記憶體。  
  
-   使用 [最小伺服器記憶體] 來控制記憶體使用量。 建立每一個執行個體的最小設定值，使這些最小值的總和小於機器的總實體記憶體 1-2 GB。 同樣地，您可以建立與該執行個體的預期負載成比例的最小值。 此方式的優點是，若沒有同時執行所有執行個體，則執行的執行個體可使用剩餘可用的記憶體。 當電腦上有另一個記憶體密集處理序時，此方法也很有用，因為它可確保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 至少取得合理的記憶體數量。 其缺點是，當新的執行個體 (或任何其他處理序) 啟動時，執行中的執行個體可能需要花一些時間來釋出記憶體，尤其如果它們必須將已修改的頁面寫回其資料庫才能這麼做的話。  
  
-   不執行任何動作 (不建議)。 有呈現工作負載的前幾個執行個體傾向於配置所有記憶體。 閒置執行個體或稍後啟動的執行個體最後可能只剩少量的記憶體可用。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會嘗試在執行個體之間平衡記憶體使用量。 不過，所有執行個體將回應 Windows 記憶體通知訊號，以便調整其記憶體使用量的大小。 Windows 不會平衡具有記憶體通知 API 的應用程式之間的記憶體。 它只提供對系統上記憶體可用性的全域回應。  
  
 您可以變更這些設定，而不必重新啟動執行個體，因此，您可以輕易體驗來尋找使用模式的最佳設定。  
  
## <a name="providing-the-maximum-amount-of-memory-to-sql-server"></a>提供最大的記憶體量給 SQL Server  
  
||32 位元|64 位元|  
|-|-------------|-------------|  
|傳統記憶體|在所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中，處理虛擬位址空間的最大限制：<br /><br /> 2 GB<br /><br /> 使用 **/3gb**開機參數的 3 GB *<br /><br /> 在 WOW64 上為 4 GB\*\*|在所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中，處理虛擬位址空間的最大限制：<br /><br /> 在 x64 架構上為 8 TB|  
  
 * **/3gb** 是作業系統開機參數。 如需詳細資訊，請瀏覽 [MSDN Library](https://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409)。  
  
 \* * WOW64 (windows 64 上的 windows) 是在64位作業系統上執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 32 位的模式。 如需詳細資訊，請瀏覽 [MSDN Library](https://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409)。  
  
## <a name="examples"></a>範例  
  
### <a name="example-a"></a>範例 A  
 下列範例會將 `max server memory` 選項設定為 4 GB：  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'max server memory', 4096;  
GO  
RECONFIGURE;  
GO  
```  
  
### <a name="example-b-determining-current-memory-allocation"></a>範例 B：決定目前的記憶體配置  
 以下查詢會傳回目前配置之記憶體的相關資訊。  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
## <a name="see-also"></a>另請參閱  
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
