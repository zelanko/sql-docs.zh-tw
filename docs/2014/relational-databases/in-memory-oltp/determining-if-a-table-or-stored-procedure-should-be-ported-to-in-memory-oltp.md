---
title: 判斷是否應將資料表或預存程序移植至記憶體內部 OLTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- Analyze, Migrate, Report
- AMR
ms.assetid: c1ef96f1-290d-4952-8369-2f49f27afee2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de6a778f9cdbfb7ab916f40a5250ca4f9e20c811
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63072366"
---
# <a name="determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp"></a>判斷是否應將資料表或預存程序匯出至記憶體中 OLTP
  中[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]的交易效能收集器可協助您評估記憶體內部 OLTP 是否能改善資料庫應用程式的效能。 交易效能分析報表還會指出應用程式啟用記憶體中 OLTP 所需執行的工作。 識別您要匯出至記憶體內部 OLTP 的磁碟資料表之後，即可使用 [記憶體最佳化建議程式](memory-optimization-advisor.md)協助您遷移資料表。 同樣地， [Native Compilation Advisor](native-compilation-advisor.md) 可協助您將預存程序匯出為原生編譯的預存程序。  
  
 本主題將討論如何執行以下工作：  
  
-   設定管理資料倉儲。  
  
-   設定資料收集。  
  
-   產生交易效能分析報表來識別效能關鍵的資料表和預存程序。  
  
 如需有關遷移方法的詳細資訊，請參閱[記憶體內部 OLTP-一般工作負載模式和遷移考慮](https://msdn.microsoft.com/library/dn673538.aspx)。  
  
 交易效能收集器和交易效能分析報表將協助您完成下列工作：  
  
-   分析您的工作負載，判斷記憶體中 OLTP 是否可改善效能。 交易效能收集器會收集和評估您的工作負載的效能特性。 . 交易效能分析報表接著會建議轉換成記憶體中 OLTP 後獲益最多的資料表和預存程序。  
  
-   協助您規劃及執行移轉為記憶體中 OLTP 的作業。 從磁碟資料表移轉到記憶體最佳化資料表，其間的移轉路徑可能會很費時。 記憶體最佳化 Advisor 可協助您識別將資料表移至記憶體中 OLTP 之前必須先從資料表移除的不相容項目。 記憶體最佳化 Advisor 也可協助您了解將資料表移轉到記憶體最佳化的資料表時，將對應用程式造成什麼影響。  
  
     當您想要規劃移轉至記憶體中 OLTP 的作業，以及想要將部分資料表和預存程序移轉至記憶體中 OLTP 時，都可以檢查您的應用程式能否獲益於記憶體中 OLTP。  
  
    > [!IMPORTANT]  
    >  資料庫系統的效能取決於各種不同的因素，並不是所有因素都可由交易效能收集器來觀察和測量。 因此，交易效能分析報表不保證實際的效能增益將會符合預測 (如果進行了任何預測)。  
  
 當您安裝[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]時，當您選取 [**管理工具-基本**] 或 [**管理工具-Advanced** ] 時，就會安裝交易效能收集器和產生交易效能分析報表的功能。  
  
## <a name="best-practices"></a>最佳做法  
 建議的工作流程如以下流程圖所示。 黃色節點代表選用程序：  
  
 ![AMR 工作流程](../../database-engine/media/amr-1.gif "AMR 工作流程")  
  
 您可以使用任何方法來建立效能基準，包括但不限於使用效能計數器記錄或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 活動監視器。 您的效能基準和比較中所要使用的資訊包括：  
  
-   的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]CPU 耗用量。  
  
-   的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]記憶體耗用量。  
  
-   的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]i/o 活動。  
  
