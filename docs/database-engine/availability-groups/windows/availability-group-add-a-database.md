---
title: "將資料庫新增至可用性群組 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 2a54eef8-9e8e-4e04-909c-6970112d55cc
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2be0fc9914446c02b4a6129d232cf631fba67bfb
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="availability-group---add-a-database"></a>可用性群組 - 新增資料庫
  本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]或 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中的 PowerShell，將資料庫加入 AlwaysOn 可用性群組中。  
  
-   **開始之前：**  
  
     [必要條件和限制](#Prerequisites)  
  
     [Permissions](#Permissions)  
  
-   **若要使用下列項目，將資料庫加入至可用性群組：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件和限制  
  
-   您必須連接到裝載主要複本的伺服器執行個體。  
  
-   資料庫必須位於裝載主要複本的伺服器執行個體上，且符合可用性資料庫的必要條件和限制。 如需詳細資訊，請參閱 [AlwaysOn 可用性群組的必要條件、限制和建議 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)設定伺服器執行個體時常見的問題。  
  
###  <a name="Security"></a> 安全性  
  
###  <a name="Permissions"></a> Permissions  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要將資料庫加入至可用性群組**  
  
1.  在 [物件總管] 中，連接到裝載主要複本的伺服器執行個體，然後展開伺服器樹狀目錄。  
  
2.  依序展開 [AlwaysOn 高可用性] 節點和 [可用性群組] 節點。  
  
3.  以滑鼠右鍵按一下可用性群組，然後選取下列其中一個命令：  
  
    -   若要啟動「將資料庫加入至可用性群組精靈」，選取 **[加入資料庫]** 命令。 如需詳細資訊，請參閱[使用 [將資料庫加入至可用性群組精靈] &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)。  
  
    -   若要在 **[可用性群組屬性]** 對話方塊中指定一個或多個資料庫來加入這些資料庫，選取 **[屬性]** 命令。 加入資料庫的步驟如下所示：  
  
        1.  在 **[可用性資料庫]** 窗格中，按一下 **[加入]** 按鈕。 這樣會建立並選取一個空白資料庫欄位。  
  
        2.  輸入符合可用性資料庫必要條件之資料庫的名稱。  
  
         若要加入另一個資料庫，請重複上述步驟。 當您指定好資料庫時，按一下 **[確定]** 以完成該作業。  
  
         使用 **[可用性群組屬性]** 對話方塊將資料庫加入至可用性群組之後，您需要在裝載次要複本的每個伺服器執行個體上設定對應的次要資料庫。 如需詳細資訊，請參閱 [於 AlwaysOn 次要資料庫啟動資料移動 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要將資料庫加入至可用性群組**  
  
1.  連接到裝載主要複本的伺服器執行個體。  
  
2.  使用 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 陳述式，如下所示：  
  
     ALTER AVAILABILITY GROUP *group_name* ADD DATABASE *database_name* [,...*n*]  
  
     其中 *group_name* 是可用性群組的名稱，而 *database_name* 是要加入群組中之資料庫的名稱。  
  
     下列範例會將 *MyDb3* 資料庫加入 *MyAG* 可用性群組中。  
  
    ```  
    -- Connect to the server instance that hosts the primary replica.  
    -- Add an existing database to the availability group.  
    ALTER AVAILABILITY GROUP MyAG ADD DATABASE MyDb3;  
    GO  
    ```  
  
3.  將資料庫加入至可用性群組之後，您需要在裝載次要複本的每個伺服器執行個體上設定對應的次要資料庫。 如需詳細資訊，請參閱 [於 AlwaysOn 次要資料庫啟動資料移動 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **若要將資料庫加入至可用性群組**  
  
1.  將目錄 (**cd**) 變更為裝載主要複本的伺服器執行個體。  
  
2.  使用 **Add-SqlAvailabilityDatabase** Cmdlet。  
  
     例如，下列命令會將次要資料庫 `MyDd` 加入 `MyAG` 可用性群組中，而其主要複本是由 `PrimaryServer\InstanceName`裝載。  
  
    ```  
  
    Add-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `   
    -Database "MyDb"  
    ```  
  
    > [!NOTE]  
    >  若要檢視 Cmdlet 的語法，請在 **PowerShell 環境中使用** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Cmdlet。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)。  
  
3.  將資料庫加入至可用性群組之後，您需要在裝載次要複本的每個伺服器執行個體上設定對應的次要資料庫。 如需詳細資訊，請參閱 [於 AlwaysOn 次要資料庫啟動資料移動 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
 如需完整範例，請參閱下面的 [範例 (PowerShell)](#PSExample)。  
  
###  <a name="PSExample"></a> 範例 (PowerShell)  
 下列範例示範此完整程序：根據裝載可用性群組之主要複本的伺服器執行個體上的資料庫準備次要資料庫、將資料庫加入至可用性群組 (做為主要資料庫)，然後將次要資料庫聯結至可用性群組。 首先，此範例會備份資料庫及其交易記錄。 然後，此範例會將資料庫和記錄備份還原至裝載次要複本的伺服器執行個體。  
  
 此範例會呼叫 **Add-SqlAvailabilityDatabase** 兩次：第一次是針對主要複本呼叫，以便將資料庫加入可用性群組中，然後再針對次要複本呼叫，以便將該複本的次要資料庫聯結至可用性群組。 如果您有多個次要複本，請還原並聯結每個次要複本的次要資料庫。  
  
```  
$DatabaseBackupFile = "\\share\backups\MyDatabase.bak"  
$LogBackupFile = "\\share\backups\MyDatabase.trn"  
$MyAgPrimaryPath = "SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg"  
$MyAgSecondaryPath = "SQLSERVER:\SQL\SecondaryServer\InstanceName\AvailabilityGroups\MyAg"  
  
Backup-SqlDatabase -Database "MyDatabase" -BackupFile $DatabaseBackupFile -ServerInstance "PrimaryServer\InstanceName"  
Backup-SqlDatabase -Database "MyDatabase" -BackupFile $LogBackupFile -ServerInstance "PrimaryServer\InstanceName" -BackupAction 'Log'  
  
Restore-SqlDatabase -Database "MyDatabase" -BackupFile $DatabaseBackupFile -ServerInstance "SecondaryServer\InstanceName" -NoRecovery  
Restore-SqlDatabase -Database "MyDatabase" -BackupFile $LogBackupFile -ServerInstance "SecondaryServer\InstanceName" -RestoreAction 'Log' -NoRecovery  
  
Add-SqlAvailabilityDatabase -Path $MyAgPrimaryPath -Database "MyDatabase"  
Add-SqlAvailabilityDatabase -Path $MyAgSecondaryPath -Database "MyDatabase"  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [建立及設定可用性群組 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)   
 [監視可用性群組 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  

