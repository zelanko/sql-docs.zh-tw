---
title: "記憶體管理架構指南 | Microsoft Docs"
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- guide, memory management architecture
- memory management architecture guide
ms.assetid: 7b0d0988-a3d8-4c25-a276-c1bdba80d6d5
caps.latest.revision: "6"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: db2d067b9daaf0ca015e8069c9e01cab783cfeb7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="memory-management-architecture-guide"></a>記憶體管理架構指南
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

## <a name="memory-architecture"></a>記憶體架構

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會視需要動態地取得和釋放記憶體。 雖然有指定記憶體的選項可供選擇而且在某些環境下也是必要的，但是系統管理員通常不需要指定應配置多少記憶體給 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。

所有資料庫軟體的主要設計目的之一，便是將磁碟 I/O 最小化，因為磁碟的讀取和寫入，是電腦上最需要用到大量資源的作業之一。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會在記憶體中建立緩衝集區，以保存從資料庫讀取的分頁。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的大部分程式碼，主要是用來最小化磁碟和緩衝集區之間實體讀取和寫入的次數。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 嘗試在兩個目標之間取得平衡：

* 避免緩衝集區過大，造成整個系統的記憶體不足。
* 最大化緩衝集區的大小以最小化資料庫檔案的實體 I/O。


> [!NOTE]
> 在工作負載極高的系統上，某些需要大量記憶體來執行的大型查詢因為無法取得要求的最少記憶體，而在等候記憶體資源時發生逾時錯誤。 若要解決這個問題，請增加 [查詢等候選項](../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md)。 如果是平行查詢，請考慮減少 [平行處理原則的最大程度選項](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。
 
> [!NOTE]
> 在記憶體負載極高的系統中，若在查詢計畫中使用合併聯結、排序與點陣圖的查詢，當查詢無法取得點陣圖所需的最低記憶體時，會卸除點陣圖。 這樣會影響查詢效能，且若排序處理序無法放入記憶體中，它會增加 tempdb 資料庫中工作資料表的使用數目，導致 tempdb 成長。 若要解決此問題，請新增記憶體或微調查詢以使用不同與更快的查詢計畫。
 
### <a name="providing-the-maximum-amount-of-memory-to-includessnoversionincludesssnoversion-mdmd"></a>提供記憶體數量上限給 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

透過使用 AWE 與 [鎖定記憶體中的分頁] 權限，您可以為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Database Engine 提供下列記憶體數量。 (下表中的欄位包含已不再提供的 32 位元版本。)

| |32 位元 <sup>1</sup> |64 位元
|-------|-------|-------| 
|傳統記憶體 |所有的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 處理序虛擬位址空間的最大限制： <br>- 2 GB<br>- 使用 /3gb 開機參數時為 3 GB <sup>2</sup> <br>- 在 WOW64 上為 4 GB <sup>3</sup> |所有的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 處理序虛擬位址空間的最大限制： <br>- 使用 IA64 架構時為 7 TB (IA64 不支援 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 和以上版本)<br>- 使用 x64 架構時為作業系統最大值 <sup>4</sup>
|AWE 機制 (允許 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在 32 位元平台上超過處理虛擬位址空間的限制。) |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard、Enterprise 與 Developer 版本：緩衝集區最多可存取 64 GB 的記憶體。|不適用 <sup>5</sup> |
|鎖定記憶體中的分頁作業系統 (OS) 權限 (允許鎖定實體記憶體，以防止鎖定記憶體的 OS 分頁)。<sup>6</sup> |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard、Enterprise 與 Developer 版本：[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 處理序使用 AWE 機制所需。 透過 AWE 機制配置的記憶體無法分頁。 <br> 授與此權限但未啟用 AWE 對伺服器將沒有作用。 |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 與 Developer 版本：建議使用，以避免作業系統分頁。 視工作負載而定，可以改善效能。 可存取的記憶體量類似於傳統記憶體案例。 |

<sup>1</sup> 從 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]開始不提供 32 位元版本。  
<sup>2</sup> /3gb 是作業系統開機參數。 如需詳細資訊，請瀏覽 MSDN Library。  
<sup>3</sup> WOW64 (Windows 64 上的 Windows) 是 32 位元的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在 64 位元作業系統上執行的模式。  
<sup>4</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard Edition 最多支援 128 GB。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition 支援作業系統最大值的上限。  
<sup>5</sup> 請注意，sp_configure awe enabled 選項會出現在 64 位元的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上，但會遭到忽略。    
<sup>6</sup> 如果(在具有 AWE 支援的 32 位元上或是本身的 64 位元上) 授與鎖定記憶體中的分頁權限 (LPIM)，我們建議另外設定最大伺服器記憶體。

> [!NOTE]
> 舊版的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以在 32 位元作業系統上執行。 在 32 位元作業系統上存取超過 4 GB 的記憶體會需要 Address Windowing Extensions (AWE) 來管理記憶體。 若 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 是在 64 位元作業系統上執行，就沒有這項需要。 如需 AWE 的詳細資訊，請參閱 [2008 文件中的](https://msdn.microsoft.com/library/ms189334) 處理序位址空間 [及](https://msdn.microsoft.com/library/ms191481) 管理大型資料庫的記憶體 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。   


## <a name="dynamic-memory-management"></a>動態記憶體管理

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Database Engine 的預設記憶體管理行為是以不造成系統發生記憶體短缺為前提，盡可能取得所需的記憶體。 Database Engine 會使用 Microsoft Windows 的「記憶體通知 API」來達成此目的。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的虛擬位址空間可分成兩個不同的區域：緩衝集區所佔用的空間與其餘的空間。 如果已啟用 AWE 機制，緩衝即區可能是位於 AWE 對應記憶體中，能為資料庫頁面提供額外的空間。 

緩衝集區可做為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的主要記憶體配置來源。 存在於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 處理序內部，且不會留意到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 記憶體管理機能的外部元件 (如 COM 物件)，會使用緩衝集區所佔用之虛擬位址空間以外的記憶體。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 啟動後，會根據系統上的參數量 (如實體記憶體量)、伺服器執行緒數量和許多的啟動參數，計算緩衝集區的虛擬位址空間的大小。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會為緩衝集區保留計算所得的處理序虛擬位址空間量，但它只會取得 (認可) 目前負載所需的實體記憶體數量。

該執行個體接著會繼續視需要取得記憶體，來支援工作負載。 當有更多使用者連接和執行查詢時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會依需要取得其他實體記憶體。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體會持續取得實體記憶體，直到達到它的最大伺服器記憶體配置目標，或直到 Windows 指出已無可用記憶體；當擁有的記憶體多於最小伺服器記憶體設定，且 Windows 指出可用記憶體短缺時，它就會釋出記憶體。

當其他應用程式開始在執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體的電腦上執行時，它們會消耗記憶體，並使可用實體記憶體的數量掉到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 目標以下。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體會調整它的記憶體耗用量。 如果其他應用程式停止而有更多記憶體可供使用， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體就會增加其記憶體配置的大小。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 每秒都可釋放及取得數 MB 的記憶體，使它能隨記憶體配置的變更快速調整。


## <a name="effects-of-min-and-max-server-memory"></a>最小與最大伺服器記憶體的作用

最小伺服器記憶體和最大伺服器記憶體組態選項會建立 Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Database Engine 之緩衝集區所使用的記憶體數量上限與下限。 緩衝集區不會立即取得最小伺服器記憶體中指定的記憶體數量。 緩衝集區只會以初始化所需的記憶體啟動。 當 Database Engine 的工作負載增加時，它會持續取得支援工作負載所需的記憶體。 除非緩衝集區達到最小伺服器記憶體中指定的數量，否則它不會釋放取得的任何記憶體。 一旦達到最小伺服器記憶體，緩衝集區便會使用標準演算法來視需要取得及釋放記憶體。 唯一的差別在於緩衝集區絕不會將其記憶體配置降到最小伺服器記憶體中指定的數量以下，也絕不會取得比最大伺服器記憶體中指定的數量還多的記憶體。

> [!NOTE]
> 做為處理序的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，需要比最大伺服器記憶體選項所指定還多的記憶體。 內部和外部元件都可以在緩衝集區之外配置記憶體 ，這會取用其他記憶體，但是配置給緩衝集區的記憶體通常代表 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]所取用之記憶體的最大部份。


Database Engine 取得的記憶體數量完全是依據執行個體的工作負載而定。 如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體不需處理許多要求，可能永遠也不會達到最小伺服器記憶體。

如果針對最小伺服器記憶體和最大伺服器記憶體指定相同的值，則一旦配置給 Database Engine 的記憶體達到該值，Database Engine 就會停止動態釋放和取得緩衝集區的記憶體。

如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體正在電腦上執行，而且電腦上有其他應用程式頻繁地停止或啟動，則 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體配置和取消配置記憶體，可能會延遲其他應用程式啟動的時間。 此外，如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 是在單一電腦上執行的數個伺服器應用程式之一，系統管理員可能需要控制配置給 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的記憶體數量。 在這些情況下，您可以使用最小伺服器記憶體和最大伺服器記憶體選項，來控制 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以使用的記憶體數量。 如需詳細資訊，請參閱 [伺服器記憶體組態選項](../database-engine/configure-windows/server-memory-server-configuration-options.md)。

最小伺服器記憶體與最大伺服器記憶體選項是以 MB 指定。

## <a name="memory-used-by-includessnoversionincludesssnoversion-mdmd-objects-specifications"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件所使用的記憶體規格

下列清單將描述 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中不同物件所使用的記憶體大約數量。 所列的數量為估計值，且可能視環境及建立物件的方式而有所不同。

* 鎖定：64 個位元組 + 每個擁有者 32 個位元組   
* 使用者連接：大約是 (3* *network_packet_size + 94 kb)    

網路封包大小是表格式資料配置 (TDS) 封包的大小，用於應用程式和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Database Engine 之間的通訊。 預設封包大小是 4 KB，由 network packet size 組態選項所控制。

啟用多個使用中結果集 (MARS) 時，使用者連接大約是 (3 + 3 * num_logical_connections) * network_packet_size + 94 KB

## <a name="buffer-management"></a>緩衝區管理

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫的主要用途是為了儲存和擷取資料，因此大量磁碟 I/O 是 Database Engine 的核心特性。 此外，因為磁碟 I/O 作業會秏用許多資源，而且相對上需要較長的時間才能完成，所以 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 非常著重提高 I/O 的效率。 緩衝區管理是達成這種效率的重要元件。 緩衝區管理元件包含兩種機制：可存取和更新資料庫頁面的緩衝區管理員，以及可減少資料庫檔案 I/O 的緩衝快取 (也稱為「緩衝集區」(Buffer Pool))。 

### <a name="how-buffer-management-works"></a>緩衝區管理如何運作

緩衝區是 8 KB 的記憶體頁面，大小與資料或索引頁面相同。 因此，緩衝區快取也分成 8 KB 的頁面。 緩衝區管理員管理從資料庫磁碟檔案將資料或索引頁面讀取到緩衝快取中，以及將修改後頁面重新寫入磁碟的功能。 頁面會保留在緩衝區快取中，直到緩衝區管理員需要緩衝區來讀取更多資料為止。 只有資料修改後，才會重新寫入磁碟。 在重新寫入磁碟之前，可以多次修改緩衝區快取中的資料。 如需詳細資訊，請參閱 [讀取分頁](../relational-databases/reading-pages.md) 和 [寫入分頁](../relational-databases/writing-pages.md)。

當 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 啟動時，會根據數種參數 (例如，系統上的實體記憶體數量、設定的最大伺服器執行緒數量，以及各種啟動參數)，計算緩衝區快取的虛擬位址空間大小。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會為緩衝區快取保留此計算所得的處理序虛擬位址空間量 (稱為記憶體目標)，但它只會取得 (認可) 目前負載所需的實體記憶體量。 您可以在 **sys.dm_os_sys_info** 目錄檢視中查詢 **bpool_commit_target** 和 [bpool_committed](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) 資料行，以分別傳回保留為記憶體目標的頁數和緩衝區快取中目前認可的頁數。

在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 啟動時與緩衝區快取取得其記憶體目標時當中的間隔稱為「擴置」(Ramp-up)。 在這段期間，讀取要求會依需要填滿緩衝區。 例如，單頁讀取要求會填滿單一緩衝區頁面。 這表示擴置是依據用戶端要求的數目和類型而定。 擴置會將單頁讀取要求轉換成對齊的八頁要求來加速。 這可讓擴置加快完成，特別是在具有大量記憶體的電腦上。

因為緩衝區管理員要使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 處理序中大部分的記憶體，所以會與記憶體管理員合作以允許其他元件使用其緩衝區。 緩衝區管理員主要與下列元件進行互動：

* 資源管理員，以控制整個記憶體的使用量，而在 32 位元平台中，還要控制位址空間使用量。  
* 資料庫管理員和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 作業系統 (SQLOS)，以進行低階檔案 I/O 作業。  
* 記錄檔管理員，以處理預寫記錄檔。  

### <a name="supported-features"></a>支援的功能

緩衝區管理員支援下列功能：

* 緩衝區管理員為非統一記憶體存取 (NUMA) 感知。 緩衝快取頁面會分散到硬體 NUMA 節點，這可讓執行緒存取本機 NUMA 節點上配置的緩衝區頁面，而不是從外部記憶體中存取。 
* 緩衝區管理員支援熱新增記憶體 (Hot Add Memory)，讓使用者不需要重新啟動伺服器即可增加實體記憶體。 
* 緩衝區管理員在 64 位元平台上支援大型分頁。 Windows 的不同版本各有特定的頁面大小。 
* 緩衝區管理員提供可透過動態管理檢視公開的額外診斷資訊。 您可以使用這些檢視來監視 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]特定的各種作業系統資源。 例如，您可以使用 sys.dm_os_buffer_descriptors 檢視來監視緩衝快取中的頁面。   

