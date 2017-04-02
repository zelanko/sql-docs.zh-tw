---
title: "執行可用性群組的已規劃手動容錯移轉 (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.availabilitygroup.manualfailover.f1"
helpviewer_keywords: 
  - "可用性群組 [SQL Server], 容錯移轉"
  - "容錯移轉 [SQL Server], AlwaysOn 可用性群組"
ms.assetid: 419f655d-3f9a-4e7d-90b9-f0bab47b3178
caps.latest.revision: 36
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 36
---
# 執行可用性群組的已規劃手動容錯移轉 (SQL Server)
  本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中的 PowerShell，在不遺失資料的情況下針對 AlwaysOn 可用性群組執行手動容錯移轉 (「規劃的手動容錯移轉」)。 可用性群組會在可用性複本層級容錯移轉。 已規劃的手動容錯移轉就像任何 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 容錯移轉一樣，會將次要複本轉換成主要角色，同時將先前的主要複本轉換成次要角色。  
  
 只有在主要複本和目標次要複本在同步認可模式下執行，而且目前經過同步處理之後才支援的已規劃手動容錯移轉，會保留聯結至目標次要複本上可用性群組之次要資料庫中的所有資料。 一旦之前的主要複本轉換成次要角色之後，其資料庫會變成次要資料庫，並開始與新的主要資料庫進行同步處理。 在將它們全部轉換成 SYNCHRONIZED 狀態之後，新的次要複本就會變成有資格當做未來已規劃之手動容錯移轉的目標。  
  
> [!NOTE]  
>  如果次要和主要複本都設定成自動容錯移轉模式，一旦次要複本經過同步處理之後，也可以當做自動容錯移轉的目標。 如需詳細資訊，請參閱[可用性模式 &#40;AlwaysOn 可用性群組&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)。  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [必要條件和限制](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目手動容錯移轉可用性群組：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **後續操作︰**[手動容錯移轉可用性群組之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   目標次要複本接受命令之後，容錯移轉命令就會傳回。 不過，在可用性群組完成容錯移轉之後，會以非同步方式復原資料庫。  
  
-   容錯移轉時，可能不會保留可用性群組內跨資料庫的一致性。  
  
    > [!NOTE]  
    >  跨資料庫和分散式交易的支援會因 SQL Server 和作業系統版本而不同。 如需詳細資訊，請參閱 [AlwaysOn 可用性群組和資料庫鏡像的跨資料庫交易和分散式交易 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions - always on availability and database mirroring.md)。  
  
###  <a name="Prerequisites"></a> 必要條件和限制  
  
-   目標次要複本和主要複本都必須在同步認可可用性模式下執行。  
  
-   目標次要複本目前必須與主要複本進行同步處理。 這需要此次要複本上的所有次要資料庫都必須已經聯結至可用性群組，並與其對應的主要資料庫進行同步處理 (亦即，本機次要資料庫必須是 SYNCHRONIZED)。  
  
    > [!TIP]  
    >  若要判斷次要複本的容錯移轉整備，請查詢 [sys.dm_hadr_database_cluster_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md) 動態管理檢視中的 **is_failover_ready** 資料行，或是查看 [AlwaysOn 群組儀表板](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)的 [容錯移轉整備] 資料行。  
  
-   只有在目標次要複本上才支援這個工作。 您必須連接到裝載目標次要複本的伺服器執行個體。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **手動容錯移轉可用性群組**  
  
1.  在 [物件總管] 中，連接至裝載需要容錯移轉之可用性群組次要複本的伺服器執行個體，然後展開伺服器樹狀目錄。  
  
2.  依序展開 [Always On 高可用性] 節點和 [可用性群組] 節點。  
  
3.  以滑鼠右鍵按一下要容錯移轉的可用性群組，然後選取 [容錯移轉] 命令。  
  
4.  這會啟動「容錯移轉可用性群組精靈」。 如需詳細資訊，請參閱[使用容錯移轉可用性群組精靈 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **手動容錯移轉可用性群組**  
  
1.  連接到裝載目標次要複本的伺服器執行個體。  
  
2.  使用 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 陳述式，如下所示：  
  
     ALTER AVAILABILITY GROUP *group_name* FAILOVER  
  
     其中 *group_name* 是可用性群組的名稱。  
  
     下列範例會將 *MyAg* 可用性群組手動容錯移轉到連接的次要複本。  
  
    ```  
    ALTER AVAILABILITY GROUP MyAg FAILOVER;  
    ```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **手動容錯移轉可用性群組**  
  
1.  將目錄 (**cd**) 變更為裝載目標次要複本的伺服器執行個體。  
  
2.  使用 **Switch-SqlAvailabilityGroup** Cmdlet。  
  
    > [!NOTE]  
    >  若要檢視 Cmdlet 的語法，請在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] PowerShell 環境中使用 **Get-Help** Cmdlet。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)。  
  
     下列範例會將 *MyAg* 可用性群組手動容錯移轉到位於指定路徑的次要複本。  
  
    ```  
    Switch-SqlAvailabilityGroup -Path SQLSERVER:\Sql\SecondaryServer\InstanceName\AvailabilityGroups\MyAg  
    ```  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [取得 SQL Server PowerShell 說明](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="FollowUp"></a> 追蹤：手動容錯移轉可用性群組之後  
 如果您容錯移轉可用性群組的 [!INCLUDE[ssFosAuto](../../../includes/ssfosauto-md.md)] 外部：調整 WSFC 節點的仲裁投票，以反映您的新可用性群組組態。 如需詳細資訊，請參閱 [SQL Server 的 Windows Server 容錯移轉叢集 &#40;WSFC&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)。  
  
## 另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [容錯移轉及容錯移轉模式 &#40;AlwaysOn 可用性群組&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [執行可用性群組的強制手動容錯移轉 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
  