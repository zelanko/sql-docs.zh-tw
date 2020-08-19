---
description: 增強一般複寫效能
title: 增強一般複寫效能 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- designing databases [SQL Server], replication performance
- Snapshot Agent, performance
- snapshots [SQL Server replication], performance considerations
- merge replication performance [SQL Server replication]
- snapshot replication [SQL Server], performance
- subscriptions [SQL Server replication], performance considerations
- agents [SQL Server replication], performance
- performance [SQL Server replication], general considerations
- transactional replication, performance
ms.assetid: 895b1ad7-ffb9-4a5c-bda6-e1dfbd56d9bf
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 307d27f85d5643b837298418279e22dc9225ac67
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423582"
---
# <a name="enhance-general-replication-performance"></a>增強一般複寫效能
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  透過使用本主題中所述的指導方針，您可以提升應用程式及網路上所有複寫類型的一般效能：  
  
## <a name="server-and-network"></a>伺服器和網路  
  
-   設定配置給 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] 的最小和最大記憶體數量。  
  
     依預設， [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 將根據可用的系統資源，動態地變更其記憶體需求。 若要避免複寫活動執行期間記憶體可用量過低，請使用 **min server memory** 選項設定最小可用的記憶體。 若要避免作業系統將記憶體分頁部署到光碟，亦可使用 **max server memory** 選項設定最大記憶體數量。 如需詳細資訊，請參閱[伺服器記憶體伺服器組態選項](../../../database-engine/configure-windows/server-memory-server-configuration-options.md)。  
  
-   確保適當配置資料庫資料檔案和記錄檔。 針對複寫相關的所有資料庫交易記錄，使用個別的磁碟機。  
  
     若想縮短寫入交易的時間，請將記錄檔儲存到與儲存資料庫不同的磁碟機上。 如果需要容錯功能，您可以使用磁碟陣列 (RAID)-1 來鏡射該磁碟。 對其他資料庫檔案請使用 RAID 0 或 0+1 (視您對容錯的需求而定)。 不論是否正在使用複寫，這都是很好的習慣。  
  
-   考慮為複寫用伺服器加入記憶體，特別是散發者。  
  
-   使用多處理器電腦。  
  
     複寫代理程式可以利用伺服器上額外的處理器。 如果您執行作業時 CPU 的使用量較高，則可考慮安裝一個更快的 CPU 或安裝多個 CPU。  
  
-   使用高速網路。  
  
     網路可能會成為顯著的效能瓶頸，特別是對於異動複寫而言。 可藉由使用 100 Mbps 或更快的高速網路而大幅提高將變更傳播到「訂閱者」的速度。 若網路太慢，請指定適當的網路設定與代理程式參數。  
  
## <a name="database-design"></a>資料庫設計  
  
-   依照資料庫設計的最佳做法。  
  
     一般，複寫資料庫與非複寫資料庫一樣享受效能最佳化帶來的助益。 但是，在「訂閱者」端應小心使用索引：「訂閱者」端的主索引鍵資料行應進行索引，但其他索引可能會影響插入、更新和刪除效能。  
  
-   考慮設定 READ_COMMITTED_SNAPSHOT 資料庫選項。  
  
     若要協助減少使用者活動與複寫代理程式活動之間的競爭，請為發行集和訂閱資料庫設定此選項：  
  
    ```  
    ALTER DATABASE AdventureWorks  
    SET READ_COMMITTED_SNAPSHOT ON  
    ```  
  
     如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)。  
  
-   小心使用觸發程序的應用程式邏輯。  
  
     在「訂閱者」端使用者自訂觸發程序中的商務邏輯可能會降低複寫變更到「訂閱者」的速度。  
  
    -   對於異動複寫而言，將這種邏輯包含於用來套用複寫命令的自訂預存程序中則更有效率。 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
    -   對於合併式複寫而言，使用商務邏輯處理常式可能更有效。 如需詳細資訊，請參閱[在合併同步處理期間執行商務邏輯](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)。  
  
     如果使用觸發程序來維護為合併式複寫發行之資料表中的參考完整性，請指定資料表的處理順序，以減少「合併代理程式」所需的重試次數。 如需詳細資訊，請參閱[指定合併式複寫選項](../../../relational-databases/replication/merge/specify-merge-replication-properties.md)。  
  
