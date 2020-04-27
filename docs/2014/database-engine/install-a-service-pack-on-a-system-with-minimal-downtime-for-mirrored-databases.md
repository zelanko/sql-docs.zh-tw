---
title: 在鏡像資料庫停機時間最短的系統上安裝 Service Pack |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- hotfixes [SQL Server]
- database mirroring [SQL Server], upgrading system
- rolling upgrades [SQL Server]
- service packs [SQL Server]
- upgrading mirrored database systems
- upgrading SQL Server, mirrored databases
ms.assetid: bdc63142-027d-4ead-9d3e-147331387ef5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 821fd05e94ac820dff50bd08c70c75e7e9cc653d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62779592"
---
# <a name="install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases"></a>在鏡像資料庫停機時間最少的情況下於系統上安裝 Service Pack
  此主題描述如何在您安裝 Service Pack 和 Hotfix 時，將鏡像資料庫的停機時間減至最少。 這個程序牽涉到循序升級參與資料庫鏡像的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 執行個體。 這種形式的更新（稱為「輪流*更新*」）可將停機時間縮短為只有單一容錯移轉。 請注意，在高效能模式的工作階段中，如果鏡像伺服器與主體伺服器之間的地理位置遙遠，輪流更新可能不適合。  
  
 輪流更新是指由下列階段組成的多階段程序：  
  
-   保護您的資料。  
  
