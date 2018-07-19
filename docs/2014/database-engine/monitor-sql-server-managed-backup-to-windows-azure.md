---
title: 監視 SQL Server Managed Backup to Windows Azure |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cfb9e431-7d4c-457c-b090-6f2528b2f315
caps.latest.revision: 20
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ff97e8210c38bac14bd7bd88075c2dea16f77489
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37149789"
---
# <a name="monitor-sql-server-managed-backup-to-windows-azure"></a>監視 SQL Server Managed Backup 到 Windows Azure
  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]有內建的測量工具，可用於找出備份程序中的問題和錯誤，並在可能時施以更正動作加以矯正。  不過有某些狀況需要使用者介入。 本主題描述可用於判斷備份之整體健康情況的工具，並找出需要處理的所有錯誤。  
  
## <a name="overview-of-includesssmartbackupincludesss-smartbackup-mdmd-built-in-debugging"></a>[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]內建偵錯概觀  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會定期檢閱排程的備份，並嘗試重新排程所有失敗的備份。 它會定期輪詢儲存體帳戶，找出記錄檔鏈結中，影響資料庫復原能力的中斷點，然後據此排程新的備份。 它也考慮到 Windows Azure 節流原則，並具備可管理多個資料庫備份的機制。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會使用擴充事件追蹤所有的活動。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]代理程式所使用的擴充事件通道包含管理、作業、分析和偵錯。 屬於管理類別的事件通常和錯誤有關，而且需要使用者的介入，並且預設為啟動。 分析事件也預設為開啟，不過通常和需要使用者介入的錯誤無關。 作業事件通常做為參考用。 例如，作業事件包括排程備份、順利完成備份等等。偵錯是最詳細的，被[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]在內部使用偵錯判斷問題，並視需要更正問題。  
  
### <a name="configure-monitoring-parameters-for-includesssmartbackupincludesss-smartbackup-mdmd"></a>設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的監視參數  
 **Smart_admin.sp_set_parameter**系統預存程序可讓您指定的監視設定。 下列章節將逐步討論啟用擴充事件的程序，以及啟用錯誤和警告的電子郵件通知。  
  
 **Smart_admin.fn_get_parameter**函式可用來取得特定參數或所有已設定的參數的目前設定。 如果從未設定過參數，該函數不會傳回任何值。  
  
1.  連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 這樣會傳回擴充事件的現有組態，以及電子郵件通知。  
  
```  
Use msdb  
Go  
SELECT * FROM smart_admin.fn_get_parameter (NULL)  
GO  
```  
  
 如需詳細資訊，請參閱 < [smart_admin.fn_get_parameter &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql)  
  
### <a name="extended-events-for-monitoring"></a>監視的擴充事件  
 管理、作業和分析事件預設為啟動。 在確認需要人工介入解決問題的錯誤時，管理事件是極為重要且實用的方法。 您可能會想要開啟作業和偵錯事件，但請注意，這些事件十分冗長，可能需要篩選。 下列程序描述如何監視透過擴充事件所記錄的事件。  
  
> [!IMPORTANT]  
>  不同於 SQL 引擎的擴充事件，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]不支援擴充事件工作階段的概念。 系統預存程序和函式可用於和擴充事件進行互動。 您也可以從記錄檔目錄檢視擴充事件記錄檔。  
  
##### <a name="to-configure-and-view-extended-events"></a>設定和檢視擴充事件  
  
1.  透過執行下列查詢來檢視可用的擴充事件通道及其目前狀態：  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     不論是否可設定，以及目前是否已啟用，此查詢的輸出會顯示 event_name。  如需詳細資訊，請參閱 < [smart_admin.fn_get_current_xevent_settings &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql)。  
  
2.  若要啟用偵錯事件，請執行下列查詢：  
  
    ```  
    --  to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
     如需有關預存程序的詳細資訊，請參閱 < [smart_admin.sp_set_parameter &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql)。  
  
3.  若要檢視紀錄的事件，請執行下列查詢：  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
    ```  
    --  view all admin events  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event nvarchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
