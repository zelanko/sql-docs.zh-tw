---
title: "繼續可用性資料庫 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.availabilitygroup.resumedatamove.f1
helpviewer_keywords:
- Availability Groups [SQL Server], resuming a database
- secondary databases [SQL Server], in availability group
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], databases
ms.assetid: 20e9147b-e985-4caa-910e-fc4b38dbf9a1
caps.latest.revision: "38"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dc747146c4629010438f26c5d4a29d9c5da252d0
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="resume-an-availability-database-sql-server"></a>繼續可用性資料庫 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 您可以使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 的 PowerShell，在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]中繼續暫停的可用性資料庫。 繼續暫停的資料庫會使資料庫處於 SYNCHRONIZING 狀態。 繼續主要資料庫也會繼續因為暫停主要資料庫而暫停的任何次要資料庫。 如果在本機 (從裝載次要複本的伺服器執行個體) 暫停任何次要資料庫，該次要資料庫必須在本機繼續。 給定的次要資料庫與對應的主要資料庫都處於 SYNCHRONIZING 狀態之後，資料同步處理就會在次要資料庫上繼續。  
  
> [!NOTE]  
>  暫停和繼續 AlwaysOn 次要資料庫並不會直接影響主要資料庫的可用性， 不過暫停次要資料庫可能影響主要資料庫的備援和容錯移轉功能，直到暫停的次要資料庫繼續為止。 相反的，在資料庫鏡像中，鏡像狀態會在鏡像資料庫和主體資料庫上暫停，直到鏡像繼續為止。 暫停 AlwaysOn 主要資料庫會暫停所有對應次要資料庫上的資料移動，而且該資料庫的備援和容錯移轉功能也會停止，直到主要資料庫繼續為止。  
  
-   **開始之前：**  
  
     [必要條件](#Prerequisites)  
  
     [Security](#Security)  
  
-   **若要使用下列項目繼續次要資料庫：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
### <a name="limitations-and-restrictions"></a>限制事項  
 一旦裝載目標資料庫的複本接受 RESUME 命令之後，就會將其傳回，但繼續資料庫實際上是以非同步方式進行。  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   您必須連接到裝載要繼續之資料庫的伺服器執行個體。  
  
-   可用性群組必須在線上。  
  
-   主要資料庫必須在線上而且可用。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料庫的 ALTER 權限。  
  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要繼續次要資料庫**  
  
1.  在 [物件總管] 中，連接到裝載您要繼續資料庫之可用性複本的伺服器執行個體，然後展開伺服器樹狀目錄。  
  
2.  依序展開 [Always On 高可用性] 節點和 [可用性群組] 節點。  
  
3.  展開可用性群組。  
  
4.  展開 [可用性資料庫] 節點、以滑鼠右鍵按一下資料庫，然後按一下 [繼續進行資料移動]。  
  
5.  在 **[繼續進行資料移動]** 對話方塊中，按一下 **[確定]**。  
  
> [!NOTE]  
>  若要繼續此複本位置的其他資料庫，請針對每個資料庫重複步驟 4 和 5。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要繼續在本機上暫停的次要資料庫**  
  
1.  連接至裝載您要繼續其資料庫之次要複本的伺服器執行個體。  
  
2.  使用下列 [ALTER DATABASE](../../../t-sql/statements/alter-database-transact-sql-set-hadr.md)陳述式，繼續次要資料庫：  
  
     ALTER DATABASE *database_name* SET HADR RESUME  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **若要繼續次要資料庫**  
  
1.  切換目錄 (**cd**) 到裝載您要繼續其資料庫之複本的伺服器執行個體。 如需詳細資訊，請參閱本主題前面的＜ [必要條件](#Prerequisites)＞。  
  
2.  使用 **Resume-SqlAvailabilityDatabase** Cmdlet 繼續可用性群組。  
  
     例如，下列命令會針對可用性群組 `MyDb3` 中的可用性資料庫 `MyAg`繼續進行資料同步處理。  
  
    ```  
    Resume-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\Databases\MyDb3  
    ```  
  
    > [!NOTE]  
    >  若要檢視 Cmdlet 的語法，請在 **PowerShell 環境中使用** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Cmdlet。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)。  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [暫止可用性資料庫 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/suspend-an-availability-database-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