### <a name="disk-io"></a>磁碟 I/O
緩衝區管理員僅針對資料庫執行讀取和寫入。 其他檔案及資料庫作業，如開啟、關閉、擴充和壓縮，都是由資料庫管理員和檔案管理員元件來執行。 

緩衝區管理員執行的磁碟 I/O 作業具有下列特性：

* 所有的 I/O 都是以非同步的方式進行，這可讓呼叫執行緒繼續進行處理，而 I/O 作業則同時於背景中執行。
* 除非使用了關連 I/O 選項，否則所有的 I/O 都是在呼叫執行緒中發出。 affinity I/O mask 選項會將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 磁碟 I/O 繫結到指定的 CPU 子集。 在高階的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上交易處理 (OLTP) 環境中，此延伸模組可強化 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行緒發行 I/O 的效能。
* 多頁 I/O 是透過散佈 - 收集 I/O 來完成，可讓資料轉入或轉出非連續的記憶體區域。 這表示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以快速填滿或排清緩衝快取，同時還能避免多個實體 I/O 要求。 

#### <a name="long-io-requests"></a>長 I/O 要求  
緩衝區管理員會報告任何至少持續 15 秒仍未處理的 I/O 要求。 這樣可以協助系統管理員區別 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 問題和 I/O 子系統問題。 報告錯誤訊息 833，並會出現在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 錯誤記錄檔中，如下：

