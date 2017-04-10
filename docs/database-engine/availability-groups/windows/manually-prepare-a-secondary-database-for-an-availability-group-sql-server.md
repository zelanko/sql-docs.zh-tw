---
title: "針對可用性群組手動準備次要資料庫 (SQL Server) | Microsoft Docs"
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
  - "sql13.swb.availabilitygroup.preparedbs.f1"
  - "sql13.swb.availabilitygroup.configsecondarydbs.f1"
helpviewer_keywords: 
  - "次要資料庫 [SQL Server], 在可用性群組中"
  - "次要資料庫 [SQL Server]"
  - "可用性群組 [SQL Server], 設定"
  - "可用性群組 [SQL Server], 資料庫"
ms.assetid: 9f2feb3c-ea9b-4992-8202-2aeed4f9a6dd
caps.latest.revision: 47
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 47
---
# 針對可用性群組手動準備次要資料庫 (SQL Server)
  本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 PowerShell，在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中準備 AlwaysOn 可用性群組的次要資料庫。 準備次要資料庫需要進行兩個步驟：(1) 使用 RESTORE WITH NORECOVERY，將主要資料庫的最新資料庫備份和後續記錄備份還原至裝載次要複本的每個伺服器執行個體，以及 (2) 將還原的資料庫聯結至可用性群組。  
  
> [!TIP]  
>  如果您有現有的記錄傳送組態，您可能可以將記錄傳送主要資料庫連同其一個或多個次要資料庫，一併轉換成 AlwaysOn 主要資料庫和一個或多個 AlwaysOn 次要資料庫。 如需詳細資訊，請參閱[從記錄傳送移轉至 AlwaysOn 可用性群組的必要條件 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs migrating log shipping to always on availability groups.md)。  
  
