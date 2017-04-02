---
title: "增強合併式複寫效能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "發行集 [SQL Server 複寫], 設計和效能"
  - "設計資料庫 [SQL Server], 複寫效能"
  - "合併代理程式, 效能"
  - "快照集 [SQL Server 複寫], 效能考量"
  - "合併式複寫效能 [SQL Server 複寫]"
  - "訂閱 [SQL Server 複寫], 效能考量"
  - "效能 [SQL Server 複寫], 合併式複寫"
  - "代理程式 [SQL Server 複寫], 效能"
ms.assetid: f929226f-b83d-4900-a07c-a62f64527c7f
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# 增強合併式複寫效能
  考慮到一般效能提示中所述 [增強一般複寫效能](../../../relational-databases/replication/administration/enhance-general-replication-performance.md), ，考慮幾個其他方面的特定合併式複寫。  
  
## 資料庫設計  
  
-   資料列篩選與聯結篩選中使用的索引資料行。  
  
     當您在已發行的發行項上使用資料列篩選時，請在篩選的 WHERE 子句中所使用的每個資料行上建立一個索引。 如果沒有索引， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 就必須讀取資料表，以判斷資料列是否應包含在資料分割中的每個資料列。 有了索引之後，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 就可以很快地找出應該包含的資料列。 當複寫單從索引便可完全解析篩選的 WHERE 子句時，便能產生最快的處理速度。  
  
     為聯結篩選所使用的全部資料行加上索引也非常重要。 每次執行「合併代理程式」時，系統都會搜尋基底資料表，以決定父資料表與相關資料表中哪些資料列應該包含於資料分割。 為聯結的資料行建立索引可避免 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在「合併式代理程式」每次執行時都讀取資料表中的每個資料列。  
  
     如需有關篩選的詳細資訊，請參閱 [篩選合併式複寫的已發佈資料](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)。  
  
-   考慮包括大型物件 (LOB) 資料類型的過度正規化資料表。  
  
     發生同步處理時，「合併代理程式」可能需要從「發行者」或「訂閱者」讀取及傳送整個資料列。 如果資料列包含使用 LOB 的資料行，則上述處理可能需要額外的記憶體配置，且即使這些資料行並未更新仍會對效能造成負面影響。 為了降低這一效能影響的可能性，請考慮將 LOB 資料行置於另一個資料表，對資料列資料的其餘部分使用一對一關聯性。 資料型別 **文字**, ，**ntext**, ，和 **映像** 已被取代。 如果您包含 Lob，建議您使用的資料型別 **varchar （max)**, ，**nvarchar （max)**, ，**varbinary （max)**, 分別。  
  
## 發行集設計  
  
-   使用 90RTM 的發行集相容性層級 ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本)。  
  
     除非一個或多個 「 訂閱者 」 使用不同版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ，指定發行集必須僅支援 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本。 這可讓發行集利用新功能與效能最佳化。  
  
-   使用適當的發行集保留設定。  
  
     發行集保留期限，即訂閱必須進行同步處理之前的最長時間，它決定追蹤中繼資料的儲存時間。 值較大可能會影響儲存與處理效能。 如需有關如何設定發行集保留期限的詳細資訊，請參閱 [訂閱逾期與停用](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
-   使用只在發行者端變更之資料表的僅限下載發行項。 如需詳細資訊，請參閱 [最佳化合併式複寫效能的 「 文章](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
### 篩選設計與使用  
  
-   限制資料列篩選子句的複雜性。  
  
     限制篩選條件的複雜度可在「合併代理程式」評估資料列變更以便傳送至「訂閱者」時協助改善效能。 請避免在合併資料列篩選子句內使用子選取。 反之請考慮使用聯結篩選，當您要依據某個資料表中的資料列篩選子句來分割另一個資料表中的資料時，使用聯結篩選通常更有效率。 如需篩選的詳細資訊，請參閱 [篩選合併式複寫的已發佈資料](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)。  
  
-   使用有參數化篩選的預先計算的資料分割 (預設為使用這項功能)。 如需詳細資訊，請參閱 [最佳化 Parameterized Filter Performance with Precomputed Partitions](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)。  
  
     預先計算的資料分割會對篩選行為造成許多限制。 如果您的應用程式無法遵守這些限制，設定 **keep_partition_changes** 選項 **True**, ，這樣會提供效能優勢。 如需詳細資訊，請參閱 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
-   如果資料已篩選，但是未在使用者之間共用，則使用非重疊資料分割。  
  
     複寫可以最佳化未在資料分割或訂閱間共用之資料的效能。 如需詳細資訊，請參閱 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
-   不要建立複雜的聯結篩選階層。  
  
     在合併處理期間聯結篩選五個 (含) 以上資料表可能對效能有很大影響。 建議要產生包含五個 (含) 以上資料表的聯結篩選時，考慮使用其他解決方案：  
  
    -   不要篩選主要為下列類型的資料表：查閱資料表、小型資料表以及內容不會變更的資料表。 讓這些資料表整體成為發行集的一部分。 建議僅在必須分割給「訂閱者」的資料表之間使用聯結篩選。 如需相關資訊，請參閱 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)。  
  
    -   如果聯結中有大量資料表，請考慮去除資料庫正規化的設計或使用對應資料表。 例如，如果業務員僅需其客戶的資料，但需要六個聯結以將客戶與業務員關聯，請考慮在客戶資料表中新增一個資料行以識別該業務員。 業務員資料有所重複，但複寫資料分割的效能益處可能要超過去除資料表正規化的成本。  
  
    -   當批次包含大量資料變更時，若要提升預先計算的資料分割效能，請小心設計您的應用程式。 務必確定先變更聯結篩選中父資料表的資料，然後再進行子資料表中對應的變更。  
  
-   設定 **join_unique_key** 選項 **1** 如果邏輯允許。  
  
     此參數設定為 **1** 表示聯結篩選中的子系和父資料表之間的關聯性為一對一或一對多。 只將此參數設定為 **1** 如果有保證唯一性的子資料表的聯結資料行的條件約束。 如果此參數設定為 **1** 不正確，可能會發生非聚合的資料。 如需相關資訊，請參閱 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)。  
  
