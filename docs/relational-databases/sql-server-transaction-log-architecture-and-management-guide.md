---
title: "SQL Server 交易記錄架構與管理指南 | Microsoft Docs"
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction log architecture guide
- guide, transaction log architecture
ms.assetid: 88b22f65-ee01-459c-8800-bcf052df958a
caps.latest.revision: 3
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 559172415fef699a60e88111a5e13eb6accbeb3c
ms.contentlocale: zh-tw
ms.lasthandoff: 10/04/2017

---
# <a name="sql-server-transaction-log-architecture-and-management-guide"></a>SQL Server 交易記錄架構與管理指南
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  每個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫都有交易記錄檔，這個記錄檔會記錄所有交易，以及個別交易在資料庫中所做的修改。 交易記錄是資料庫的重要元件，而且如果系統故障，就可能需要交易記錄讓資料庫返回一致的狀態。 本指南提供有關交易記錄實體及邏輯架構的資訊。 了解此架構可提升交易記錄管理的效能。  

  
##  <a name="Logical_Arch"></a> 交易記錄邏輯架構  
 在邏輯上， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 交易記錄檔會以記錄檔記錄字串的形式進行運作。 每個記錄檔記錄均由記錄序號 (LSN) 來識別。 每筆新記錄檔記錄都會寫入記錄檔的邏輯結尾處，並且其 LSN 比它前一個記錄的 LSN 來得大。 記錄檔記錄將在它們建立時依序儲存。 每筆記錄檔記錄都包含所屬交易的識別碼。 對於每筆交易，所有與交易關聯的記錄檔記錄將使用反向指標個別地連結於鏈結之中，以加速交易的回復。  
  
 資料修改的記錄檔記錄可記錄所執行的邏輯作業，或是已修改資料的前置與後置資料影像。 前置資料影像為執行作業之前的資料副本；後置資料影像為執行作業之後的資料副本。  
  
 復原作業的步驟取決於記錄檔記錄的類型：  
  
-   記錄的邏輯作業  
  
    -   若要向前復原邏輯作業，必須再次執行作業。  
  
    -   若要回復邏輯作業，則執行反向的邏輯作業。  
  
-   記錄的前置與後置資料影像  
  
    -   若要向前復原作業，將套用後置資料影像。  
  
    -   若要回復作業，將套用前置資料影像。  
  
 交易記錄檔中記錄了許多類型的作業。 這些作業包括：  
  
-   每筆交易的開始與結束。  
  
-   每個資料修改 (插入、更新或刪除)。 這包括系統預存程序或資料定義語言 (DDL) 陳述式對任何資料表 (包括系統資料表) 所做的變更。  
  
-   每個範圍與分頁的配置或取消配置。  
  
-   建立或卸除資料表或索引。  
  
 回復作業也會留下記錄。 每筆交易都會在交易記錄檔中保留空間，以確保有足夠的記錄檔空間可支援由明確回復陳述式所造成的回復，或因發生錯誤而造成的回復。 保留的空間大小須視交易中執行的作業而定，但通常會等於用來記錄每個作業的空間大小。 當交易完成後就會釋放這個保留空間。  
  
 在記錄檔中，從對成功回復全資料庫而言不可或缺的第一筆記錄檔記錄，一直到最後寫入的記錄檔記錄的這個區段，稱為記錄檔的使用中部分，或「使用中的記錄」。 這是需要進行完整資料庫復原的記錄區段。 沒有任何使用中的記錄部分可被截斷。 此第一個記錄檔記錄的記錄序號 (LSN) 就稱為最小復原 LSN (*MinLSN*)。  
  