-   限制使用大型物件 (LOB) 資料類型。  
  
     LOB 比其他資料行資料類型需要更多儲存空間和處理。 除非您的應用程式需要，否則不要在發行項中包含這些資料行。 資料類型 **text**、 **ntext**和 **image** 已被取代。 若您納入 LOB，建議您分別依序使用資料類型 **varchar(max)**、 **nvarchar(max)**、 **varbinary(max)**。  
  
     對於異動複寫，請考慮使用名為 **OLEDB 資料流的散發設定檔**的「散發代理程式」設定檔。 如需相關資訊，請參閱 [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
## <a name="publication-design"></a>發行集設計  
  
-   只發行需要的資料。  
  
     由於複寫的設定相當容易，因此容易發生發行超過實際需要的資料數量。 這樣會耗用散發資料庫與快照集內的額外資源，而且可能降低必要資料的處理能力。 請避免發行不必要的資料表，並降低更新發行的頻率。  
  
-   透過發行集設計和發行集行為，將衝突最小化。  
  
     下列複寫類型可讓資料在「訂閱者」端變更：合併式複寫、具有可更新訂閱的異動複寫以及點對點異動複寫。 如果給定資料列在同步處理之間的多個節點上有更新，則合併式複寫和具有可更新訂閱的異動複寫支援資料衝突。 對點對複寫不支援資料衝突；必須對資料變更進行資料分割。 無論使用何種複寫類型，都建議您盡可能分割變更，因為這樣會減少衝突偵測和解決方案所需的處理。  
  
     變更可透過發行資料子集到每個「訂閱者」或透過使用可直接變更給定資料列到給定節點的應用程式來進行分割：  
  
    -   合併式複寫支援使用具有單一發行集的參數化篩選來發行資料子集。 如需詳細資訊，請參閱＜ [參數化資料列篩選器](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
    -   異動複寫支援使用具有多個發行集的靜態篩選來發行資料子集。 如需詳細資訊，請參閱[篩選發行的資料](../../../relational-databases/replication/publish/filter-published-data.md)。  
  
-   明智使用資料列篩選。  
  
     如果交易式發行集包括一或多個使用資料列篩選的發行項，則「記錄讀取器代理程式」就必須在掃描交易記錄檔時，將篩選套用到受資料表更新影響的每個資料列。 「記錄讀取器代理程式」的輸送量因而受到影響。  
  
     同樣地，合併式複寫必須評估變更或刪除的資料列，以判斷哪些「訂閱者」應接收這些資料列。 當資料列篩選是用來減少「訂閱者」端所需的資料時，此處理就會更複雜而且可能比發行資料表的所有資料列更慢。 請仔細權衡降低每個「訂閱者」端儲存需求以及達到最大輸送量需求之間的優劣。 如需篩選的詳細資訊，請參閱[篩選發行的資料](../../../relational-databases/replication/publish/filter-published-data.md)。  
  
## <a name="subscription-considerations"></a>訂閱考量因素  
  
-   有大量訂閱者時，使用提取訂閱。  
  
     「散發代理程式」與「合併代理程式」在發送訂閱的「散發者」端和提取訂閱的「訂閱者」端執行。 使用提取訂閱可透過將代理程式處理從「散發者」移動到「訂閱者」來提升效能。 如需詳細資訊，請參閱[訂閱發行集](../../../relational-databases/replication/subscribe-to-publications.md)。  
  
-   若訂閱者嚴重落後，將考慮訂閱重新初始化。  
  
     當需要將大量的變更傳送到「訂閱者」時，請使用新的快照集來重新初始化訂閱，這可能比使用複寫來移動個別的變更還要快。 如需詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
     對於異動複寫，「複寫監視器」在 **[未散發的命令]** 索引標籤上顯示以下資訊：在散發資料庫中尚未散發到「訂閱者」的交易數量；散發這些交易的估計時間。 如需詳細資訊，請參閱[使用複寫監視器來檢視資訊及執行工作](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
## <a name="snapshot-considerations"></a>快照集考量  
  
-   視需要且必須在離峰時間才執行快照集代理程式。  
  
     「快照集代理程式」會將發行者已經發行的資料表資料大量複製到散發者快照集資料夾中的一個檔案。 產生快照集可能是一項需要大量資源的處理，因此最好排程在離峰時間。  
  
-   除非需要字元模式快照集，否則請使用原生模式快照集。  
  
     除了非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者和執行 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]的訂閱者 (這兩者需要字元模式快照集) 以外，對所有訂閱者使用預設的原生模式快照集。  
  
-   為發行集使用單一快照集資料夾。  
  
     指定與快照集位置有關的發行集屬性時，您可以選擇讓快照集檔案產生於預設的快照集資料夾、替代的快照集資料夾、或是兩者皆採用。 同時在兩個位置上產生快照集檔案，則執行「快照集代理程式」時需要額外的磁碟空間和更多的處理。  
  
-   將快照集資料夾置於散發者本機磁碟機，且該散發者並非用來儲存資料庫或記錄檔。  
  
     「快照集代理程式」將資料循序寫入快照集資料夾。 將快照集資料夾放置在與任何資料庫或記錄檔不同的磁碟機上，會減少磁碟之間的競爭，有助於更快地完成快照集處理。  
  
-   在訂閱者端建立訂閱資料庫時，考慮指定簡單或大量記錄復原模式。 這樣可讓在「訂閱者」端執行快照集應用程式時，對執行大量插入工作的記錄最小。 在將快照集套用到訂閱資料庫之後，如有必要，可變更為另一個復原模式 (複寫的資料庫可使用任何復原模式)。 如需選取復原模式的詳細資訊，請參閱[還原和復原概觀 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)。  
  
-   對於低頻寬網路，請考慮在抽取式媒體上使用替代快照集資料夾和壓縮快照集。  
  
     壓縮替代快照集資料夾中的快照集檔案，可減少磁碟儲存需求，使在抽取式媒體上傳送快照集檔案更容易。  
  
     在某些情況下，壓縮的快照集可以改善網路之間傳送快照集檔案的效能。 不過，壓縮快照集需要由快照集代理程式在產生快照集檔案時，進行其他處理動作；並於套用快照集檔案時，進行散發代理程式或合併代理程式。 如此可能會減緩快照集的產生且在某些情況下會增加套用快照集的時間。 此外，若發生網路失敗，則無法繼續壓縮快照集；因此並不適合不穩定的網路。 透過網路使用壓縮快照集時，仔細考量這些權衡問題。 如需詳細資訊，請參閱 [修改快照集選項](../../../relational-databases/replication/snapshot-options.md)。 
-   考慮手動初始化訂閱。  
  
     在某些情況下，例如涉及大型初始資料集，最好是使用快照集之外的方法初始化訂閱。 如需詳細資訊，請參閱 [不使用快照集初始化交易式訂閱](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。  
  
## <a name="agent-parameters"></a>代理程式參數  
  
-   減少複寫代理程式的詳細資訊層級，僅初始化測試、監視或偵錯時除外。  
  
     減少散發代理程式和合併代理程式的 **–HistoryVerboseLevel** 參數和 **–OutputVerboseLevel** 參數。 如此可減少插入追蹤代理程式記錄和輸出中的新資料列數目。 反之，具有相同狀態的先前記錄訊息會更新為新的記錄資訊。 提高測試、監視及偵錯的詳細資訊層級，以便您能盡可能多地獲得代理程式活動的相關資訊。  
  
-   使用快照集代理程式、合併代理程式以及散發代理程式的 **–MaxBCPThreads** 參數 (指定的執行緒數目不應超過電腦上的處理器數目)。 此參數指定在建立和套用快照集時可平行執行的大量複製作業數目。  
  
-   使用散發代理程式和合併代理程式的 **–UseInprocLoader** 參數 (如果發行的資料表包括 XML 資料行，則不可使用此參數)。 此參數會使代理程式在套用快照集時使用 BULK INSERT 命令。  
  
 可於代理程式設定檔和命令列中指定代理程式參數。 如需詳細資訊，請參閱  
  
-   [處理複寫代理程式設定檔](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [檢視並修改複寫代理程式命令提示字元參數 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
-   [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)的最小和最大記憶體數量。  
  
  