-   **開始之前：**  
  
     [必要條件和限制](#Prerequisites)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來準備次要資料庫：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [相關備份和還原工作](#RelatedTasks)  
  
-   **後續操作**：[準備次要資料庫之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件和限制  
  
-   請確定您規劃放置資料庫的系統已配備具有足夠空間來保存次要資料庫的磁碟機。  
  
-   次要資料庫的名稱必須與主要資料庫的名稱相同。  
  
-   針對每個還原作業使用 RESTORE WITH NORECOVERY。  
  
-   如果次要資料庫與主要資料庫必須位於不同的檔案路徑 (包括磁碟機代號)，還原命令也必須針對每個資料庫檔案使用 WITH MOVE 選項，以便將它們指定為次要資料庫的路徑。  
  
-   如果您是按檔案群組逐一還原資料庫，請務必還原整個資料庫。  
  
-   還原資料庫之後，您必須還原 (WITH NORECOVERY) 自從上次還原資料備份以來所建立的每個記錄備份。  
  
###  <a name="Recommendations"></a> 建議  
  
-   在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的獨立執行個體上，我們建議，給定次要資料庫的檔案路徑 (包括磁碟機代號) 盡可能與對應主要資料庫的路徑完全相同。 這是因為，如果您在建立次要資料庫時移動資料庫檔案，之後在次要資料庫上加入檔案的作業可能會失敗，而且導致次要資料庫暫停。  
  
-   準備次要資料庫之前，我們強烈建議您針對可用性群組中的資料庫暫停排程的記錄備份，直到次要複本的初始化完成為止。  
  
###  <a name="Security"></a> 安全性  
 備份資料庫時， [TRUSTWORTHY 資料庫屬性](../../../relational-databases/security/trustworthy-database-property.md) 將設為 OFF。 因此，新還原資料庫上的 TRUSTWORTHY 一律為 OFF。  
  
####  <a name="Permissions"></a> Permissions  
 BACKUP DATABASE 和 BACKUP LOG 權限預設為**sysadmin** 固定伺服器角色以及 **db_owner** 和 **db_backupoperator** 固定資料庫角色的成員。 如需詳細資訊，請參閱 [BACKUP &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-transact-sql.md)。  
  
 當還原的資料庫不存在伺服器執行個體上時，RESTORE 陳述式就需要 CREATE DATABASE 權限。 如需詳細資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
> [!NOTE]  
>  如果主控主要複本的伺服器執行個體和主控次要複本的每個執行個體之間的備份和還原檔案路徑相同，則您應該可以使用[新增可用性群組精靈](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)、[將複本加入至可用性群組精靈](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)或[將資料庫加入至可用性群組精靈](../../../database-engine/availability-groups/windows/use-the-add-database-to-availability-group-wizard-sql-server-management-studio.md)建立次要資料庫。  
  
 **若要準備次要資料庫**  
  
1.  除非您已經擁有主要資料庫的最新資料庫備份，否則請建立新的完整或差異資料庫備份。 最佳作法是將這個備份和任何後續記錄備份放置於建議的網路共用。  
  
2.  至少建立主要資料庫的一個新記錄備份。  
  
3.  在裝載次要複本的伺服器執行個體上，還原主要資料庫的完整資料庫備份 (並選擇性地還原差異備份)，接著還原任何後續記錄備份。  
  
     在 [RESTORE DATABASE 選項] 頁面上，選取 [讓資料庫保持不運作，且不回復未認可的交易。可以還原其他交易記錄。(RESTORE WITH NORECOVERY)]。  
  
     如果主要資料庫與次要資料庫的檔案路徑不同 (例如，主要資料庫位於磁碟機 'F:' 而裝載次要複本的伺服器執行個體缺少 F: 磁碟機)，請在您的 WITH 子句中加入 MOVE 選項。  
  
4.  若要完成次要資料庫的組態設定，您必須將次要資料庫聯結至可用性群組。 如需詳細資訊，請參閱[將次要資料庫聯結至可用性群組 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)。  
  
> [!NOTE]  
>  如需如何執行這些備份和還原作業的相關資訊，請參閱本節稍後的[相關備份和還原工作](#RelatedTasks)。  
  
###  <a name="RelatedTasks"></a> 相關備份和還原工作  
 **若要建立資料庫備份**  
  
-   [建立完整資料庫備份 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [建立差異資料庫備份 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 **若要建立記錄備份**  
  
-   [備份交易記錄 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **若要還原備份**  
  
-   [Restore a Database Backup Using SSMS](../../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [還原差異資料庫備份 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-differential-database-backup-sql-server.md)  
  
-   [還原交易記錄備份 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [將資料庫還原到新位置 &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要準備次要資料庫**  
  
> [!NOTE]  
>  如需這個程序的範例，請參閱本主題前面的[範例 (Transact-SQL)](#ExampleTsql)。  
  
1.  除非您擁有主要資料庫的最新完整備份，否則請連接到裝載主要複本的伺服器執行個體，並且建立完整資料庫備份。 最佳作法是將這個備份和任何後續記錄備份放置於建議的網路共用。  
  
2.  在裝載次要複本的伺服器執行個體上，還原主要資料庫的完整資料庫備份 (並選擇性地還原差異備份)，接著還原所有後續記錄備份。 針對每個還原作業使用 WITH NORECOVERY。  
  
     如果主要資料庫與次要資料庫的檔案路徑不同 (例如，主要資料庫位於磁碟機 'F:' 而裝載次要複本的伺服器執行個體缺少 F: 磁碟機)，請在您的 WITH 子句中加入 MOVE 選項。  
  
3.  如果自從必要的記錄備份以來，在主要資料庫上建立過任何記錄備份，您也必須將這些備份複製到裝載次要複本的伺服器執行個體，並且一律使用 RESTORE WITH NORECOVERY，從最早的記錄開始，將每個記錄備份套用至次要資料庫。  
  
    > [!NOTE]  
    >  如果主要資料庫剛剛建立，而且尚未建立任何記錄備份，或者復原模式剛剛從簡單變更為完整，記錄備份就不存在。  
  
4.  若要完成次要資料庫的組態設定，您必須將次要資料庫聯結至可用性群組。 如需詳細資訊，請參閱[將次要資料庫聯結至可用性群組 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)。  
  
> [!NOTE]  
>  如需如何執行這些備份和還原作業的相關資訊，請參閱本主題稍後的[相關備份和還原工作](#RelatedTasks)。  
  
###  <a name="ExampleTsql"></a> Transact-SQL 範例  
 下列範例會準備次要資料庫。 此範例使用 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 範例資料庫，依預設採用簡單復原模式。  
  
1.  若要使用 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 資料庫，請將它修改為使用完整復原模式：  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE MyDB1   
    SET RECOVERY FULL;  
    GO  
    ```  
  
2.  將資料庫的復原模式從 SIMPLE 修改為 FULL 之後，請建立完整備份，以便用於建立次要資料庫。 因為剛剛才變更復原模式，所以指定了 WITH FORMAT 選項以建立新的媒體集。 要區分在完整復原模式與簡單復原模式建立的備份時，此方式非常有協助。 為了完成此範例的目的，我們會在資料庫所在的相同磁碟機上建立備份檔 (C:\\[!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)].bak)。  
  
    > [!NOTE]  
    >  對於實際執行的資料庫，您必須備份至其他裝置。  
  
     在裝載主要複本的伺服器執行個體 (`INSTANCE01`) 上，依照下列方式建立主要資料庫的完整備份：  
  
    ```  
    BACKUP DATABASE MyDB1   
        TO DISK = 'C:\MyDB1.bak'   
        WITH FORMAT  
    GO  
    ```  
  
3.  將完整備份複製到裝載次要複本的伺服器執行個體。  
  
4.  使用 RESTORE WITH NORECOVERY，將完整備份還原至裝載次要複本的伺服器執行個體。 還原命令需視主要與次要資料庫的路徑是否相同而定。  
  
    -   **若路徑相同：**  
  
         在裝載次要複本的電腦上，依照下列方式還原完整備份：  
  
        ```  
        RESTORE DATABASE MyDB1   
            FROM DISK = 'C:\MyDB1.bak'   
            WITH NORECOVERY  
        GO  
        ```  
  
    -   **若路徑不同：**  
  
         如果次要資料庫的路徑與主要資料庫的路徑不同 (例如，磁碟機代號不同)，則建立次要資料庫時，還原作業中必須包含 MOVE 子句。  
  
        > [!IMPORTANT]  
        >  如果主要與次要資料庫的路徑名稱不同，您將無法加入檔案。 這是因為接收加入檔案作業的記錄時，次要複本的伺服器執行個體會嘗試將新檔案放在主要資料庫所使用的相同路徑中。  
  
         例如，下列命令會還原位於 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 預設執行個體資料目錄 (C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA) 中之主要資料庫的備份。 還原資料庫作業必須將資料庫移至名為 (*Always On1*) 之 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 遠端執行個體的資料目錄，其中裝載另一個叢集節點的次要複本。 然後，資料和記錄檔就會還原至 *C:\Program Files\Microsoft SQL Server\MSSQL13.Always On1\MSSQL\DATA* 目錄。 此還原作業會使用 WITH NORECOVERY，將次要資料庫保留在還原資料庫中。  
  
        ```  
        RESTORE DATABASE MyDB1  
          FROM DISK='C:\MyDB1.bak'  
         WITH NORECOVERY,   
            MOVE 'MyDB1_Data' TO   
             'C:\Program Files\Microsoft SQL Server\MSSQL13.Always On1\MSSQL\DATA\MyDB1_Data.mdf',   
            MOVE 'MyDB1_Log' TO  
             'C:\Program Files\Microsoft SQL Server\MSSQL13.Always On1\MSSQL\DATA\MyDB1_Data.ldf';  
        GO  
        ```  
  
5.  還原完整備份之後，您必須在主要資料庫上建立記錄備份。 例如，下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式會將記錄備份至名為 *E:\MyDB1_log.bak* 的備份檔：  
  
    ```  
    BACKUP LOG MyDB1   
      TO DISK = 'E:\MyDB1_log.bak'   
    GO  
    ```  
  
6.  您必須先套用必要的記錄備份 (以及任何後續記錄備份)，然後才能將資料庫聯結至次要複本。  
  
     例如，下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式會從 *C:\MyDB1.bak* 還原第一筆記錄：  
  
    ```  
    RESTORE LOG MyDB1   
      FROM DISK = 'E:\MyDB1_log.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
7.  如果資料庫聯結次要複本之前執行了任何額外的記錄備份，您也必須使用 RESTORE WITH NORECOVERY，依序將這些記錄備份全部還原至裝載次要複本的伺服器執行個體。  
  
     例如，下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式會從 *E:\MyDB1_log.bak* 還原兩個額外的記錄：  
  
    ```  
    RESTORE LOG MyDB1   
      FROM DISK = 'E:\MyDB1_log.bak'   
        WITH FILE=2, NORECOVERY  
    GO  
    RESTORE LOG MyDB1   
      FROM DISK = 'E:\MyDB1_log.bak'   
        WITH FILE=3, NORECOVERY  
    GO  
    ```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **若要準備次要資料庫**  
  
1.  如果您需要建立主要資料庫的最新備份，請將目錄 (**cd**) 變更為裝載主要複本的伺服器執行個體。  
  
2.  使用 **Backup-SqlDatabase** Cmdlet 來建立每個備份。  
  
3.  將目錄切換到 (**cd**) 裝載次要複本的伺服器執行個體。  
  
4.  若要還原每個主要資料庫的資料庫和記錄備份，請使用 **restore-SqlDatabase** Cmdlet，並指定 **NoRecovery** 還原參數。 如果在裝載主要複本的電腦和裝載目標次要複本的電腦之間有檔案路徑差異，也要使用 **RelocateFile** 還原參數。  
  
    > [!NOTE]  
    >  若要檢視 Cmdlet 的語法，請在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 環境中使用 **Get-Help** Cmdlet。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)。  
  
5.  若要完成次要資料庫的組態設定，您必須將它聯結至可用性群組。 如需詳細資訊，請參閱[將次要資料庫聯結至可用性群組 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)。  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
###  <a name="ExamplePSscript"></a> 範例備份與還原指令碼和命令  
 下列 PowerShell 命令會將完整資料庫備份和交易記錄備份至網路共用，並且從該共用還原這些備份。 此範例會假設還原資料庫的目標檔案路徑與備份資料庫的檔案路徑相同。  
  
```  
# Create database backup  
Backup-SqlDatabase -Database "MyDB1" -BackupFile "\\share\backups\MyDB1.bak" -ServerInstance "SourceMachine\Instance"  
# Create log backup  
Backup-SqlDatabase -Database "MyDB1" -BackupAction "Log" -BackupFile "\\share\backups\MyDB1.trn" -ServerInstance "SourceMachine\Instance"  
# Restore database backup   
Restore-SqlDatabase -Database "MyDB1" -BackupFile "\\share\backups\MyDB1.bak" -NoRecovery -ServerInstance "DestinationMachine\Instance"  
# Restore log backup   
Restore-SqlDatabase -Database "MyDB1" -BackupFile "\\share\backups\MyDB1.trn" -RestoreAction "Log" -NoRecovery –ServerInstance "DestinationMachine\Instance"  
  
```  
  
##  <a name="FollowUp"></a> 後續操作：準備次要資料庫之後  
 若要完成次要資料庫的組態設定，您必須將新還原的資料庫聯結至可用性群組。 如需詳細資訊，請參閱[將次要資料庫聯結至可用性群組 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)。  
  
## 另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE 引數 &#40;Transact-SQL&#41;](../Topic/RESTORE%20Arguments%20\(Transact-SQL\).md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [疑難排解失敗的加入檔案作業 &#40;AlwaysOn 可用性群組&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
  