---
title: 升級記錄傳送到 SQL Server 2014 (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], upgrading
ms.assetid: b1289cc3-f5be-40bb-8801-0e3eed40336e
caps.latest.revision: 57
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 96179ecc9f49bde6b27e2d2bf8dab86835054f0b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37310398"
---
# <a name="upgrade-log-shipping-to-sql-server-2014-transact-sql"></a>將記錄傳送升級至 SQL Server 2014 (Transact-SQL)
  當您從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時，可保留記錄傳送組態。 本主題描述升級記錄傳送組態的替代案例和最佳做法。  
  
> [!NOTE]  
>  [中所導入的＜](../../relational-databases/backup-restore/backup-compression-sql-server.md) 備份壓縮 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]＞。 升級的記錄傳送組態會使用 **備份壓縮預設** 伺服器層級組態選項，來控制備份壓縮是否會用於交易記錄備份檔案。 可以針對每一個記錄傳送組態來指定記錄備份的備份壓縮行為。 如需詳細資訊，請參閱[設定記錄傳送 &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)。  
  
  
##  <a name="ProtectData"></a> 在升級之前保護資料  
 我們建議的最佳做法是在升級記錄傳送之前先保護資料。  
  
 **保護資料**  
  
1.  在每一個主要資料庫上執行完整資料庫備份。  
  
     如需詳細資訊，請參閱 [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)中建立差異資料庫備份。  
  
2.  在每一個主要資料庫上執行 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 命令。  
  
##  <a name="UpgradeMonitor"></a> 升級監視伺服器執行個體  
 可以隨時升級監視伺服器執行個體 (如果有的話)。  
  
 在升級監視伺服器時，記錄傳送組態會持續有效，但是監視器上的資料表中不會記錄它的狀態。 當升級監視伺服器時，將不會觸發任何已經設定的警示。 在升級之後，您可以執行 [sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql) 系統預存程序來更新監視資料表內的資訊。  
  