`` 
SQL Server has encountered %d occurrence(s) of I/O requests taking longer than %d seconds to complete on file [%ls] in database [%ls] (%d). The OS file handle is 0x%p. The offset of the latest long I/O is: %#016I64x.
`` 

長 I/O 可能是讀取或寫入動作；不會在目前的訊息中指出。 長 I/O 訊息是警告，而非錯誤。 這些訊息並不表示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]有問題。 報告這些訊息的目的是在協助系統管理員更快找到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 回應時間遲緩的原因，並區別 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]控制範圍之外的問題。 因此，不需要對它們採取任何動作，但是系統管理員應該調查 I/O 要求為何會用那麼久的時間，以及這段時間是否合理。

#### <a name="causes-of-long-io-requests"></a>長 I/O 要求的原因  
長 I/O 訊息可能指出 I/O 已遭永久封鎖而永遠無法完成 (稱為遺失 I/O)，或者只是尚未完成。 雖然遺失 I/O 經常導致閂鎖逾時，但也無法從訊息中辨別實際狀況是什麼。

長 I/O 通常表示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工作負載對磁碟子系統而言有些過重。 出現下列情形時，可能表示磁碟子系統已經不勝負荷：

* 在繁重的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工作負載期間，錯誤記錄出現多則長 I/O 訊息。
* Perfmon 計數器顯示長時間的磁碟延遲、冗長的磁碟佇列或沒有磁碟閒置時間。  