-   在處理交易時的執行個體交易輸送量。  
  
 交易效能收集器每隔 15 分鐘擷取一次資料。 為了取得實用的結果，請執行交易效能收集器至少一個小時。 為了取得最佳結果，請讓交易效能收集器有充裕的執行時間，以擷取主要案例所需的資料。 唯有在您完成資料的收集之後，再產生交易效能分析報表。  
  
 將交易效能收集器設定為在生產環境的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上執行，並收集開發 (測試) 環境中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上的資料，以確保負擔最低。 如需如何將資料儲存在遠端[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]實例上的管理資料倉儲資料庫中的詳細資訊，請參閱在[遠端 SQL Server 實例上設定資料收集](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md#xxx)。  
  
## <a name="performance-impacts"></a>效能影響  
 交易效能收集器是由兩個資料收集組所組成：  
  
-   資料表使用分析  
  
-   預存程序分析  
  
 收集組每隔十五分鐘會從三個動態管理檢視 (DMV) 收集資料，並將資料上傳到設定為當做管理資料倉儲的資料庫。 上傳收集的資料對於效能的影響很低。  
  
## <a name="use-the-transaction-performance-collector"></a>使用交易效能收集器  
 以下步驟需要 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
> [!IMPORTANT]  
>  請勿在分析期間變更結構描述 (例如，新增或移除資料庫，或建立或卸除資料表)。 如果您在收集資料時變更資料庫的結構描述，納入報表中的資料庫可能會不準確。  
  
### <a name="configure-management-data-warehouse"></a>設定管理資料倉儲  
 管理資料倉儲必須設定為使用交易效能收集器。  
  
 您收集資料所在的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體版本 (設定檔) 應該與設定管理資料倉儲的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本相同或更舊。  
  
1.  在物件總管中，展開 [管理]****。  
  
2.  以滑鼠右鍵按一下 [**資料收集**]**並選取 [** 工作]，然後**設定 [管理資料倉儲**]。 [**設定管理資料倉儲 Wizard]** 隨即開始。  
  
3.  按 **[下一步]** 以選取將作為管理資料倉儲的資料庫。  
  
4.  按一下 [**新增**] 以建立新的資料庫來保存設定檔資料。 當您完成建立資料庫之後，請按一下嚮導中的 **[下一步**]。  
  
5.  精靈中的下一個步驟可讓您加入使用者和登入。 您可以將登入對應到 MDW 執行個體的角色成員資格。 從本機執行個體收集資料並不一定要這樣做。 如果您不是從本機執行個體收集資料，您可以將資料庫角色成員資格 `mdw_admin` 授與將執行即將分析之交易的帳戶。 完成時，按 **[下一步]**。  
  
6.  確定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 正在執行中。  
  
7.  在下一個畫面上，按一下 **[完成] 結束**嚮導。  
  
### <a name="configure-data-collection-on-a-local-includessnoversionincludesssnoversion-mdmd-instance"></a>在本機 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上設定資料收集  
 資料收集需要啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent。 您只需要在伺服器上設定一個資料收集器。  
  
 您可以在 SQL Server 2012 或更新版本的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]上設定資料收集器。  
  
 若要設定資料收集，以便上傳至相同執行個體上的管理資料倉儲資料庫：  
  
1.  在**物件總管**中，展開 [**管理**]。  
  
2.  以滑鼠右鍵按一下 [**資料收集**] **、選取 [** 工作]，然後**設定 [資料收集**]。 [**設定資料收集嚮導]** 隨即開始。  
  
3.  按 **[下一步]** 以選取將收集設定檔資料的資料庫。  
  
4.  選取目前的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體以及該執行個體上的管理資料倉儲資料庫。  
  
5.  在標示 [**選取您要啟用的資料收集器集合**] 的方塊中，選取 [**交易效能收集組**]。 完成時按 **[下一步]**。  
  
6.  驗證選取項目。 按 [**上一步**] 修改設定。 完成時按一下 **[完成]** 。  
  
###  <a name="xxx"></a>設定遠端[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]實例上的資料收集  
 您必須在收集資料所在的執行個體上啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 才能進行資料收集。  
  
 您可以在 SQL Server 2012 或更新版本的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]上設定資料收集器。  
  
 您需要使用正確認證建立的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent Proxy，資料收集器才能將資料上傳到執行個體上的管理資料倉儲資料庫 (此執行個體與即將分析交易的地方不同)。 若要啟用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent Proxy，您必須先使用具有網域功能的登入建立認證。 具有網域功能的登入必須是管理資料倉儲資料庫的 `mdw_admin` 群組成員。 如需如何建立認證的相關資訊，請參閱[如何：建立認證（SQL Server Management Studio）](../security/authentication-access/create-a-credential.md) 。  
  
 若要設定資料收集，以便上傳至不同執行個體上的管理資料倉儲資料庫：  
  
1.  在包含您想要遷移至記憶體中 OLTP 之磁片物件的實例上，展開物件總管中的 [**管理**] 節點。  
  
2.  以滑鼠右鍵按一下 [**資料收集**]**並選取 [** 工作]，然後**設定 [資料收集**]。 [**設定資料收集嚮導]** 隨即開始。  
  
3.  按 **[下一步]** 以選取將收集設定檔資料的資料庫。  
  
4.  確認另一個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上有管理資料倉儲資料庫存在。  
  
5.  選取另一個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體和該執行個體上的管理資料倉儲資料庫。  
  
     您收集資料所在的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體版本 (設定檔) 應該與設定管理資料倉儲的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本相同或更舊。  
  
6.  在標示 [**選取您要啟用的資料收集器集合**] 的方塊中，選取 [**交易效能收集組**]。  
  
7.  選取 [**使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]代理程式 proxy 進行遠端上傳**]。  
  
8.  完成時按 **[下一步]**。  
  
9. 選取 Proxy。  
  
     如果您要建立新的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent Proxy，  
  
    1.  按一下 [**新增**] 以顯示 [**新 Proxy 帳戶**] 對話方塊。  
  
    2.  在 [**新 Proxy 帳戶**] 對話方塊中，輸入 proxy 的名稱，選取認證，然後選擇性地輸入描述。 然後，按一下 [**主體**]。  
  
    3.  按一下 [**新增**]，然後選取 [ **Msdb**角色]。  
  
    4.  選取`dc_proxy`並按一下 **[確定]**。 然後再按一下 [確定]****。  
  
     選取正確的 proxy 之後，按 **[下一步]**。  
  
10. 若要設定系統收集組，請檢查**系統收集組**，然後按 **[下一步]**。  
  
