---
title: 複寫管理的最佳做法 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- administering replication, best practices
- replication [SQL Server], administering
ms.assetid: 850e8a87-b34c-4934-afb5-a1104f118ba8
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 00683ffe3901a02f2996f638ed7ec231acf3f98d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="best-practices-for-replication-administration"></a>複寫管理的最佳做法
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  設定複寫之後，請務必了解如何管理複寫拓撲。 這個主題提供各個範疇的基本最佳做法指導，並可透過連結方式分別取得進一步資訊。 除了依照此主題中呈現的最佳做法指導以外，請考慮閱讀常見問答集，以更加熟悉一般問題：[複寫管理員的常見問題集](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)。  
  
 將最佳做法指南分成兩個方面非常有用：  
  
-   下列資訊涵蓋應為所有複寫拓撲實作的最佳做法：  
  
    -   開發並測試備份與還原策略。  
  
    -   編寫複寫拓撲指令碼。  
  
    -   建立臨界值和警示。  
  
    -   監視複寫拓撲。  
  
    -   必要時，建立效能基準線並微調複寫。  
  
-   下列資訊涵蓋對於您的拓撲來說應予以考慮，但可能不是必要的最佳做法：  
  
    -   定期驗證資料。  
  
    -   透過設定檔調整代理程式參數。  
  
    -   調整發行集和散發保留期限。  
  
    -   了解應用程式需求變更時如何變更發行項與發行集屬性。  
  
    -   了解應用程式需求變更時如何變更結構描述。  
  
## <a name="develop-and-test-a-backup-and-restore-strategy"></a>開發並測試備份與還原策略  
 所有的資料庫應定期備份，並應定期測試還原這些備份的功能；複寫的資料庫也不能例外。 下列資料庫應定期備份：  
  
-   發行集資料庫  
  
-   散發資料庫  
  
-   訂閱資料庫  
  
-   「發行者」、「散發者」及所有「訂閱者」端的**msdb** 資料庫和 **master** 資料庫  
  
 針對複寫的資料庫進行資料的備份與還原時，需要特別地注意。 如需詳細資訊，請參閱 [備份及還原複寫的資料庫](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)。  
  
## <a name="script-the-replication-topology"></a>編寫複寫拓撲指令碼  
 拓撲中的所有複寫元件都應作為損毀復原計畫的一部份來編寫指令碼，而指令碼也可以用於自動執行重複性工作。 指令碼包含實作已編寫指令碼之複寫元件所必要的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 系統預存程序，如發行集或訂閱。 指令碼可以在精靈中建立 (如新增發行集精靈)，或者可以在建立元件之後，於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 建立。 您可使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 **sqlcmd**，檢視、修改和執行指令碼。 指令碼可以和備份檔案一起儲存，萬一必須重新設定複寫拓撲時即可使用。 如需詳細資訊，請參閱＜ [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)＞。  
  
 如果任何屬性被變更，則應對該元件重新編寫指令碼。 若您在異動複寫中使用自訂預存程序，每個程序副本會與指令碼同時儲存；若程序變更，則副本必須更新 (程序通常在結構描述變更或改變應用程式需求時進行更新)。 如需自訂程序的詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
## <a name="establish-performance-baselines-and-tune-replication-if-necessary"></a>必要時，建立效能基準線並微調複寫  
 在設定複寫前，建議您先熟悉影響複寫效能的因素：  
  
-   伺服器和網路硬體  
  
-   資料庫設計  
  
-   散發者組態  
  
-   發行集設計與選項  
  
-   篩選設計與使用  
  
-   訂閱選項  
  
-   快照集選項  
  
-   代理程式參數  
  
-   維護  
  
 在設定複寫後，建議您開發一個效能基準線，它可讓您判斷複寫在您的應用程式及拓撲之一般工作負載下的行為。 使用複寫監視器和系統監視器來判斷下列五個複寫效能維度的特定數值：  
  
-   延遲：資料變更要在複寫拓撲的節點之間傳播所需要花費的時間。  
  
-   輸送量：系統在一段長時間可承受的複寫活動量 (以某段時間傳遞的命令數量來測量)。  
  
-   並行：在系統上可同步操作的複寫處理數量。  
  
-   同步處理的持續時間：完成給定同步處理所需要的時間長度。  
  
-   資源消耗：用來作為複寫處理結果的硬體和網路資源。  
  
 延遲和輸送量與異動複寫關係密切，因為在異動複寫上建立的系統通常需要低度延遲和高輸送量。 並行和同步處理的持續時間與合併式複寫關係密切，因為在合併式複寫上建立的系統通常有大量的訂閱者，同時發行者可與這些訂閱者擁有許多並行的同步處理。  
  
 建立比較基準數之後，設定複寫監視器的臨界值。 如需詳細資訊，請參閱[在複寫監視器中設定臨界值和警告](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)和[使用複寫代理程式事件的警示](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)。 若您遭遇效能上的問題，建議閱讀上述改善效能主題中所有建議事項，並針對您遇到的問題，套用可能產生影響的變更。  
  