##  <a name="physical_arch"></a> 交易記錄實體架構  
 資料庫中的交易記錄會對應到一個或多個實體檔案。 從概念上來說，記錄檔是記錄的字串。 就實際上來說，記錄的順序必須有效地儲存在實作交易記錄的一組實體檔案中。 每個資料庫至少要有一個記錄檔。  
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會在內部將每個實體記錄檔分成數個虛擬記錄檔 (VLF)。 虛擬記錄檔沒有固定的大小，一個實體記錄檔也沒有固定的虛擬記錄檔數目。 [!INCLUDE[ssDE](../includes/ssde-md.md)] 在建立或擴充記錄檔時，會動態選擇虛擬記錄檔的大小。 [!INCLUDE[ssDE](../includes/ssde-md.md)] 會盡量維持少量的虛擬檔。 記錄檔擴充之後的虛擬檔大小，是現有記錄檔大小以及新檔案所增加的大小總和。 系統管理員無法設定虛擬記錄檔的大小或數目。  

> [!NOTE]
> VLF 建立遵循此方法：
> - 若下一個成長小於目前記錄實體大小的 1/8，請建立 1 個能夠涵蓋成長大小的 VLF (從 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 開始)
> - 若成長小於 64MB，請建立 4 個能夠涵蓋成長大小的 VLF (例如：成長若為 1 MB，請建立四個 256KB 的 VLF)
> - 若成長介於 64MB 到 1GB 之間，請建立 8 個能夠涵蓋成長大小的 VLF (例如：成長若為 512MB，請建立八個 64MB 的 VLF)
> - 若成長大於 1GB，請建立 16 個能夠涵蓋成長大小的 VLF (例如：成長若為 8 GB，請建立十六個 512MB 的 VLF)

 只有當實體記錄檔是以較小的 *size* 和 *growth_increment* 值來定義時，虛擬記錄檔才會影響到系統效能。 *size* 值是記錄檔的初始大小，而 *growth_increment* 值則是每次需要新空間時加入檔案的空間量。 如果記錄檔因為許多少量增加而變得很龐大，將會產生許多虛擬記錄檔。 這樣會減慢資料庫啟動的速度，也會降低記錄備份和還原作業的執行速度。 建議您使用接近最後所需大小的 *size* 值來指派記錄檔，並使用相對較大的 *growth_increment* 值。 如需這些參數的詳細資訊，請參閱 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)。  
  
 交易記錄是循環使用的檔案。 例如，假設資料庫的一個實體記錄檔分成四個虛擬記錄檔。 資料庫建立時，邏輯記錄檔從實體記錄檔的最前面開始。 新的記錄會加在邏輯記錄檔的最後，並朝向實體記錄檔的結尾處擴充。 記錄截斷會釋出記錄出現在最小復原記錄序號 (MinLSN) 前面的所有虛擬記錄。 *MinLSN* 是成功回復全資料庫所需之最舊記錄檔記錄的記錄序號。 範例資料庫中的交易記錄看起來如下圖所示。  
  
 ![tranlog3](../relational-databases/media/tranlog3.gif)  
  
 當邏輯記錄檔的結尾到達實體記錄檔的結尾時，新的記錄資料將寫回實體記錄檔的開頭處。  
  
![tranlog4](../relational-databases/media/tranlog4.gif)   
  
 只要邏輯記錄檔的結尾永遠不碰到邏輯記錄檔的開頭，此週期就會不斷地重複。 如果經常截斷舊的記錄，以便讓目前到下個檢查點之間建立的所有新記錄一定會有足夠的空間可以使用，記錄檔就永遠不會填滿。 不過，如果邏輯記錄檔的結尾已到達邏輯記錄檔的開頭，會發生下列其中一種狀況：  
  
-   如果記錄檔啟用 FILEGROWTH 設定，而且磁碟也有可用的空間，則檔案會以 *growth_increment* 參數所指定的數量擴大，並將新的記錄新增到擴充部分。 如需 FILEGROWTH 設定的詳細資訊，請參閱 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)。  
  
-   如果未啟用 FILEGROWTH，或保存記錄檔的磁碟可用空間少於 *growth_increment* 所指定的數量，則會產生 9002 錯誤。 如需詳細資訊，請參閱[為完整交易記錄進行疑難排解](../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)。  
  
 如果記錄檔包含多個實體記錄檔，邏輯記錄檔會從頭到尾在所有的實體記錄檔移動之後，才繞回第一個實體記錄檔的起點。  
  
