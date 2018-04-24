---
title: 升級複寫的資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- merge replication database upgrades [SQL Server replication]
- replication [SQL Server], upgrading
- transactional replication, upgrading databases
- snapshot replication [SQL Server], upgrading databases
- upgrading replicated databases
ms.assetid: 9926a4f7-bcd8-4b9b-9dcf-5426a5857116
caps.latest.revision: 74
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 670b4f90c0461de12718fcf5a8cf2dfc97817b4d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="upgrade-replicated-databases"></a>升級複寫的資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] 支援從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級複寫資料庫。升級節點時，不需要停止其他節點上的活動。 請確定您遵守有關拓撲中支援之版本的規則：  
  
-   散發者可以是任何版本，只要其高於或等於發行者版本 (在許多情況下，散發者與發行者為同一執行個體)。  
  
-   發行者可以是任何版本，只要它小於或等於散發者版本即可。  
  
-   訂閱者版本視發行集的類型而定：  
  
    -   交易式發行集的訂閱者可以是兩個發行者版本內的任何版本。 例如， [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 發行者可以有 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 訂閱者，而 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 發行者可以有 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 訂閱者。  
  
    -   合併式發行集的訂閱者可以是小於或等於發行者版本的任何版本。  
  
> [!NOTE]  
>  如需本文，參閱「安裝說明」文件和《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》。 「安裝說明」文件中以粗體文字表示的文章連結，表示僅可於《線上叢書》取得的文章。 **您可以使用本[文章](https://blogs.msdn.microsoft.com/sql_server_team/upgrading-a-replication-topology-to-sql-server-2016/)**中所述的選項來設計「發行者」、「訂閱者」和「散發者」的升級策略。 
  
## <a name="run-the-log-reader-agent-for-transactional-replication-before-upgrade"></a>在升級之前執行異動複寫的記錄讀取器代理程式  
 升級 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] 之前，您必須確定所有來自已發行資料表的認可交易都已經由記錄讀取器代理程式處理過。 若要確定已經處理過所有交易，請針對每個包含交易式發行集的資料庫執行下列步驟：  
  
1.  確定已在針對資料庫執行記錄讀取器代理程式。 依預設，代理程式會持續執行。  
  
2.  停止在已發行資料表上的使用者活動。  
  
3.  提供時間讓記錄讀取器代理程式將交易複製到散發資料庫，然後再停止代理程式。  
  
4.  執行 [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) 以確認已處理所有的交易。 這個程序中所產生的結果集應該是空的。  
  
5.  執行 [sp_replflush](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) 以關閉 sp_replcmds 的連接。  
  
6.  將伺服器升級至最新版 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]。  
  
7.  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 和記錄讀取器代理程式在升級之後沒有自動啟動，則將其重新啟動。  
  
## <a name="run-agents-for-merge-replication-after-upgrade"></a>升級之後為合併式複寫執行代理程式  
 升級之後，請為每一個合併式發行集執行快照集代理程式，並為每一個訂閱執行合併代理程式來更新複寫中繼資料。 您不必套用新的快照集，因為不需要重新初始化訂閱。 升級之後，第一次執行合併代理程式時會更新訂閱中繼資料。 這表示在發行者升級時，訂閱資料庫可以持續在線上運作並保持使用中狀態。  
  
 合併式複寫會將發行集與訂閱中繼資料儲存在發行集與訂閱資料庫中的許多系統資料表內。 執行快照集代理程式會更發行集中繼資料，而執行合併代理程式會更新訂閱中繼資料。 只有要產生發行集快照集時才需要它。 如果合併式發行集使用參數化篩選，則每個資料分割也會有快照集。 您不需要更新這些分割快照集  
  
 您可以從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、複寫監視器或命令列執行代理程式。 如需如何執行快照集代理程式的詳細資訊，請參閱下列文章：  
  
-   [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)  
  
-   [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [複寫代理程式可執行檔概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
 如需如何執行合併代理程式的詳細資訊，請參閱下列文章：  
  
-   [同步處理提取訂閱](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [同步處理發送訂閱](../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
 在使用合併式複寫的拓撲中升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後，如果您想要使用新功能，請變更任何發行集的發行集相容性層級。  
  
## <a name="upgrading-to-standard-workgroup-or-express-editions"></a>升級至 Standard、Workgroup 或 Express Edition  
 從 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 的一個版本升級到另一個版本之前，請確認您目前使用的功能在您想要升級後的版本中受到支援。 如需詳細資訊，請參閱 [SQL Server 版本和支援的功能](../../sql-server/editions-and-components-of-sql-server-2017.md)中的＜複寫＞一節。  
  
## <a name="web-synchronization-for-merge-replication"></a>合併式複寫的 Web 同步處理  
 合併式複寫的 Web 同步處理選項要求，必須將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener (replisapi.dll) 複製到用於同步處理之 Internet Information Services (IIS) 伺服器上的虛擬目錄。 當您設定 Web 同步處理時，「設定 Web 同步處理精靈」會將檔案複製到虛擬目錄。 如果您升級安裝在 IIS 伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件，就必須將 replisapi.dll 從 COM 目錄手動複製到 IIS 伺服器上的虛擬目錄。 如需設定 Web 同步處理的詳細資訊，請參閱 [設定 Web 同步處理](../../relational-databases/replication/configure-web-synchronization.md)。  
  
## <a name="restoring-a-replicated-database-from-an-earlier-version"></a>從舊版還原複寫的資料庫  
 若要確定從舊版還原複寫資料庫的備份時有保留複寫設定：還原到與建立備份的伺服器和資料庫同名的伺服器和資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [管理 &#40;複寫&#41;](../../relational-databases/replication/administration/administration-replication.md)   
 [複寫回溯相容性](../../relational-databases/replication/replication-backward-compatibility.md)   
 [新功能 &#40;複寫&#41;](../../relational-databases/replication/what-s-new-replication.md)   
 [支援的版本與版本升級](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [升級 SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
  
  
