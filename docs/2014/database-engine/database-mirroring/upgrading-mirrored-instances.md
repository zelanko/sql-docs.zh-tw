---
title: 升級伺服器執行個體時，縮短停機時間的鏡像資料庫 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading SQL Server, rolling upgrade of mirrored databases
- database mirroring [SQL Server], upgrading system
- rolling upgrades [SQL Server]
ms.assetid: 0e73bd23-497d-42f1-9e81-8d5314bcd597
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 857e18b1b956d3d8c9d2fc4c5692dbf022bf85fe
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509423"
---
# <a name="minimize-downtime-for-mirrored-databases-when-upgrading-server-instances"></a>在升級伺服器執行個體時將鏡像資料庫的停機時間減至最少
  升級伺服器執行個體時[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，您也可以執行的循序升級，只有單一手動容錯移轉來減少每個鏡像資料庫的停機時間稱為*輪流升級*。 輪流升級是一種多階段程序，其最簡單的形式包括升級目前在鏡像工作階段中當做鏡像伺服器的伺服器執行個體，然後手動容錯移轉鏡像資料庫、升級之前的主體伺服器，以及繼續進行鏡像。 實際上，確切的程序會取決於作業模式以及在您要升級之伺服器執行個體上執行的鏡像工作階段數目和配置而定。  
  
> [!NOTE]  
>  執行輪流升級，以安裝 service pack 或 hotfix 的詳細資訊，請參閱[上安裝 Service Pack 系統 with Minimal Downtime for Mirrored](../install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases.md)。  
  
 **建議的準備事項 （最佳做法）**  
  
 開始輪流升級之前，我們建議您：  
  
1.  至少在其中一個鏡像工作階段上執行手動容錯移轉練習：  
  
    -   [手動容錯移轉資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [手動容錯移轉資料庫鏡像工作階段 &#40;Transact-SQL&#41;](manually-fail-over-a-database-mirroring-session-transact-sql.md)。  
  
    > [!NOTE]  
    >  如需手動容錯移轉如何運作的資訊，請參閱[資料庫鏡像工作階段期間的角色切換 &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)。  
  
2.  保護您的資料：  
  
    1.  在每個主體資料庫上執行完整資料庫備份：  
  
         [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)。  
  
    2.  在每一個主體資料庫上執行 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 命令。  
  
 **輪流升級階段**  
  
 輪流升級的特定步驟會因鏡像組態的作業模式而不同。 不過，基本階段都是相同的。  
  
> [!NOTE]  
>  如需作業模式的資訊，請參閱 [資料庫鏡像作業模式](database-mirroring-operating-modes.md)。  
  
 下圖是一張流程圖，其中針對每個作業模式顯示輪流升級的基本階段。 對應的程序將在該圖之後描述。  
  
 ![顯示輪流升級步驟的流程圖](../media/dbm-rolling-upgrade.gif "顯示輪流升級步驟的流程圖")  
  
> [!IMPORTANT]  
>  伺服器執行個體可能在並行鏡像工作階段中執行不同的鏡像角色 (主體伺服器、鏡像伺服器或見證)。 在此情況下，您必須依照狀況來配合基本輪流升級程序。 如需詳細資訊，請參閱 [資料庫鏡像工作階段期間的角色切換 &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)版本都可使用見證伺服器執行個體。  
  
### <a name="to-change-a-session-from-high-performance-mode-to-high-safety-mode"></a>將工作階段從高效能模式變更為高安全性模式  
  
1.  如果鏡像工作階段是在高效能模式下執行，請在執行輪流升級之前，將作業模式變更為高安全性模式，而沒有自動容錯移轉。  
  
    > [!IMPORTANT]  
    >  如果鏡像伺服器與主體伺服器之間的地理位置遙遠，輪流升級可能不適合。  
  
    -   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中：變更**作業模式**選項設定為**不具有自動容錯移轉 （同步） 的高安全性**利用[鏡像頁面](../../relational-databases/databases/database-properties-mirroring-page.md)的**資料庫屬性** 對話方塊。 如需如何存取此頁面的資訊，請參閱[啟動設定資料庫鏡像安全性精靈 &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)。  
  
    -   在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中：將交易安全性設定為 FULL。 如需詳細資訊，請參閱[在資料庫鏡像工作階段中變更交易安全性 &#40;Transact-SQL&#41;](change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)  
  
### <a name="to-remove-a-witness-from-a-session"></a>從工作階段中移除見證  
  
1.  如果鏡像工作階段牽涉到見證，我們建議您在執行輪流升級之前，最好先移除該見證。 否則，當升級鏡像伺服器執行個體時，資料庫可用性會相依於仍然連接至主體伺服器執行個體的見證。 當您移除見證之後，您可以在輪流升級期間的任何時候將它升級，避免發生資料庫停機的風險。  
  
    > [!NOTE]  
    >  如需詳細資訊，請參閱[仲裁：見證如何影響資料庫可用性&#40;資料庫鏡像&#41;](quorum-how-a-witness-affects-database-availability-database-mirroring.md)。  
  
    -   [從資料庫鏡像工作階段移除見證 &#40;SQL Server&#41;](remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
### <a name="to-perform-the-rolling-upgrade"></a>執行輪流升級  
  
1.  若要讓停機時間減至最少，我們建議您採取以下作法：在所有鏡像工作階段中更新目前為鏡像伺服器的任何鏡像夥伴伺服器，以開始輪流升級。 您在此時可能必須更新多個伺服器執行個體。  
  
    > [!NOTE]  
    >  您可以在輪流升級程序的任何時間升級見證。 例如，如果伺服器執行個體在工作階段 1 為鏡像伺服器，而在工作階段 2 為見證，您可以立刻升級此伺服器執行個體。  
  
     要升級的伺服器執行個體首先取決於鏡像工作階段的目前組態，如下面所述：  
  
    -   如果有任何伺服器執行個體在所有鏡像工作階段中已經是鏡像伺服器，請將此伺服器執行個體升級為新的版本。  
  
    -   如果所有的伺服器執行個體目前在任何鏡像工作階段中為主體伺服器，請先選取一個伺服器執行個體來升級。 然後，手動容錯移轉它的每一個主體資料庫，並升級該伺服器執行個體。  
  
     在升級之後，伺服器執行個體會自動重新加入它的每一個鏡像工作階段。  
  
2.  請針對剛剛升級鏡像伺服器執行個體的每一個鏡像工作階段，等候此工作階段同步處理。 然後，連接到主體伺服器執行個體，並手動容錯移轉工作階段。 在容錯移轉時，升級的伺服器執行個體會變成該工作階段的主體伺服器，而之前的主體伺服器會變成鏡像伺服器。  
  
     這個步驟的目標是要讓另一個伺服器執行個體在當做夥伴伺服器的每一個鏡像工作階段中變成鏡像伺服器。  
  
     **在容錯移轉至升級的伺服器執行個體之後的限制**  
  
     當您從舊版伺服器執行個體容錯移轉至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器執行個體之後，資料庫工作階段會暫停。 要等到其他夥伴伺服器升級之後，才會繼續此工作階段。 但是，主體伺服器仍然接受連接，並允許在主體資料庫上進行資料存取和修改。  
  
    > [!NOTE]  
    >  建立新的鏡像工作階段需要所有的伺服器執行個體都執行相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本。  
  
3.  容錯移轉之後，我們建議您執行[DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) theprincipal 資料庫命令。  
  
4.  如果有任何伺服器執行個體目前在當做夥伴伺服器的所有鏡像工作階段中為鏡像伺服器，請將它升級。 您在此時可能必須更新多部伺服器。  
  
    > [!IMPORTANT]  
    >  在複雜鏡像組態中，某些伺服器執行個體在一或多個鏡像工作階段中可能仍然是原始的主體伺服器。 請針對這些伺服器執行個體重複步驟 2-4，直到相關的所有執行個體都已升級為止。  
  
5.  繼續鏡像工作階段。  
  
    > [!NOTE]  
    >  要等到升級見證而且加回鏡像工作階段之後，自動容錯移轉才能運作。  
  
6.  如果有任何其餘的伺服器執行個體在所有鏡像工作階段中為見證，請將它升級。 在升級之後，見證會重新加入鏡像工作階段，而自動容錯移轉可再度運作。 您在此時可能必須更新多部伺服器。  
  
### <a name="to-return-a-session-to-high-performance-mode"></a>讓工作階段回到高效能模式  
  
1.  您可以選擇使用下列其中一個方法來回到高效能模式：  
  
    -   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中：變更**作業模式**選項設定為**高效能 （非同步）** 利用[鏡像頁面](../../relational-databases/databases/database-properties-mirroring-page.md)的**資料庫屬性** 對話方塊。  
  
    -   在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中：使用[ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)將交易安全性設定為 OFF。  
  
### <a name="to-add-a-witness-back-into-a-mirroring-session"></a>若要將見證加回鏡像工作階段  
  
1.  您可以選擇在高安全性模式下，重新建立每一個鏡像工作階段的見證。  
  
     **返回見證**  
  
    -   [新增或取代資料庫鏡像見證 &#40;SQL Server Management Studio&#41;](add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
    -   [使用 Windows 驗證新增資料庫鏡像見證 &#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE 資料庫鏡像 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [檢視鏡像資料庫的狀態 &#40;SQL Server Management Studio&#41;](view-the-state-of-a-mirrored-database-sql-server-management-studio.md)   
 [資料庫鏡像 &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [在最短停機時間的系統上安裝 Service Pack，為鏡像資料庫](../install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases.md)   
 [資料庫鏡像工作階段期間的角色切換 &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)   
 [在資料庫鏡像工作階段中強制服務 &#40;Transact-SQL&#41;](force-service-in-a-database-mirroring-session-transact-sql.md)   
 [啟動資料庫鏡像監視器 &#40;SQL Server Management Studio&#41;](start-database-mirroring-monitor-sql-server-management-studio.md)   
 [資料庫鏡像作業模式](database-mirroring-operating-modes.md)  
  
  
