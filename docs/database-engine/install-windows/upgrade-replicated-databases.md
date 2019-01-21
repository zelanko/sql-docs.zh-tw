---
title: 升級複寫的資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- merge replication database upgrades [SQL Server replication]
- replication [SQL Server], upgrading
- transactional replication, upgrading databases
- snapshot replication [SQL Server], upgrading databases
- upgrading replicated databases
ms.assetid: 9926a4f7-bcd8-4b9b-9dcf-5426a5857116
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 279a5c55ddc305d62e3e09f1f8073057b4ff226b
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124608"
---
# <a name="upgrade-replicated-databases"></a>升級複寫的資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] 支援從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級複寫資料庫。升級節點時，不需要停止其他節點上的活動。 請確定您遵守有關拓撲中支援之版本的規則：  
  
-   散發者可以是任何版本，只要其高於或等於發行者版本 (在許多情況下，散發者與發行者為同一執行個體)。    
-   發行者可以是任何版本，只要它小於或等於散發者版本即可。    
-   訂閱者版本視發行集的類型而定：    
    - 交易式發行集的訂閱者可以是兩個發行者版本內的任何版本。 例如：SQL Server 2012 (11.x) 發行者可以有 SQL Server 2014 (12.x) 和 SQL Server 2016 (13.x) 訂閱者，而 SQL Server 2016 (13.x) 發行者可以有 SQL Server 2014 (12.x) 和 SQL Server 2012 (11.x) 訂閱者。     
    - 合併式發行集的訂閱者可以是等於或小於版本生命週期支援週期所支援發行者版本的所有版本。  
 
SQL Server 的升級路徑視部署模式而有所不同。 SQL Server 在一般情況下會提供兩種升級路徑：
- 並存：部署平行環境，並將資料庫及相關聯的執行個體層級物件 (例如登入、作業等) 移到新環境。 
- 就地升級：允許 SQL Server 安裝媒體透過取代 SQL Server 位元並升級資料庫物件，將現有的 SQL Server 安裝升級。 針對執行 Always On 可用性群組或容錯移轉叢集執行個體的環境，就地升級會結合[輪流升級](choose-a-database-engine-upgrade-method.md#rolling-upgrade)，將停機時間縮到最短。 

複寫拓撲並存升級所採用常見方法是將部分發行者/訂閱者配對移到新的並存環境，而不是移動整個拓撲。 這種階段式方法可協助控制停機時間，並針對取決於複寫的商務將影響降低到某個程度。  


> [!NOTE]  
> **如需將複寫拓撲升級至 SQL 2016 的詳細資訊，請參閱部落格文章 [Upgrading a Replication Topology to SQL Server 2016](https://blogs.msdn.microsoft.com/sql_server_team/upgrading-a-replication-topology-to-sql-server-2016/)** (將複寫拓撲升級至 SQL Server 2016)。 

 >[!WARNING]
 > 升級複寫拓樸是多步驟程序。 建議您先在測試環境中嘗試升級複寫拓撲的複本，再於實際生產環境上執行升級。 這有助於制訂順暢處理升級所需的任何操作文件，而不會在實際升級過程期間導致昂貴且長時間的停機。 我們已看到客戶升級其複寫拓樸時，透過為其生產環境使用 Always On 可用性群組和/或 SQL Server 容錯移轉叢集執行個體，大幅減少停機時間。 此外，建議您先備份所有的資料庫 (包括 MSDB、Master、散發資料庫及參與複寫的使用者資料庫)，再嘗試升級。


## <a name="replication-matrix"></a>複寫矩陣

[!INCLUDE[repl matrix](../../includes/replication-compat-matrix.md)]
  
## <a name="run-the-log-reader-agent-for-transactional-replication-before-upgrade"></a>在升級之前執行異動複寫的記錄讀取器代理程式  
 升級 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] 之前，您必須確定所有來自已發行資料表的認可交易都已經由記錄讀取器代理程式處理過。 若要確定已經處理過所有交易，請針對每個包含交易式發行集的資料庫執行下列步驟：  
  
1.  確定已在針對資料庫執行記錄讀取器代理程式。 依預設，代理程式會持續執行。    
2.  停止在已發行資料表上的使用者活動。  
3.  提供時間讓記錄讀取器代理程式將交易複製到散發資料庫，然後再停止代理程式。  
4.  執行 [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) 以確認已處理所有的交易。 這個程序中所產生的結果集應該是空的。   
5.  執行 [sp_replflush](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) 以關閉 sp_replcmds 的連接。   
6.  將伺服器升級至最新版的 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]。   
7.  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 和記錄讀取器代理程式在升級之後沒有自動啟動，則將其重新啟動。  
  
