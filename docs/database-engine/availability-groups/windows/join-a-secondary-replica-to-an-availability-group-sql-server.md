---
title: "將次要複本聯結至可用性群組 (SQL Server) | Microsoft Docs"
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
  - "sql13.swb.availabilitygroup.joinreplica.f1"
helpviewer_keywords: 
  - "可用性群組 [SQL Server], 可用性複本"
  - "可用性群組 [SQL Server], 聯結"
  - "可用性群組 [SQL Server], 設定"
ms.assetid: e5bd2489-097a-490e-8ea1-34fe48378ad1
caps.latest.revision: 41
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 41
---
# 將次要複本聯結至可用性群組 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中的 PowerShell，將次要複本聯結至 Always On 可用性群組。 當次要複本加入至 Always On 可用性群組之後，此次要複本必須聯結至可用性群組。 聯結複本作業必須在裝載次要複本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上執行。  
  
-   **開始之前：**  
  
     [必要條件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來準備次要資料庫：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **待處理：**[設定次要資料庫](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   可用性群組的主要複本目前必須在線上。  
  
-   您必須連接到伺服器執行個體，此執行個體會裝載尚未加入至可用性群組的次要複本。  
  
-   本機伺服器執行個體必須能夠連接到裝載主要複本之伺服器執行個體的資料庫鏡像端點。  
  
> [!IMPORTANT]  
>  如果不符合任何先決條件，聯結作業會失敗。 聯結嘗試失敗之後，您可能需要連接至裝載主要複本的伺服器執行個體，以移除及重新加入次要複本，然後將其聯結至可用性群組。 如需詳細資訊，請參閱[將次要複本從可用性群組移除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md) 和[將次要複本加入至可用性群組 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要將可用性複本聯結至可用性群組**  
  
1.  在 [物件總管] 中，連接到裝載次要複本的伺服器執行個體，然後按一下伺服器名稱以展開伺服器樹狀目錄。  
  
2.  依序展開 [Always On 高可用性] 節點和 [可用性群組] 節點。  
  
3.  選取所連接之次要複本的可用性群組。  
  
4.  以滑鼠右鍵按一下次要複本，然後按一下 [加入可用性群組]。  
  
5.  這會開啟 **[將複本加入至可用性群組]** 對話方塊。  
  
6.  若要將次要複本聯結至可用性群組，請按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要將可用性複本聯結至可用性群組**  
  
1.  連接到裝載次要複本的伺服器執行個體。  
  
2.  使用 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 陳述式，如下所示：  
  
     ALTER AVAILABILITY GROUP \<群組名稱> JOIN  
  
     其中 \<群組名稱> 是可用性群組的名稱。  
  
     下列範例會將次要複本加入至 `MyAG` 可用性群組。  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    ```  
  
    > [!NOTE]  
    >  若要查看內容中使用的這個 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式，請參閱[建立可用性群組和 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)。  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **若要將可用性複本聯結至可用性群組**  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 提供者內：  
  
1.  切換目錄 (**cd**) 到裝載次要複本的伺服器執行個體。  
  
2.  使用可用性群組的名稱執行 **Join-SqlAvailabilityGroup** Cmdlet，將次要複本聯結至可用性群組。  
  
     例如，下列命令會將位於指定路徑之伺服器執行個體所裝載的次要複本聯結至名為 `MyAg` 的可用性群組。  這個伺服器執行個體必須裝載這個可用性群組中的次要複本。  
  
    ```  
    Join-SqlAvailabilityGroup -Path SQLSERVER:\SQL\SecondaryServer\InstanceName -Name 'MyAg'  
    ```  
  
    > [!NOTE]  
    >  若要檢視 Cmdlet 的語法，請在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 環境中使用 **Get-Help** Cmdlet。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)。  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> 待處理：設定次要資料庫  
 對於可用性群組中的每個資料庫而言，您需要在裝載次要複本的伺服器執行個體上擁有次要資料庫。 在您將次要複本加入可用性群組之前或之後，您都可以設定次要資料庫，如下所示：  
  
1.  針對每一個還原作業使用 RESTORE WITH NORECOVERY，將每一個主要資料庫的最新資料庫和記錄備份還原到裝載次要複本的伺服器執行個體上。 如需詳細資訊，請參閱[針對可用性群組手動準備次要資料庫 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)。  
  
2.  將每一個次要資料庫加入可用性群組。 如需詳細資訊，請參閱[將次要資料庫聯結至可用性群組 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)。  
  
## 另請參閱  
 [建立及設定可用性群組 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [Always On 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [疑難排解 Always On 可用性群組組態 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  