-   使用預先計算的資料分割時，應避免執行有大量變更的批次。  
  
     在執行包含大量資料變更的批次之後執行合併代理程式時，代理程式會嘗試將此大型批次分割成幾個較小的批次。 這時候，其他合併代理程式處理序可能會遭到封鎖。 請考慮減少批次中的變更次數，並在批次之間執行合併代理程式。 如果無法進行此，增加的值， **generation_leveling_threshold** 發行集。  
  
## 訂閱考量因素  
  
-   交錯訂閱同步處理排程。  
  
     如果有大量「訂閱者」與某「發行者」同步，請考慮交錯配置排程以使「合併代理程式」在不同時間執行。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md)。  
  
## 合併代理程式參數  
 「 合併代理程式和其參數的相關資訊，請參閱 [複寫合併代理程式](../../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
-   升級的提取訂閱的所有訂閱者 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本。  
  
     升級至 「 訂閱者 」 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新本會升級該訂閱者端之訂閱所使用 「 合併代理程式。 若要利用各項新功能與效能最佳化，則需要使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本的「合併代理程式」。  
  
-   如果透過快速連接同步處理的訂閱從 「 發行者 」 與 「 訂閱者 」 傳送變更，請使用 **– ParallelUploadDownload** 「 合併代理程式參數。  
  
     [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引進新的合併代理程式參數︰ **– ParallelUploadDownload**。 設定此參數可讓「合併代理程式」平行處理上傳至「發行者」以及下載至「訂閱者」的變更。 這對於高網路頻寬的高容量環境非常有用。 可於代理程式設定檔和命令列中指定代理程式參數。 如需詳細資訊，請參閱：  
  
    -   [Work with Replication Agent Profiles](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [檢視及修改複寫代理程式命令提示字元參數 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
    -   [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
-   請考慮增加的值 **-MakeGenerationInterval** 參數，特別是在同步處理從上的傳訂閱者下載項目比 「 訂閱者 」。  
  
-   當您同步處理具有大量資料的資料列 (例如，具有 LOB 資料行的資料列) 時，Web 同步處理會要求額外的記憶體配置，而這樣會降低效能。 當「合併代理程式」產生 XML 訊息，而此訊息包含了過多具有大量資料的資料列時，便會發生這個情況。 如果「合併代理程式」在 Web 同步處理期間耗用太多的資源，請使用以下其中一個方法來減少在單一訊息中所傳送的資料列數目：  
  
    -   對「合併代理程式」使用慢速連結代理程式設定檔。 如需詳細資訊，請參閱 [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
    -   減少 **-DownloadGenerationsPerBatch** 和 **-UploadGenerationsPerBatch** 參數的值為 10 或以下的 「 合併代理程式。 這兩個參數的預設值為 50。  
  
## 快照集考量  
  
-   在產生初始快照集之前，於大型資料表上建立 ROWGUIDCOL 資料行。  
  
     合併式複寫要求每個發行的資料表都要有一個 ROWGUIDCOL 資料行。 若在「快照集代理程式」建立最初的快照集檔案之前表格中還沒有 ROWGUIDCOL 資料行的存在，則代理程式就必須先新增並填入 ROWGUIDCOL 資料行。 若要在合併式複寫期間產生快照集時獲得效能優勢，請在發行之前於每個資料表上建立 ROWGUIDCOL 資料行。 資料行可以具有任何名稱 (**rowguid** 由預設的快照集代理程式)，但是必須具有下列資料類型特性︰  
  
    -   資料類型 UNIQUEIDENTIFIER。  
  
    -   預設值 NEWSEQUENTIALID() 或 NEWID()。 建議使用 NEWSEQUENTIALID()，因為它可以在進行變更及追蹤變更時提供更高的效能。  
  
    -   ROWGUIDCOL 屬性集。  
  
    -   資料行上的唯一索引。  
  
-   預先產生快照集及/或允許訂閱者在第一次同步處理時，要求快照集的產生與套用。  
  
     使用上述一或兩個選項為使用參數化篩選的發行集提供快照集。 如果您未指定其中一個選項，使用一系列 SELECT 與 INSERT 陳述式，而不是使用初始化的訂閱 **bcp** 公用程式; 此程序變得很慢。 如需相關資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
## 維護與監視考量  
  
-   偶爾重新索引合併式複寫系統資料表。  
  
     合併式複寫維護的一部分，偶爾會檢查與合併式複寫相關的系統資料表的成長︰ **MSmerge_contents**, ，**MSmerge_genhistory**, ，和 **MSmerge_tombstone**, ，**MSmerge_current_partition_mappings**, ，和 **MSmerge_past_partition_mappings**。 定期重新整理資料表的索引。 如需詳細資訊，請參閱 [重新組織與重建索引](../../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
-   使用效能監視同步處理 **同步處理記錄** 複寫監視器 」 中的索引標籤。  
  
     合併式複寫，複寫監視器 」 會顯示詳細的統計資料中 **同步處理記錄** ] 索引標籤，每個發行項同步處理期間，包括的時間處理所花費的每個處理階段 （上傳變更、 下載變更等等）。 這樣有助於找出導致過慢的特定資料表，同時也是解決合併訂閱效能問題的最佳地點。 如需檢視詳細統計資料的詳細資訊，請參閱 [檢視資訊並執行工作的代理程式相關聯的訂閱 & #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
  