## <a name="create-thresholds-and-alerts"></a>建立臨界值和警示  
 「複寫監視器」允許您設定大量與狀態及效能相關的臨界值。 建議為您的拓撲設定適當的臨界值；當達到臨界值時，會顯示警告，並可以選擇性地將警示傳送到電子郵件帳戶、呼叫器或其他裝置。 如需相關資訊，請參閱 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
 除了與監視臨界值相關聯的警示之外，複寫還提供大量用於回應複寫代理程式動作之預先定義的警示。 管理員可以使用這些警示隨時獲悉複寫拓撲的狀態。 建議閱讀描述該警示的主題，並使用適合您管理需要的任何警示 (必要時，也可以建立其他警示)。 如需詳細資訊，請參閱[使用針對複寫代理程式事件的警示](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)。  
  
## <a name="monitor-the-replication-topology"></a>監視複寫拓撲  
 在設定複寫拓撲且已設定臨界值及警示後，建議您定期監視複寫。 監控複寫拓撲是部署複寫時很重要的層面。 由於已散發複寫活動，因此必須跨越所有複寫相關的電腦，追蹤活動和狀態 下列工具可用來監視複寫：  
  
-   「複寫監視器」是監視複寫的最重要的工具，可讓您監視複寫拓撲的全面健全狀況。 如需詳細資訊，請參閱＜ [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)＞。  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] 和 Replication Management Objects (RMO) 提供監視複寫的介面。 如需詳細資訊，請參閱＜ [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)＞。  
  
-   「系統監視器」也可用於監視複寫效能。 如需詳細資訊，請參閱＜ [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md)＞。  
  
## <a name="validate-data-periodically"></a>定期驗證資料  
 複寫並不需要進行驗證，但建議對異動複寫和合併式複寫定期執行驗證。 驗證允許您驗證「訂閱者」端的資料與「發行者」端的資料是否相符合。 成功的驗證則表示，在那個時間點，「發行者」端的所有變更都已複寫到「訂閱者」端 (同時，如果「訂閱者」端支援更新，則「訂閱者」端的所有變更也都會複寫到「發行者」端)，而且這兩個資料庫將保持同步。  
  
 建議根據發行集資料庫的備份排程執行驗證。 例如，如果發行集資料庫每週進行一次完整備份，則驗證會在備份完成後每週執行一次。 如需詳細資訊，請參閱[驗證複寫的資料](../../../relational-databases/replication/validate-replicated-data.md)。  
  
## <a name="use-agent-profiles-to-change-agent-parameters-if-necessary"></a>必要時，使用代理程式設定檔變更代理程式參數  
 代理程式設定檔提供一個設定複寫代理程式參數的便利方法。 參數也可以在代理程式命令列指定，但是如果您需要變更參數值，則一般更適合使用預先定義的代理程式設定檔或者建立一個新設定檔。 例如，如果您使用合併式複寫，同時「訂閱者」從寬頻連接移到撥號連接，請考慮為「合併代理程式」使用 **慢速連結** 設定檔；此設定檔會使用一組更適合慢速通訊連結的參數。 如需詳細資訊，請參閱＜ [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)＞。  
  
## <a name="adjust-publication-and-distribution-retention-periods-if-necessary"></a>必要時，調整發行集和散發保留期限  
 異動複寫和合併式複寫使用保留期限，對交易在散發資料庫中儲存的時間及訂閱必須進行同步處理的頻率分別進行判斷。 建議在開始階段使用預設設定，但要監視您的拓撲以判斷設定是否需要調整。 例如，在合併式複寫的情況下，發行集保留期限 (預設為 14 天) 會決定中繼資料在系統資料表中的儲存時間。 如果訂閱總是在五天內同步，則考慮將設定調整為一個較低的數字，這樣可以減少中繼資料，並可能提供更好的效能。 如需詳細資訊，請參閱＜ [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)＞。  
  
## <a name="understand-how-to-modify-publications-if-application-requirements-change"></a>了解應用程式需求變更時如何修改發行集  
 建立發行集之後，可能需要加入或卸除發行項，或者變更發行集與發行項屬性。 建立發行集之後即允許多數變更。但在某些情況下，必須產生新的發行集快照集和 (或) 重新初始化訂閱到發行集。 如需詳細資訊，請參閱[變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)和[在現有發行集中新增和卸除發行項](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
## <a name="understand-how-to-make-schema-changes-if-application-requirements-change"></a>了解應用程式需求變更時如何變更結構描述  
 許多情況下，在應用程式運行後需要進行結構描述變更。 在複寫拓撲中，這些變更必須經常傳播給所有的「訂閱者」。 複寫支援對已發行物件進行大範圍的結構描述變更。 當您在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行者端針對適當已發行物件，進行下列任何一種結構描述變更時，該變更也預設傳播到所有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者：  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
## <a name="see-also"></a>另請參閱  
 [管理 &#40;複寫&#41;](../../../relational-databases/replication/administration/administration-replication.md)  
  
  