-   如果工作階段包含見證，建議您最好移除該見證。 否則，當更新鏡像伺服器執行個體時，資料庫可用性會相依於仍然連接至主體伺服器執行個體的見證。 當您移除見證之後，您可以在輪流更新期間的任何時候將它更新，避免發生資料庫停機的風險。  
  
    > [!NOTE]  
    >  如需詳細資訊，請參閱[仲裁：見證如何影響資料庫可用性 &#40;資料庫鏡像&#41;](database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)。  
  
-   如果工作階段是在高效能模式中執行，請將作業模式變更為高安全性模式。  
  
-   更新與資料庫鏡像有關的每一個伺服器執行個體。 輪流更新牽涉到將目前為鏡像伺服器的伺服器執行個體升級、手動容錯移轉它的每一個鏡像資料庫，以及將一開始為主體伺服器 (現在為新的鏡像伺服器) 的伺服器執行個體升級。 在此時，您必須繼續鏡像作業。  
  
    > [!NOTE]  
    >  在開始輪流更新之前，我們建議您至少在一個鏡像工作階段執行手動容錯移轉練習。  
  
-   在必要時還原成高效能模式。  
  
-   在必要時讓見證回到鏡像工作階段。  
  
 這裡將說明這些階段的程序。  
  
> [!IMPORTANT]  
>  伺服器執行個體可能在並行鏡像工作階段中執行不同的鏡像角色 (主體伺服器、鏡像伺服器或見證)。 在此情況下，您必須依照狀況來配合基本輪流更新程序。  
  
### <a name="to-protect-your-data-before-an-update-a-best-practice"></a>在更新之前保護資料 (最佳作法)  
  
1.  在每一個主體資料庫上執行完整資料庫備份。  
  
     **備份資料庫**  
  
    -   [&#40;SQL Server&#41;建立完整資料庫備份](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)。  
  
2.  在每一個主體資料庫上執行 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 命令。  
  
### <a name="to-remove-a-witness-from-a-session"></a>從工作階段中移除見證  
  
1.  如果鏡像工作階段牽涉到見證，我們建議您在執行輪流更新之前，最好先移除該見證。  
  
     **移除見證**  
  
    -   [從資料庫鏡像工作階段移除見證 &#40;SQL Server&#41;](database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
### <a name="to-change-a-session-from-high-performance-mode-to-high-safety-mode"></a>將工作階段從高效能模式變更為高安全性模式  
  
1.  如果鏡像工作階段是在高效能模式下執行，請在執行輪流更新之前，將作業模式變更為高安全性模式，而沒有自動容錯移轉。 請使用下列其中一個方法：  
  
    -   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中：使用 [資料庫屬性]**** 對話方塊的[鏡像頁面](../relational-databases/databases/database-properties-mirroring-page.md)，將 [作業模式]**** 選項變更為 [不具有自動容錯移轉的高安全性 (同步)]****。 如需如何存取此頁面的資訊，請參閱[啟動設定資料庫鏡像安全性精靈 &#40;SQL Server Management Studio&#41;](database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)。  
  
    -   在 [!INCLUDE[tsql](../includes/tsql-md.md)] 中：將交易安全性設定為 FULL。 如需詳細資訊，請參閱[在資料庫鏡像工作階段中變更交易安全性 &#40;Transact-SQL&#41;](database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)。  
  
### <a name="to-perform-the-rolling-update"></a>若要執行輪流更新  
  
1.  若要讓停機時間減至最少，我們建議您採取以下作法：在所有鏡像工作階段中更新目前為鏡像伺服器的任何鏡像夥伴伺服器，藉以開始輪流更新。 您在此時可能必須更新多個伺服器執行個體。  
  
    > [!NOTE]  
    >  您可以在輪流更新程序的任何時間更新見證。 例如，如果伺服器執行個體在工作階段 1 為鏡像伺服器，而在工作階段 2 為見證，您可以立刻更新此伺服器執行個體。  
  
     要更新的伺服器執行個體首先取決於鏡像工作階段的目前組態，如下面所述：  
  
    -   如果有任何伺服器執行個體在所有鏡像工作階段中已經是鏡像伺服器，請在該伺服器執行個體上安裝 Service Pack 或 Hotfix。  
  
    -   如果所有的伺服器執行個體目前在任何鏡像工作階段中都是主體伺服器，請先選取一個伺服器執行個體來更新。 然後，手動容錯移轉它的每一個主體資料庫，並透過安裝 Service Pack 或 Hotfix 來更新該伺服器執行個體。  
  
     在更新之後，伺服器執行個體會自動重新加入它的每一個鏡像工作階段。  
  
     **執行手動容錯移轉**  
  
    -   [手動容錯移轉資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [&#40;transact-sql&#41;手動故障切換資料庫鏡像會話](database-mirroring/manually-fail-over-a-database-mirroring-session-transact-sql.md)。  
  
     如需手動容錯移轉如何運作的資訊，請參閱[資料庫鏡像工作階段期間的角色切換 &#40;SQL Server&#41;](database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)。  
  
2.  請針對剛剛更新鏡像伺服器執行個體的每一個鏡像工作階段，等候此工作階段同步處理。 然後，連接到主體伺服器執行個體，並手動容錯移轉工作階段。 在容錯移轉時，更新的伺服器執行個體會變成該工作階段的主體伺服器，而之前的主體伺服器會變成鏡像伺服器。  
  
     這個步驟的目標是要讓另一個伺服器執行個體在當做夥伴伺服器的每一個鏡像工作階段中變成鏡像伺服器。  
  
3.  在您容錯移轉之後，我們建議您在主體資料庫上執行 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 命令。  
  
4.  如果有任何伺服器執行個體目前在當做夥伴伺服器的所有鏡像工作階段中為鏡像伺服器，請在該伺服器執行個體上安裝 Service Pack 或 Hotfix。 您在此時可能必須更新多部伺服器。  
  
    > [!IMPORTANT]  
    >  在複雜鏡像組態中，某些伺服器執行個體在一或多個鏡像工作階段中可能仍然是原始的主體伺服器。 針對這些伺服器實例重複步驟2-4，直到所有相關的實例都更新為止。  
  
5.  繼續鏡像工作階段。  
  
    > [!NOTE]  
    >  要等到更新見證之後，自動容錯移轉才能運作。  
  
6.  如果有任何其餘的伺服器執行個體在所有鏡像工作階段中為見證，請在該伺服器執行個體上安裝 Service Pack 或 Hotfix。 在更新之後，見證會重新加入鏡像工作階段，而自動容錯移轉可再度運作。 您在此時可能必須更新多部伺服器。  
  
### <a name="to-return-a-session-to-high-performance-mode"></a>讓工作階段回到高效能模式  
  
1.  您可以選擇使用下列其中一個方法來回到高效能模式：  
  
    -   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中：使用 [資料庫屬性]**** 對話方塊的[鏡像頁面](../relational-databases/databases/database-properties-mirroring-page.md)，將 [作業模式]**** 選項變更為 [高效能 (非同步)]****。  
  
    -   在[!INCLUDE[tsql](../includes/tsql-md.md)]中：使用[ALTER database](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)將交易安全性設定為 OFF。  
  
### <a name="to-return-a-witness-to-a-mirroring-session"></a>讓見證回到鏡像工作階段  
  
1.  您可以選擇在高安全性模式下，重新建立每一個鏡像工作階段的見證。  
  
     **若要重新建立見證**  
  
    -   [新增或取代資料庫鏡像見證 &#40;SQL Server Management Studio&#41;](database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
    -   [使用 Windows 驗證新增資料庫鏡像見證 &#40;Transact-SQL&#41;](database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE 資料庫鏡像 &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [資料庫鏡像 &#40;SQL Server&#41;](database-mirroring/database-mirroring-sql-server.md)   
 [資料庫鏡像作業模式](database-mirroring/database-mirroring-operating-modes.md)   
 [資料庫鏡像會話期間的角色切換 &#40;SQL Server&#41;](database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [啟動資料庫鏡像監視器 &#40;SQL Server Management Studio&#41;](database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [檢視鏡像資料庫的狀態 &#40;SQL Server Management Studio&#41;](database-mirroring/view-the-state-of-a-mirrored-database-sql-server-management-studio.md)  
  
  