11. 驗證選取項目。 按 [**上一步**] 修改設定。 完成時完成**完成]** 。  
  
 資料收集組現在應該已經設定妥，並且正在您的執行個體上執行。  
  
### <a name="generate-reports"></a>產生報表  
 您可以用滑鼠右鍵按一下管理資料倉儲的資料庫，然後依序選取 [**報表**]、[**管理資料倉儲**] 和 **[交易效能分析總覽**]，來產生交易效能分析報表。  
  
 報表會收集工作負載伺服器上所有使用者資料庫的相關資訊。 如果您的管理資料倉儲 (MDW) 資料庫位於本機電腦上，則會在報表中看見 MDW 資料庫。  
  
 CPU 時間與經過時間的比率較高的預存程序就是移轉作業的候選。 報表會顯示所有資料表參考，因為原生方式編譯預存程序只能參考記憶體最佳化資料表，而這些資料表可能會增加移轉成本。  
  
 資料表的詳細報表包含三個部分：  
  
-   掃描統計資料部分  
  
     此部分包含單一資料表，將顯示所收集有關資料庫資料表上掃描次數的統計資料。 資料行如下：  
  
    -   總存取數百分比。 整個資料庫活動中，此資料表上掃描次數與搜尋次數百分比。 此百分比愈高，表示與資料庫中的其他資料表相較下，較大量使用此資料表。  
  
    -   查閱統計資料/範圍掃描統計資料。 此資料行記錄分析期間，資料表上執行的點查閱及範圍掃描 (索引掃描及資料表掃描) 數。 每筆交易的平均值為預估。  
  
    -   Interop 改善和原生改善。 這些資料行可預估當資料表轉換成記憶體最佳化資料表時，點查閱或範圍掃描將會得到的效能獲益量。  
  
-   競爭統計資料部分  
  
     此部分包含在資料庫資料表上顯示競爭的資料表。 如需有關資料庫閂鎖和鎖定的詳細資訊，請參閱[鎖定架構](https://msdn.microsoft.com/library/aa224738\(v=sql.80\).aspx)。 資料行如下：  
  
    -   總等候次數百分比。 與資料庫活動相比，此資料庫資料表上閂鎖和鎖定等候數的百分比。 此百分比愈高，表示與資料庫中的其他資料表相較下，較大量使用此資料表。  
  
    -   閂鎖統計資料。 這些資料行記錄關於此資料表查詢的閂鎖等候數。 如需閂鎖的詳細資訊，[請參閱閂鎖。](https://msdn.microsoft.com/library/aa224727\(v=SQL.80\).aspx) 此數字越高，表示資料表有越多閂鎖競爭。  
  
    -   鎖定統計資料。 此資料行群組記錄頁面鎖定取得數以及查詢此資料表的等候數。 如需鎖定的詳細資訊，請參閱[瞭解 SQL Server 中的鎖定](https://msdn.microsoft.com/library/aa213039\(v=SQL.80\).aspx)。 等候數越多，表示資料表上越多鎖定競爭。  
  
-   移轉難度部分  
  
     此部分包含顯示將此資料庫資料表轉換成記憶體最佳化資料表之難度的資料表。 較高的難度評等表示較難轉換資料表。 若要查看要轉換此資料庫資料表的詳細資料，請使用[記憶體優化 Advisor](memory-optimization-advisor.md)。  
  
 資料表詳細資料包表的掃描和競爭統計資料是從[sys. dm_db_index_operational_stats &#40;transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql)收集和匯總。  
  
 預存程序的詳細資料報表包含兩個部分：  
  
-   執行統計資料部分  
  
     此部分包含的資料表將顯示所收集有關預存程序之執行的統計資料。 資料行如下：  
  
    -   快取的時間。 此執行計畫快取的時間。 如果預存程序從計畫快取卸除並重新輸入，每個快取都需要時間。  
  
    -   總 CPU 時間。 在分析期間，預存程序所耗用的總 CPU 時間。 此數字愈高，預存程序使用的 CPU 越多。  
  
    -   總執行時間。 在分析期間，預存程序使用的總執行時間量。 此數字和 CPU 時間之間的差異愈高，預存程序使用 CPU 的效率越低。  
  
    -   快取遺漏總數。 在分析期間，預存程序的執行所導致的快取遺漏數 (從實體儲存體讀取)。  
  
    -   執行計數。 在分析期間，此預存程序執行的次數。  
  
-   資料表參考部分  
  
     此部分包含的資料表是顯示此預存程序所參考的資料表。 將預存程序轉換至原生方式編譯預存程序之前，必須將所有這些資料表轉換為記憶體最佳化資料表，且必須放置在相同的伺服器和資料庫上。  
  
 預存程式詳細資料包表的執行統計資料是從[sys. dm_exec_procedure_stats &#40;transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql)收集和匯總。 參考是從 sys.databases 取得[sql_expression_dependencies &#40;transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)。  
  
 若要查看如何將預存程式轉換成原生編譯預存程式的詳細資料，請使用[Native 編譯](native-compilation-advisor.md)建議程式。  
  
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](migrating-to-in-memory-oltp.md)  
  
  