## <a name="run-agents-for-merge-replication-after-upgrade"></a>升級之後為合併式複寫執行代理程式  
 升級之後，請為每一個合併式發行集執行快照集代理程式，並為每一個訂閱執行合併代理程式來更新複寫中繼資料。 您不必套用新的快照集，因為不需要重新初始化訂閱。 升級之後，第一次執行合併代理程式時會更新訂閱中繼資料。 這表示在發行者升級時，訂閱資料庫可以持續在線上運作並保持使用中狀態。  
  
 合併式複寫會將發行集與訂閱中繼資料儲存在發行集與訂閱資料庫中的許多系統資料表內。 執行快照集代理程式會更發行集中繼資料，而執行合併代理程式會更新訂閱中繼資料。 只有要產生發行集快照集時才需要它。 如果合併式發行集使用參數化篩選，則每個資料分割也會有快照集。 您不需要更新這些分割快照集  
  
 您可以從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、複寫監視器或命令列執行代理程式。 如需如何執行快照集代理程式的詳細資訊，請參閱下列文章：  
  
-   [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)
-   [啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)
-   [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)
-   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  

如需如何執行合併代理程式的詳細資訊，請參閱下列文章：
-   [同步處理提取訂閱](../../relational-databases/replication/synchronize-a-pull-subscription.md)
-   [同步處理發送訂閱](../../relational-databases/replication/synchronize-a-push-subscription.md)  
  

在使用合併式複寫的拓撲中升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後，如果您想要使用新功能，請變更任何發行集的發行集相容性層級。  
  
## <a name="upgrading-to-standard-workgroup-or-express-editions"></a>升級至 Standard、Workgroup 或 Express Edition  
從 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 的一個版本升級到另一個版本之前，請確認您目前使用的功能在您想要升級後的版本中受到支援。 如需詳細資訊，請參閱 [SQL Server 版本和支援的功能](../../sql-server/editions-and-components-of-sql-server-2017.md)中的＜複寫＞一節。  

## <a name="steps-to-upgrade-a-replication-topology"></a>升級複寫拓撲的步驟
這些步驟概述升級複寫拓撲中伺服器時應該採用的順序。 無論您執行的是交易式或合併式複寫，都適用相同的步驟。 不過，這些步驟並未涵蓋點對點複寫、佇列更新訂閱，也未涵蓋立即更新訂閱。 

### <a name="in-place-upgrade"></a>就地升級 
1. 升級散發者。 
2. 升級發行者和訂閱者。 這些可以依任何順序升級。 

 >[!NOTE]
 > 若為 SQL 2008 和 2008 R2，必須同時完成發行者和訂閱者的升級，以與複寫拓樸矩陣保持一致。 SQL 2008 或 2008R2 的發行者或訂閱者不能有 SQL 2016 (或更高版本) 的發行者或訂閱者。 如果無法同時升級，請使用中繼升級將 SQL 執行個體升級至 SQL 2014，再將其升級至 SQL 2016 (或更高版本)。  

### <a name="side-by-side-upgrade"></a>並存升級
1. 升級散發者。
1. 在新的 SQL Server 執行個體上重新設定[散發](../../relational-databases/replication/configure-distribution.md)。
1. 升級發行者。
1. 升級訂閱者。
1. 重新設定所有的發行者-訂閱者配對，包括重新初始化訂閱者。 