##  <a name="UpgradeSingleSecondary"></a> 升級記錄傳送組態，使用單一次要伺服器  
 本章節所述的升級程序假設組態是由主要伺服器以及只有一部次要伺服器所組成。 這個組態會在下圖中表示，其中顯示主要伺服器執行個體 A 及單一次要伺服器執行個體 B。  
  
 ![一部次要伺服器，但是沒有監視伺服器](../media/ls-2-wayconfig-nomonitor.gif "一部次要伺服器，但是沒有監視伺服器")  
  
 如需有關升級多部次要伺服器的詳細資訊，請參閱本主題稍後的＜ [升級多個次要伺服器執行個體](#MultipleSecondaries)＞。  
 
  
###  <a name="UpgradeSecondary"></a> 升級次要伺服器執行個體  
 升級程序牽涉到升級的次要伺服器執行個體[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更高的記錄傳送組態，以[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]然後再升級主要伺服器執行個體。 一定要先升級次要伺服器執行個體。 如果主要伺服器已升級的次要伺服器之前，記錄傳送會失敗，因為在較新版本上所建立的備份[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]無法還原較舊版本的上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 記錄傳送會在整個升級過程中繼續，因為升級的次要伺服器會繼續從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版主要伺服器還原記錄備份。 升級次要伺服器執行個體的程序部分取決於記錄傳送組態是否會處理多部次要伺服器。 如需詳細資訊，請參閱本主題稍後的＜ [升級多個次要伺服器執行個體](#MultipleSecondaries)＞。  
  
 當升級次要伺服器執行個體時，記錄傳送複製和還原作業不會執行，所以未還原的交易記錄備份將會累積。 累積的數量取決於在主要伺服器上排程備份的頻率。 此外，如果已經設定了個別的監視伺服器，則可能會引發警示，指出還原執行的時間長度尚未超過設定的間隔。  
  
 一旦升級了次要伺服器之後，記錄傳送代理程式作業就會繼續，並繼續從主要伺服器執行個體 (伺服器 A) 複製及還原記錄備份。次要伺服器讓次要資料庫變成最新狀態所需的時間會有所差異，取決於升級次要伺服器所花的時間以及主要伺服器上的備份頻率而定。  
  
> [!NOTE]  
>  伺服器在升級期間，次要資料庫不會升級到[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]資料庫。 只有當該資料庫處於線上時，才會進行升級。  
  
> [!IMPORTANT]  
>  需要升級的資料庫不支援 RESTORE WITH STANDBY 選項。 如果已升級的次要資料庫已經使用 RESTORE WITH STANDBY 加以設定，升級之後無法再還原交易記錄。 若要繼續進行該次要資料庫上的記錄傳送，您需要在該部待命伺服器上再次設定記錄傳送。 如需有關 STANDBY 選項的詳細資訊，請參閱 < [RESTORE 引數&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)。  
  
###  <a name="UpgradePrimary"></a> 升級主要伺服器執行個體  
 在規劃升級時，有一個極重要的考量就是無法使用資料庫的時間量。 最簡單的升級案例牽涉到當您升級主要伺服器時所無法使用的資料庫 (底下的案例 1)。  
  
 但代價是更複雜的升級程序中，您可以最大化您的資料庫可用性的容錯移轉[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更高版本的主要伺服器[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]次要伺服器，然後再升級原始主要伺服器 (案例 2 底下)。 容錯移轉案例有兩種變化。 您可以切換回原始主要伺服器，並保留原始記錄傳送組態。 另外，您也可以在升級原始主要伺服器之前先移除原始記錄傳送組態，之後再使用新的主要伺服器建立新的組態。 本章節描述這兩種案例。  
  
> [!IMPORTANT]  
>  在升級主要伺服器執行個體之前，請務必先升級次要伺服器執行個體。 如需詳細資訊，請參閱本主題前面的＜ [升級次要伺服器執行個體](#UpgradeSecondary)＞。  
  
  
####  <a name="Scenario1"></a> 案例 1： 升級主要伺服器執行個體，而不需要容錯移轉  
 這是比較簡單的案例，因為它的停機時間比使用容錯移轉來得長。 只會升級主要伺服器執行個體，而在這個升級作業期間將無法使用資料庫。  
  
 升級伺服器之後，資料庫就會自動回到線上，以便進行升級。 在升級資料庫之後，記錄傳送作業就會繼續。  
  
#### <a name="scenario-2-upgrade-primary-server-instance-with-failover"></a>案例 2：使用容錯移轉升級主要伺服器執行個體  
 此案例會讓可用性提升到最高，並讓停機時間減至最少。 此案例使用一種受到控制的方式來容錯移轉至次要伺服器執行個體，在升級原始主要伺服器執行個體期間維持資料庫的可用性。 停機時間限制為容錯移轉所需的相對簡短時間，而非升級主要伺服器執行個體所需的時間。  
  
 在使用容錯移轉來升級主要伺服器執行個體時，會牽涉到三個一般程序：執行受到控制的方式來容錯移轉到次要伺服器、將原始主要伺服器執行個體升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，並在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 主要伺服器執行個體上設定記錄傳送。 本章節會描述這些程序。  
  
> [!IMPORTANT]  
>  如果您打算讓次要伺服器執行個體當做新的主要伺服器執行個體，您需要移除記錄傳送組態。 當原始主要伺服器執行個體升級之後，需要重新設定從新的主要伺服器到新的次要伺服器的記錄傳送。 如需詳細資訊，請參閱 <<c0> [ 移除記錄傳送&#40;SQL Server&#41;](remove-log-shipping-sql-server.md)。</c0>  
  
  
#####  <a name="Procedure1"></a> 程序 1： 執行受到控制的容錯移轉到次要伺服器  
 以受到控制的方式容錯移轉到次要伺服器：  
  
1.  手動執行[結尾記錄備份](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)指定 WITH NORECOVERY 在主要資料庫上的交易記錄檔。 這個記錄備份會擷取任何尚未備份的記錄檔記錄，並讓資料庫離線。 請注意，當資料庫離線時，記錄傳送備份作業將會失敗。  
  
     下列範例會在主要伺服器上建立 `AdventureWorks` 資料庫的結尾記錄備份。 備份檔案命名為 `Failover_AW_20080315.trn`：  
  
    ```  
    BACKUP LOG AdventureWorks   
      TO DISK = N'\\FileServer\LogShipping\AdventureWorks\Failover_AW_20080315.trn'   
       WITH NORECOVERY;  
    GO  
    ```  
  
     我們建議您最好使用不同的檔案命名規範來區分手動建立的備份檔案以及記錄傳送備份作業所建立的備份檔案。  
  
2.  在次要伺服器上：  
  
    1.  確定記錄傳送備份作業所自動進行的所有備份都已經套用。 若要檢查哪些備份作業已經套用，請使用[sp_help_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql)監視伺服器或是主要和次要伺服器上，系統預存程序。 相同的檔案應該列在**last_backup_file**， **last_copied_file**，並**last_restored_file**資料行。 如果有任何備份檔案尚未複製和還原，請針對記錄傳送組態手動叫用代理程式複製和還原作業。  
  
         如需啟動工作的相關資訊，請參閱 <<c0> [ 啟動工作](../../ssms/agent/start-a-job.md)。  
  
    2.  將您在步驟 1 建立的最後記錄備份檔案從檔案共用位置複製到次要伺服器上的記錄傳送所使用的本機位置。  
  
    3.  指定 WITH RECOVERY 來還原最後記錄備份，讓資料庫回到線上。 讓資料庫回到線上的過程中，資料庫將會升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
         下列範例會在次要資料庫上還原 `AdventureWorks` 資料庫的結尾記錄備份。 此範例使用 WITH RECOVERY 選項，讓資料庫回到線上：  
  
        ```  
        RESTORE LOG AdventureWorks   
          FROM DISK = N'c:\logshipping\Failover_AW_20080315.trn'   
           WITH RECOVERY;  
        GO  
        ```  
  
        > [!NOTE]  
        >  如果是包含多部次要伺服器的組態，則有額外的考量。 如需詳細資訊，請參閱本主題稍後的＜ [升級多個次要伺服器執行個體](#MultipleSecondaries)＞。  
  
    4.  將用戶端從原始主要伺服器 (伺服器 A) 重新導向線上次要伺服器 (伺服器 B) 來容錯移轉資料庫。  
  
    5.  請注意，當資料庫在線上時，次要資料庫的交易記錄並不會填滿。 若要避免交易記錄被填滿，您可能需要加以備份。 如果是這種情況，我們建議您將它備份到共用位置 ( *「備份共用」*(Backup Share))，讓備份可在其他伺服器執行個體上用來還原。  
  
#####  <a name="Procedure2 "></a> 程序 2： 升級原始主要伺服器執行個體 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 在您將原始主要伺服器執行個體升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之後，資料庫仍然會在離線狀態而且採用格式。  
  
#####  <a name="Procedure3"></a> 程序 3： 設定記錄傳送 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 升級程序的其餘步驟取決於是否仍設定記錄傳送而定，如下所示：  
  
-   如果您已保留 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版記錄傳送組態，請切換回原始的主要伺服器執行個體。 如需詳細資訊，請參閱本主題稍後的＜ [切換回原始的主要伺服器執行個體](#SwitchToOrigPrimary)＞。  
  
-   如果您在容錯移轉之前移除此記錄傳送組態，請建立新的記錄傳送組態，其中原始的次要伺服器執行個體為新的主要伺服器執行個體。 如需詳細資訊，請參閱本主題稍後的＜ [將舊的次要伺服器執行個體保留為新的主要伺服器執行個體](#KeepOldSecondaryAsNewPrimary)＞。  
  
######  <a name="SwitchToOrigPrimary"></a> 若要切換回原始的主要伺服器執行個體  
  
1.  在暫時的主要伺服器 (伺服器 B) 上，使用 WITH NORECOVERY 來備份記錄的結尾，以便建立結尾記錄備份並讓資料庫離線。 結尾記錄備份命名為 `Switchback_AW_20080315.trn`。例如：  
  
    ```  
    BACKUP LOG AdventureWorks   
      TO DISK = N'\\FileServer\LogShipping\AdventureWorks\Switchback_AW_20080315.trn'   
       WITH NORECOVERY;  
    GO  
    ```  
  
2.  如果在暫時的主要資料庫上進行任何交易記錄備份，而不是您在步驟 1 建立的結尾備份，請使用 WITH NORECOVERY 將這些記錄備份還原到原始主要伺服器 (伺服器 A) 上的離線資料庫。 資料庫升級為[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]格式化的第一個記錄備份還原時。  
  
3.  使用 WITH RECOVERY 在原始的主要資料庫上還原結尾記錄備份 `Switchback_AW_20080315.trn`，讓資料庫回到線上。  
  
4.  將用戶端從原始主要伺服器重新導向線上次要伺服器，容錯移轉回到原始的主要資料庫 (在伺服器 A 上)。  
  
 當資料庫變成線上狀態之後，原始的記錄傳送組態將會繼續。  
  
######  <a name="KeepOldSecondaryAsNewPrimary"></a> 若要將舊的次要伺服器執行個體保留為新的主要伺服器執行個體  
 將舊的次要伺服器執行個體 B 當做主要伺服器使用，並將舊的主要伺服器執行個體 A 當做新的次要伺服器使用，以建立新的記錄傳送組態，如下所示：  
  
> [!IMPORTANT]  
>  在進行手動交易記錄備份來讓資料庫離線之前，舊的記錄傳送組態應該在程序開始時就已經從原始的主要伺服器中移除。  
  
1.  若要避免在新的次要伺服器 (伺服器 A) 上執行資料庫的完整備份及還原，請將記錄備份從新的主要資料庫套用到新的次要資料庫。 在範例組態中，這牽涉到將伺服器 B 上所做的記錄備份還原到伺服器 A 上的資料庫。  
  
2.  從新的主要資料庫備份記錄 (在伺服器 B 上)。  
  
3.  使用 WITH NORECOVERY 將記錄備份還原到新的次要伺服器執行個體 (伺服器 A)。 第一項還原作業將資料庫更新為[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
4.  使用之前的次要伺服器 (伺服器 B) 將記錄傳送組態為主要伺服器執行個體。  
  
    > [!IMPORTANT]  
    >  如果您使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，指定次要資料庫已初始化。  
  
     如需詳細資訊，請參閱[設定記錄傳送 &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)。  
  
5.  將用戶端從原始主要伺服器 (伺服器 A) 重新導向線上次要伺服器 (伺服器 B) 來容錯移轉資料庫。  
  
    > [!IMPORTANT]  
    >  當您容錯移轉到新的主要資料庫時，應該確保其中繼資料與原始主要資料庫的中繼資料一致。 如需詳細資訊，請參閱 [在另一個伺服器執行個體上提供可用的資料庫時，管理中繼資料 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)。  
  
##  <a name="MultipleSecondaries"></a> 升級多個次要伺服器執行個體  
 這個組態會在下圖中表示，其中顯示主要伺服器執行個體 A 及兩個次要伺服器執行個體 B 和 C。  
  
 ![兩個次要伺服器，但是沒有監視伺服器](../media/ls-3-wayconfig-nomonitor.gif "兩個次要伺服器，但是沒有監視伺服器")  
  
 本節討論如何使用容錯移轉進行升級，然後再切換回原始的主要伺服器。 當您使用容錯移轉升級主要執行個體時，程序要比多個次要伺服器執行個體來得複雜。 在下列程序中，當升級所有次要伺服器之後，主要伺服器會容錯移轉成其中一個升級的次要資料庫。 原始主要伺服器會升級，而記錄傳送則會容錯移轉回該伺服器。  
  
> [!IMPORTANT]  
>  在升級主要伺服器之前，請務必先升級所有次要伺服器執行個體。  
  
 **若要升級使用容錯移轉，然後再切換回原始主要伺服器**  
  
1.  升級所有必要的伺服器執行個體 (伺服器 B 和 C)。  
  
2.  使用 WITH NORECOVERY 來備份交易記錄，以取得主要資料庫的交易記錄結尾 (在伺服器 A 上)，並讓資料庫離線。  
  
3.  在您打算容錯移轉到其上的次要伺服器 (伺服器 B) 上，使用 WITH RECOVERY 還原記錄備份來讓次要資料庫回到線上。  
  
4.  在其他每一部次要伺服器 (伺服器 C) 上，使用 WITH NORECOVERY 還原記錄備份來讓次要資料庫離線。  
  
    > [!NOTE]  
    >  記錄傳送複製和還原作業將會在次要伺服器上執行，但是這些作業不會做任何事，因為新的記錄備份檔案將不會置於備份共用位置。  
  
5.  將用戶端從原始主要伺服器 (伺服器 A) 重新導向線上次要伺服器 (伺服器 B) 來容錯移轉資料庫。 線上資料庫會變成暫時的主要伺服器，以便在原始的主要伺服器 (伺服器 A) 離線時可保持資料庫的可用性。  
  
6.  升級原始的主要伺服器 (伺服器 A)。  
  
7.  在您容錯移轉到其上的資料庫 (也就是伺服器 B 上的暫時主要資料庫) 上，使用 WITH NORECOVERY 手動備份交易記錄。 這樣會讓資料庫離線。  
  
8.  使用 WITH NORECOVERY 將您在暫時主要資料庫 (在伺服器 B) 上建立的所有交易記錄備份還原到其他每一個次要資料庫 (在伺服器 C 上)。 如此可在升級之後從原始的主要資料庫繼續進行記錄傳送，而不需要在每一個次要資料庫上還原完整的資料庫。  
  
9. 使用 WITH RECOVERY 將交易記錄從暫時的主要伺服器 (伺服器 B) 還原到原始的主要資料庫。  
  
##  <a name="Redeploying"></a> 重新部署記錄傳送  
 如果不想使用上述任一個程序來移轉您的記錄傳送組態，則也可以重新部署記錄傳送，方法是利用主要資料庫的完整備份與還原來重新初始化次要資料庫。 如果您的資料庫較小，或是升級程序期間不需要高可用性，這個方法可能會比較適用。  
  
 如需啟用記錄傳送的資訊，請參閱[設定記錄傳送&#40;SQL Server&#41;](configure-log-shipping-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [記錄傳送資料表與預存程序](log-shipping-tables-and-stored-procedures.md)  
  
  