長 I/O 也可能是 I/O 路徑中的元件 (例如，驅動程式、控制器或韌體) 所造成，因為這個元件持續延後對舊有 I/O 要求的服務，而優先服務較接近磁碟讀寫頭目前位置的較新要求。 一般以最接近讀寫頭目前位置的要求為優先處理的技術即稱為「電梯式尋軌」(Elevator Seeking)。 這就很難用 Windows 系統監視器 (PERFMON.EXE) 工具來證實，因為多數情況下都應該立即服務 I/O 作業才對。 執行大量循序 I/O 的工作負載，如備份與還原、資料表掃描、排序、建立索引、大量載入以及清空檔案等作業，會使長 I/O 要求的情況惡化。

顯然與上述任何情況無關的孤立長 I/O，可能是因硬體或驅動程式問題所引起。 系統事件記錄檔可能會包含有助於診斷問題的相關事件。

#### <a name="error-detection"></a>錯誤偵測  
資料庫頁面可以使用兩個選用機制 (損毀頁保護與總和檢查碼保護) 的其中一個，來確保頁面從寫入磁碟一直到再次被讀取的完整性。 這些機制讓獨立的方法，不僅可以確認資料儲存媒體的正確性，而且也可以驗證硬體元件，如控制器、驅動程式、纜線，甚至作業系統。 這個保護會在頁面寫入磁碟之前加諸頁面，並在從磁碟讀取頁面之後進行驗證。