## <a name="steps-for-side-by-side-migration-of-the-distributor-to-windows-server-2012-r2"></a>將散發者並存移轉至 Windows Server 2012 R2 的步驟
如果您規劃將 SQL Server 執行個體升級至 SQL 2016 (或更新版本)，且您目前的 OS 是 Windows 2008 (或 2008 R2)，則必須將 OS 並存升級至 Windows Server 2012 R2 或更新版本。 使用此中繼 OS 升級的原因是 SQL Server 2016 不能安裝在 Windows Server 2008/2008 R2 上，且 Windows Server 2008/20008 R2 不允許就地升級容錯移轉叢集。 您可以在獨立 SQL Server 執行個體，或 Always On 容錯移轉叢集執行個體 (FCI) 內的 SQL Server 執行個體上執行下列步驟。

1. 在 Windows Server 2012 R2/2016 上使用不同的 Windows 叢集和 SQL Server FCI 名稱或獨立主機名稱，設定新的 SQL Server 執行個體 (獨立或 Always On 容錯移轉叢集)、版次和版本作為散發者。 您必須使目錄結構與舊散發者保持相同，以確保可以在新環境的相同路徑中找到複寫代理程式可執行檔、複寫資料夾及資料庫檔案路徑。 這會減少任何必要的移轉後/升級後步驟。
1. 請確定您的複寫已同步，然後關閉所有的複寫代理程式。 
1. 關閉目前的 SQL Server 散發者執行個體。 如果這是獨立執行個體，請關閉伺服器。 如果這是 SQL FCI，則在叢集管理員中將整個 SQL Server 角色離線，包括網路名稱。 
1. 移除舊 (目前的散發者執行個體) 環境的 DNS 和 AD 電腦物件項目。 
1. 變更新伺服器的主機名稱，以符合舊伺服器的主機名稱。
    1. 如果這是 SQL FCI，請使用與舊執行個體相同的虛擬伺服器名稱重新命名新 SQL FCI。 
1. 使用 SAN 重新導向、儲存體複製或檔案複製，從前一個執行個體中複製資料庫檔案。 
1. 將新的 SQL Server 執行個體上線。 
1. 重新啟動所有的複寫代理程式，並確認代理程式都成功執行。
1. 驗證複寫是否正常運作。 
1. 使用 SQL Server 安裝媒體，將您的 SQL Server 執行個體就地升級至新版 SQL Server。 


  >[!NOTE]
  > 若要減少停機時間，建議您將「並存移轉」散發者作為一個活動執行，並將「就地升級至 SQL Server 2016」作為另一個活動執行。 這可讓您採取階段式方法、降低風險，並將停機時間縮至最短。

## <a name="web-synchronization-for-merge-replication"></a>合併式複寫的 Web 同步處理  
 合併式複寫的 Web 同步處理選項要求，必須將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener (replisapi.dll) 複製到用於同步處理之 Internet Information Services (IIS) 伺服器上的虛擬目錄。 當您設定 Web 同步處理時，「設定 Web 同步處理精靈」會將檔案複製到虛擬目錄。 如果您升級安裝在 IIS 伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件，就必須將 replisapi.dll 從 COM 目錄手動複製到 IIS 伺服器上的虛擬目錄。 如需設定 Web 同步處理的詳細資訊，請參閱 [設定 Web 同步處理](../../relational-databases/replication/configure-web-synchronization.md)。  
  
## <a name="restoring-a-replicated-database-from-an-earlier-version"></a>從舊版還原複寫的資料庫  
 若要確定從舊版還原複寫資料庫的備份時有保留複寫設定：還原到與建立備份的伺服器和資料庫同名的伺服器和資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 複寫](../../relational-databases/replication/sql-server-replication.md)  
 [複寫管理常見問題集](../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)   
 [複寫回溯相容性](../../relational-databases/replication/replication-backward-compatibility.md)   
 [支援的版本與版本升級](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [升級 SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
 [Upgrading a Replication Topology to SQL Server 2016](https://blogs.msdn.microsoft.com/sql_server_team/upgrading-a-replication-topology-to-sql-server-2016/) (將複寫拓撲升級至 SQL Server 2016)