### <a name="aggregated-error-countshealth-status"></a>彙總錯誤計數/健康情況  
 **Smart_admin.fn_get_health_status**函式會傳回每個類別，可用來監視的健全狀況狀態的彙總的錯誤計數資料表[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 系統也使用相同的功能設定本主題稍後所述的電子郵件通知機制。   
這些彙總計算可用來監視系統健全狀況。 例如，如果 number_ of_retention_loops 資料行在 30 分鐘內為 0，則保留管理可能需要耗費長時間運作，或甚至運作不正確。 非零的錯誤資料行可能表示出現問題，應檢查擴充事件記錄來發現此問題。 或者，呼叫**smart_admin.sp_get_backup_diagnostics**預存程序找到錯誤的詳細資訊。  
  
### <a name="using-agent-notification-for-assessing-backup-status-and-health"></a>使用代理程式通知以評估備份狀態和健全狀況  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]包含使用 SQL Server 原則式管理原則的通知機制。  
  
 **必要條件：**  
  
-   需要 Database Mail 使用這項功能。 如需如何啟用 DB 郵件的 SQL Server 執行個體的詳細資訊，請參閱 <<c0> [ 設定 Database Mail](../relational-databases/database-mail/configure-database-mail.md)。  
  
-   SQL Server Agent 警示系統的屬性應設定為使用 Database Mail。  
  
 **通知架構：**  
  
-   **原則式管理：** 兩個原則設定為監視備份健全狀態：**智慧型管理系統健全狀況原則**，而**智慧管理使用者動作健全狀況原則**。 智慧型管理系統健全狀況原則會評估嚴重的錯誤，例如缺少或無效的 SQL 認證以及連接錯誤，並且回報系統的健全狀況。 這些通常需要手動的動作才能修正基礎的問題。 智慧管理使用者動作健全狀況原則會評估警告訊息，例如損毀的備份等等。  這些可能不需要任何動作，只是事件的警告訊息。 依照預期，這類問題會由[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]代理程式自動處理。  
  
-   **SQL Server Agent**作業： 使用具有三個作業步驟的 SQL Server Agent 作業以執行通知。 在第一個作業步驟中，它會偵測[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]是否為資料庫或執行個體進行設定。 當其偵測到已有啟用及設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]時，會執行第二個步驟：透過評估 SQL Server 原則式管理原則，執行 PowerShell 指令程式評估健康狀態。 若是偵測到錯誤或警告便，其會失敗，然後觸發第三個步驟︰傳送隨附此錯誤/警告報表的電子郵件通知。  但是此 SQL Server Agent 預設為不啟用。 若要啟用電子郵件通知工作，請使用**smart_admin.sp_set_backup_parameter**系統預存程序。  下列程序將更詳細說明這些步驟：  
  
##### <a name="enabling-email-notification"></a>啟用電子郵件通知  
  
1.  如果尚未設定 Database Mail，使用中所述的步驟[設定 Database Mail](../relational-databases/database-mail/configure-database-mail.md)。  
  
2.  將資料庫設定 SQL Server 警示系統的郵件系統： 以滑鼠右鍵按一下**SQL Server Agent**，選取**警示系統**，檢查**啟用郵件設定檔**方塊中，選取**Database Mail**作為**郵件系統**，然後選取先前建立的郵件設定檔。  
  
3.  在查詢視窗中執行下列查詢，並提供您希望通知送達的電子郵件地址：  
  
    ```  
    Use msdb  
    Go  
    EXEC smart_admin.sp_set_parameter @parameter_name = 'SSMBackup2WANotificationEmailIds', @parameter_value = '<email address>'  
  
    ```  
  
     當備份有錯誤或問題時，這會建立用來蒐集健康情況及傳送通知的 SQL Server Agent 作業。  
  
 下列是啟用 DB 郵件和透過 SQL Server Agent 作業設定電子郵件通知的範例指令碼  
  
```  
-- Prereq: Make sure that SQL Server service runs in a service account that has  
--  access to SMTP Server   
-- set SQL Server service account as domain account   
  
EXEC sp_configure 'show advanced', 1  
RECONFIGURE  
GO  
  
-- Enable DBMail  
EXEC sp_configure 'Database Mail XPs',1  
GO  
RECONFIGURE  
GO  
  
-- Configure DBMail  
DECLARE @emailid NVARCHAR(255)  
-- Note: change this email to your own email id  
SET @emailid = N'emailalias@mycompany.com'  
  
DECLARE @smtpserver NVARCHAR(255)  
SET @smtpserver = N'smtphost.domainname.com'  
  
DECLARE @mailprofile NVARCHAR(255)  
SET @mailprofile = N'my_profile'  
  
EXEC msdb.dbo.sysmail_add_account_sp @account_name=N'myaccount',  
                @email_address = @emailid,  
                @replyto_address = @emailid,  
                @mailserver_name = @smtpserver,  
                @use_default_credentials = 1  
  
EXEC msdb.dbo.sysmail_add_profile_sp @profile_name=@mailprofile  
EXEC msdb.dbo.sysmail_add_profileaccount_sp @profile_name=@mailprofile, @account_name=N'myaccount', @sequence_number=1  
  
-- Set SQL Agent to use DBMail profile  
EXEC msdb.dbo.sp_set_sqlagent_properties @databasemail_profile = @mailprofile  
  
-- Configure Notifications   
EXEC msdb.smart_admin.sp_set_parameter  
@parameter_name = 'SSMBackup2WANotificationEmailIds',  
@parameter_value = @emailid  
  
-- To test is you are receiving notifications  
-- delete few backup files from your storage container, Wait for 15 minutes & see if you get any email notification  
  
```  
  