#### <a name="torn-page-protection"></a>損毀頁保護  
在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 中導入的損毀頁保護，是偵測因電源故障而導致分頁損毀的主要方法。 例如，非預期的電源故障可能造成只有部分的頁面寫入磁碟。 使用損毀頁保護時，(在複製了原始的兩個位元到頁面標頭中之後)，會有個 2 位元簽章放在頁面中每個 512 位元組磁區的結尾。 簽章會在每次寫入時交替使用二進位數 01 與 10，因此總是可以判斷何時未將磁區完整寫入磁碟：如果稍後讀取頁面時，位元處於錯誤的狀態，即代表頁面寫入不正確，因而可以偵測到損毀頁。 損毀頁偵測會使用最少的資源，但是無法偵測磁碟硬體故障引起的所有錯誤。

#### <a name="checksum-protection"></a>總和檢查碼保護  
在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005 中導入的總和檢查碼保護，會提供更強的資料完整性檢查。 總和檢查碼會針對每個頁面中寫入的資料來計算，並且儲存在頁面標頭中。 每當從磁碟讀取具有已儲存總和檢查碼的頁面時，資料庫引擎會在頁面中重新計算資料的總和檢查碼，如果新的總和檢查碼與儲存的總和檢查碼不同，即引發錯誤 824。 總和檢查碼保護可以比損毀頁保護捕捉更多的錯誤，因為頁面的每個位元組都會牽動它，不過相對上也需要大量的資源。 啟用總和檢查碼時，緩衝區管理員任何時間從磁碟讀取頁面，都能偵測到因電源故障和有缺陷硬體或韌體所造成的錯誤。

頁面使用的保護類型是含有該頁面之資料庫的屬性。 總和檢查碼保護是在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005 和更新版本中建立之資料庫的預設保護。 頁面保護機制是在資料庫建立期間指定，並且可以使用 ALTER DATABASE 來變更。 您可以查詢 [sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 目錄檢視中的 page_verify_option 資料行，或查詢 [DATABASEPROPERTYEX](../t-sql/functions/databasepropertyex-transact-sql.md) 函數的 IsTornPageDetectionEnabled 屬性，來判斷目前的分頁保護設定。 如果變更頁面保護設定，新的設定並不會立即影響整個資料庫。 反而每當頁面有資料寫入時，這些頁面還是會採用目前的資料庫保護等級。 這表示資料庫可能會由具有不同保護類型的頁面組成。 

## <a name="understanding-non-uniform-memory-access"></a>了解非統一記憶體存取

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會感知非統一記憶體存取 (NUMA)，而且不需要特殊組態就可以在 NUMA 硬體上順利執行。 隨著處理器時脈和數目的增加，要降低使用此額外處理能力所需要的記憶體延遲變得越來越困難。 為了避免這個狀況，硬體供應商提供了大型的 L3 快取，但這只是有限的解決方案。 NUMA 架構對這個問題提供了可擴充的解決方案。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 已設計成可利用 NUMA 型電腦的優點，而不需要進行任何應用程式變更。 如需詳細資訊，請參閱 [作法：設定 SQL Server 使用軟體 NUMA](../database-engine/configure-windows/soft-numa-sql-server.md)。

## <a name="see-also"></a>另請參閱
[讀取分頁](../relational-databases/reading-pages.md)   
 [寫入分頁](../relational-databases/writing-pages.md)