### <a name="log-truncation"></a>記錄截斷  
 為了避免記錄被填滿，必須截斷記錄。 記錄截斷會從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫的邏輯交易記錄中刪除非使用中的虛擬記錄檔，釋出邏輯記錄中的空間以供實體交易記錄重複使用。 如果永遠都不截斷交易記錄，最終將會填滿配置給其實體記錄檔的所有磁碟空間。 不過，必須先進行檢查點作業，才能截斷記錄。 檢查點會將目前記憶體中已修改的頁面 (稱為中途分頁) 和交易記錄資訊從記憶體寫入磁碟。 執行檢查點時，交易記錄的非使用中部分會標示成可重複使用。 之後，記錄截斷就可以釋出非使用中的部分。 如需檢查點的詳細資訊，請參閱[資料庫檢查點 &#40;SQL Server&#41;](../relational-databases/logs/database-checkpoints-sql-server.md)。  
  
 下圖將顯示截斷前後的交易記錄。 第一張圖是顯示從未進行截斷的交易記錄。 目前，邏輯記錄正使用四個虛擬記錄檔。 邏輯記錄檔是從第一個虛擬記錄檔的前面開始，並於虛擬記錄檔 4 結束。 MinLSN 記錄位於虛擬記錄檔 3 中。 虛擬記錄檔 1 和虛擬記錄檔 2 僅包含非使用中的記錄檔記錄。 這些記錄都可以截斷。 虛擬記錄 5 仍未使用而且不屬於目前邏輯記錄的一部分。  
  
![tranlog2](../relational-databases/media/tranlog2.gif)  
  
 第二張圖是顯示記錄截斷之後的內容。 虛擬記錄 1 和虛擬記錄 2 已經釋出以便重複使用。 現在邏輯記錄檔是從虛擬記錄檔 3 的前面開始。 虛擬記錄檔 5 仍未使用，而且不屬於目前邏輯記錄檔的一部分。  
  
![tranlog3](../relational-databases/media/tranlog3.gif)  
  
 除了因為某種原因而延遲以外，記錄截斷會在發生下列事件之後自動進行：  
  
-   在簡單復原模式下，發生在檢查點之後。  
  
-   在完整復原模式或大量記錄復原模式下，上一次備份以來發生檢查點時的記錄備份之後。  
  
 記錄截斷可能會因為各種因素而延遲。 如果在記錄截斷中發生長時間的延遲，交易記錄可能會填滿。 如需詳細資訊，請參閱[可能會延遲記錄截斷的因素](../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation)和[寫滿交易記錄疑難排解 &#40;SQL Server 錯誤 9002&#41;](../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)。  
  
##  <a name="WAL"></a> 預先寫入交易記錄  
 本章節說明預先寫入交易記錄在將資料修改記錄至磁碟時所扮演的角色。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會使用預先寫入記錄 (WAL) 演算法，而這項功能可確保在相關記錄檔的記錄寫入磁碟之前，不會將任何資料修改寫入磁碟。 如此可保留交易的 ACID 屬性。  
  
 若要了解預寫記錄檔的運作方式，您一定要知道如何將修改的資料寫入磁碟。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會維護緩衝快取，當需要擷取資料時，就可以將資料頁讀取到其中。 當緩衝快取中的頁面被修改時，不會立即重新寫入磁碟；而是將頁面標示為「中途」。 在實際將資料頁寫入磁碟之前，可以進行多次邏輯寫入。 每次邏輯寫入時，都會有交易記錄插入至記載修改的記錄快取中。 記錄檔記錄必須在關聯的中途分頁從緩衝區快取移除而寫入至磁碟之前，先寫入磁碟中。 檢查點處理序會定期掃描緩衝快取，檢查是否有內含來自指定資料庫之頁面的緩衝區，並將所有中途分頁寫入磁碟。 藉由建立一個點來確保所有中途分頁都已寫入磁碟中，檢查點可讓稍後的復原節省時間。  
  
 將緩衝區快取中之修改資料頁面寫入磁碟中的動作稱為清除頁面。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 含有防止中途分頁在寫入相關聯記錄檔記錄之前遭到清除的邏輯。 記錄會在交易被認可後寫入磁碟中。  
  
##  <a name="Backups"></a> 交易記錄備份  
 本章節提出有關如何備份和還原 (套用) 交易記錄的概念。 在完整和大量記錄復原模式下，進行交易記錄 (「記錄備份」) 的例行備份，對復原資料而言是必要的。 您可以在任何完整備份正在執行的同時備份記錄。 如需復原模型的詳細資訊，請參閱 [SQL Server 資料庫的備份與還原](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。  
  
 在建立第一個記錄備份之前，您必須建立完整備份，例如資料庫備份或檔案備份組中的第一個備份。 僅使用檔案備份來還原資料庫，可能會讓情況變得很複雜。 因此，我們建議您盡可能先從完整資料庫備份開始。 之後，則需要定期備份交易記錄。 這不僅是要降低工作損失的風險，也是為了在必要時可以截斷交易記錄。 交易記錄通常在每個傳統記錄備份之後截斷。  
  
 我們建議您經常進行充分的記錄備份來支援商務需求，特別是您對工作損失 (例如可能因損壞的記錄磁碟機而引起) 的耐受性。 進行記錄備份的頻率如何才適當，視您在工作損失風險的耐受性，與儲存、管理及可能還原記錄備份的容量之間所做的取捨而定。 每 15 到 30 分鐘進行一次記錄備份可能就足夠了。 如果您的業務需要將工作損失風險減至最低，請考慮更頻繁地進行記錄備份。 較頻繁的記錄備份還會帶來另一優點，就是增加記錄截斷的頻率，從而產生較小的記錄檔。  
  
 若要限制您需要還原的記錄備份數目，定期備份資料是基本作業。 例如，您可能會排程每週的完整資料庫備份和每日的差異資料庫備份。  
  
### <a name="the-log-chain"></a>記錄鏈結  
 連續的記錄備份順序稱為「記錄檔鏈結」。 記錄鏈結以資料庫的完整備份開始。 通常，只有在首次備份資料庫，或將簡單復原模式切換為完整或大量記錄復原模式之後，才會開始新的記錄鏈結。 除非您在建立完整資料庫備份時選擇覆寫現有的備份組，否則現有的記錄鏈結會維持不變。 透過維持不變的記錄鏈結，您可以從媒體集中的任何完整資料庫備份還原資料庫，後面接著所有後續的記錄備份，直到復原點為止。 復原點可能是上一個記錄備份的結尾，或是任何記錄備份中的特定復原點。 如需詳細資訊，請參閱[套用交易記錄備份 &#40;SQL Server&#41;](../relational-databases/backup-restore/transaction-log-backups-sql-server.md)。  
  
 若要將資料庫還原到失敗點，必須有完整的記錄鏈結。 也就是說，必須將交易記錄備份的順序不間斷地延伸到失敗點。 這個記錄順序必須從何處開始視您要還原的資料備份類型而定：資料庫、部分或檔案。 如果是資料庫或部分備份，記錄備份的順序必須從資料庫或部分備份的結尾延伸。 如果是檔案備份組，記錄備份的順序則必須從完整檔案備份組的起始來延伸。 如需詳細資訊，請參閱[套用交易記錄備份 &#40;SQL Server&#41;](../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)。  
  
### <a name="restore-log-backups"></a>還原記錄備份  
 還原記錄備份會向前復原交易記錄中所記錄的變更，以重新建立開始進行記錄備份作業時的正確資料庫狀態。 還原資料庫時，您必須還原在所要的完整資料庫備份之後建立的記錄備份，或者必須從您所還原之第一個檔案備份的起始開始還原記錄備份。 一般而言，還原最近的資料或差異備份之後，您必須還原一連串的記錄備份，直到復原點為止。 然後再復原資料庫。 這樣會回復所有在復原啟動時未完成的交易，並使資料庫回到線上。 復原資料庫之後，您不能再還原其他備份。 如需詳細資訊，請參閱[套用交易記錄備份 &#40;SQL Server&#41;](../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)。  

## <a name="checkpoints-and-the-active-portion-of-the-log"></a>檢查點與記錄檔的使用中部份  

檢查點可從目前資料庫的緩衝區快取將中途 (Dirty) 資料頁排清至磁碟。 這可將資料庫完整復原必須處理的記錄部分減至最少。 在完整復原時，將執行下列動作類型：

* 在系統停止之前，尚未排清至磁碟的修改記錄會向前復原。
* 未完成之交易 (例如，未包含 COMMIT 或 ROLLBACK 記錄的交易) 所關聯的所有修改都必須回復。

### <a name="checkpoint-operation"></a>檢查點作業

檢查點將在資料庫中執行下列處理序：

* 將記錄寫入記錄檔，並標示檢查點的起點。
* 儲存記錄於檢查點記錄鏈結中的檢查點資訊。  
 
    記錄於檢查點的某項資訊是必須出現於成功回復全資料庫中之第一筆記錄檔記錄的記錄序號 (LSN)。 此 LSN 就稱為「最小復原 LSN」(MinLSN)。 MinLSN 是下列項目的最小值： 

    * 檢查點起點的 LSN。
    * 最舊使用中交易之起點的 LSN。
    * 尚未傳遞至散發資料庫之最舊複寫交易起點的 LSN。 

    檢查點的記錄還包含已經修改資料庫之所有使用中交易的清單。

* 如果資料庫使用簡單復原模式，就會將 MinLSN 前面的空間標示為可重複使用。 
* 將所有中途 (Dirty) 記錄與資料頁寫入磁碟之中。
* 將標示檢查點終點的記錄寫入記錄檔中。
* 將此鏈結起點的 LSN 寫入資料庫開機頁面中。

#### <a name="activities-that-cause-a-checkpoint"></a>產生檢查點的活動

在下列情況下會產生檢查點：

* 明確執行 CHECKPOINT 陳述式。 在連接的目前資料庫中發生檢查點。
* 在資料庫中執行最基本的登入作業；例如，在使用大量記錄復原模式的資料庫中執行大量復製作業。 
* 使用 ALTER DATABASE 加入或移除資料庫檔案。
* 以 SHUTDOWN 陳述式或透過停止 SQL Server (MSSQLSERVER) 服務來停止 SQL Server 執行個體。 任何一項動作都會導致在 SQL Server 執行個體的每個資料庫中產生檢查點。
* SQL Server 執行個體會定期在每個資料庫中產生自動檢查點，以減少執行個體需要復原資料庫的時間。
* 取得資料庫備份。
* 執行需要關閉資料庫的活動。 例如，AUTO_CLOSE 為 ON，且上次使用者與資料庫的連接已經關閉，或是已變更資料庫選項，因此需要重新啟動資料庫。

### <a name="automatic-checkpoints"></a>自動檢查點

SQL Server Database Engine 會產生自動檢查點。 自動檢查點之間的間隔，是根據所使用的記錄空間量以及自上個檢查點後所經過的時間而設置。 如果資料庫只做了一些修改，自動檢查點之間的時間間隔可能會有很多變化且很長。 如果修改了許多資料，自動檢查點就會經常發生。

請使用 [復原間隔] 伺服器組態選項，針對伺服器執行個體上的所有資料庫，計算自動檢查點之間的間隔。 此選項指定了 Database Engine 在系統重新啟動的過程中，用來復原資料庫的時間上限。 將估計它在復原作業的 [復原間隔] 中可處理多少記錄。 

自動檢查點之間的間隔也是取決於復原模式：  

* 若資料庫使用完整復原模式或大量記錄復原模式，每次記錄達到 Database Engine 可在「復原間隔」選項指定之時間內處理的數目時，就會產生自動檢查點。
* 若資料庫使用的是簡單復原模式，每次當記錄的數目到達下列兩個數值的較小者時，就會產生一個自動檢查點： 

    * 記錄填滿百分之 70 時。
    * 記錄的數目到達 Database Engine 估計可在「復原間隔」選項指定之時間內處理的數目時。

如需設定復原間隔的詳細資訊，請參閱 [設定復原間隔伺服器組態選項](../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)。

> [!TIP]  
>  資料庫管理員可使用 -k SQL Server 進階安裝選項，根據某些類型的檢查點之 I/O 子系統輸送量，來調節檢查點 I/O 行為。 -k 安裝選項會套用到自動檢查點以及任何未調節的檢查點。 
 
若資料庫使用的是簡單復原模式，自動檢查點將截斷交易記錄的未使用部分。 然而，如果資料庫使用的是完整或大量記錄復原模式，自動檢查點將不會截斷記錄。 如需詳細資訊，請參閱 [交易記錄](../relational-databases/logs/the-transaction-log-sql-server.md)。 

CHECKPOINT 陳述式現在提供一個選擇性的 checkpoint_duration 引數，指定完成檢查點之要求的時間週期 (以秒為單位)。 如需詳細資訊，請參閱 [CHECKPOINT](../t-sql/language-elements/checkpoint-transact-sql.md)。


### <a name="active-log"></a>使用中的記錄

從 MinLSN 到最後寫入之記錄的記錄檔部分，稱為記錄的使用中部分，或是「使用中的記錄」。 這是需要進行完整資料庫復原的記錄部分。 沒有任何使用中的記錄部分可被截斷。 所有的記錄截斷動作必須發生於 MinLSN 之前的記錄部分。

下圖將顯示包含兩個使用中交易之交易記錄檔結尾的簡化版本。 檢查點記錄已被壓縮成一個記錄。

![active_log](../relational-databases/media/active-log.gif) 

LSN 148 是交易記錄中最後一個記錄。 當記錄於 LSN 147 的檢查點經過處理之後，將會認可 Tran 1，而 Tran 2 將成為唯一的使用中交易。 這會使得 Tran 2 的第一個記錄成為最後檢查點之使用中交易的最早記錄。 這可讓 LSN 142，也就是 Tran 2 的 Begin 交易記錄，成為 MinLSN。

### <a name="long-running-transactions"></a>長時間執行的交易

使用中的記錄必須包含所有未認可交易的每個部分。 啟動交易、但尚未認可或復原交易的應用程式，將不會讓 Database Engine 將 MinLSN 往前移。 這可能導致兩類問題：

* 若系統是在交易已執行許多未認可的修改之後關機，接著重新啟動之復原階段所需的時間可能比 [復原間隔] 選項所指定的時間多很多。
* 因為記錄無法截斷超過 MinLSN，記錄可能會成長得很大。 即使資料庫使用的是簡單的復原模式，此狀況也會發生，因為交易記錄檔通常會在每個自動檢查點截斷。

### <a name="replication-transactions"></a>複寫交易

「記錄讀取器代理程式」會監視針對異動複寫設定之每個資料庫的交易記錄，並將標示要複寫的交易從交易記錄複製到散發資料庫中。 使用中的記錄必須包含所有標示要複寫但尚未傳遞到散發資料庫的交易。 如果這些交易未及時複寫的話，將使記錄無法截斷。 如需詳細資訊，請參閱 [異動複寫](../relational-databases/replication/transactional/transactional-replication.md)。

  
## <a name="additional-reading"></a>其他閱讀資料  
 建議您閱覽下列文章和書籍，了解交易記錄的其他相關資訊。  
  
 [管理交易記錄檔的大小](../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)   
 [sys.dm_db_log_info &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)  
 [sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)     
 [交易記錄 &#40;SQL Server&#41;](../relational-databases/logs/the-transaction-log-sql-server.md)        
 [了解 SQL Server 中的記錄與復原，作者 Paul Randal](http://technet.microsoft.com/magazine/2009.02.logging.aspx)    
 [《SQL Server Transaction Log Management》，作者 Tony Davis 和 Gail Shaw](http://www.simple-talk.com/books/sql-books/sql-server-transaction-log-management-by-tony-davis-and-gail-shaw/)  
  
  