### <a name="using-powershell-to-setup-custom-health-monitoring"></a>使用 PowerShell 設定自訂健全狀況監視  
 **Test-sqlsmartadmin** cmdlet 可用來建立自訂健全狀況監視。 例如，前一節所述的通知選項可在執行個體層級設定。  如果您將多個 SQL Server 執行個體設定為使用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，即可使用 PowerShell 指令程式建立指令碼，以收集所有執行個體之備份的狀態及健全狀態。  
  
 **Test-sqlsmartadmin** cmdlet 會評估 SQL Server 原則式管理原則所傳回的警告與錯誤，然後回報積存狀態。  根據預設，此指令程式使用系統原則。 若要包含所有自訂原則，請使用 `–AllowUserPolicies` 參數。  
  
 下面是 PowerShell 指令碼的範例，它會根據系統原則和所有建立的使用者原則，傳回錯誤和警告報告：  
  
```  
$policyResults = get-sqlsmartadmin | test-sqlsmartadmin -AllowUserPolicies  
$policyResults.PolicyEvaluationDetails | select Name, Category, Expression, Result, Exception | fl  
  
```  
  
 下列指令碼會傳回預設執行個體的錯誤和警告詳細報告：  
  
```  
PS C:\>PS SQLSERVER:\SQL\COMPUTER\DEFAULT> (get-sqlsmartadmin ).EnumHealthStatus()  
```  
  
### <a name="objects-in-msdb-database"></a>MSDB 資料庫中的物件  
 系統會安裝實作此功能的物件。 這些物件會保留給內部使用。 不過，有一個系統資料表對於監視備份狀態很實用：smart_backup_files。 大部分的資訊儲存在此與像是備份、 資料庫類型的監視相關的資料表名稱，第一次和最後一個 lsn，備份的到期日透過系統函式公開[smart_admin.fn_available_backups &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql). 但是，使用此函數則無法使用 smart_backup_files 資料表中的狀態資料行 (可指示備份檔案的狀態)。 以下是您可以從系統資料表中擷取部分資訊 (包括狀態) 的範例查詢：  
  
```  
USE msdb  
GO  
SELECT  
 database_name AS [Database Name]  
,backup_path AS [Backup Destination and File]  
,[Backup Type] =  
CASE backup_type  
WHEN 1 THEN 'FULL'  
WHEN 2 THEN 'LOG'  
END  
,[Backup Status] =  
CASE [status]  
WHEN 'A' THEN 'Available'  
WHEN 'B' THEN 'Copy In Progress'  
WHEN 'C' THEN 'Corrupted'  
WHEN 'D' THEN 'Deleted'  
WHEN 'F' THEN 'Copy Failed'  
WHEN 'U' THEN 'Unknown'  
END  
,first_lsn AS [First LSN]  
,last_lsn AS [Last LSN]  
,backup_start_date AS [Backup Start Time]  
,backup_finish_date AS [Backup Completion Time]  
,expiration_date AS [Backup Expiry Date/Time]  
FROM  
smart_backup_files;  
  
```  
  
 下面是傳回之不同狀態的詳細說明：  
  
-   **可用-A**這是正常的備份檔案。 備份已經完成，也已經確認它可在 Windows Azure 儲存體中使用。  
  
-   **複製進行中的-b:** 這個狀態是專門針對可用性群組資料庫。 如果[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]在備份記錄鏈結中偵測到中斷，它會先嘗試識別可能在備份鏈結中造成中斷的備份。 在尋找備份檔案時，它會嘗試將檔案複製到 Windows Azure 儲存體。 當複製作業正在進行時，它將會顯示這個狀態。  
  
-   **複製失敗-F**類似複製進行中 」，這是專用的可用性群組資料庫。 如果複製程序失敗，狀態會標示成 F。  
  
-   **已損毀-c:** 如果[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]是無法多次嘗試之後，即使執行 RESTORE HEADER_ONLY 命令來確認儲存體中的備份檔案，它將此檔案標示為損毀。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會排程備份，以確保損毀的檔案不會導致備份鏈結中斷。  
  
-   **已刪除-d:** Windows Azure 儲存體中找不到對應的檔案。 如果已刪除的檔案造成備份鏈結中斷，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]將會排程備份。  
  
-   **未知-U**此狀態指出[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]尚未能夠確認檔案是否存在，而且它在 Windows Azure 儲存體中的屬性。 下次執行此程序時 (大約每隔 15 分鐘執行一次)，將會更新此狀態。  
  
  
