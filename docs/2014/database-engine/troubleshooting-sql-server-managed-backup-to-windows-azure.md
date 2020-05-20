---
title: 針對 SQL Server 受控備份至 Azure 進行疑難排解 |Microsoft Docs
description: 本文說明您可以用來疑難排解 SQL Server Managed 備份至 Microsoft Azure 作業期間可能發生之錯誤的工作和工具。
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: a34d35b0-48eb-4ed1-9f19-ea14754650da
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: db55c753317f945a8156b671fa9cbcd72ce4c641
ms.sourcegitcommit: 553d5b21bb4bf27e232b3af5cbdb80c3dcf24546
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2020
ms.locfileid: "82849596"
---
# <a name="troubleshooting-sql-server-managed--backup-to-azure"></a>SQL Server Managed Backup 到 Azure 的疑難排解
  本主題說明[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]作業期間，針對其中可能發生的錯誤所使用的工作和工具進行疑難排解。  
  
## <a name="overview"></a>概觀  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]內建有檢查和疑難排解程序，所以在許多情況中，內部失敗會由[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]程序自行處理。  
  
 其中一種情況的範例是刪除備份檔案，而導致記錄檔鏈中斷影響復原能力- [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 會識別記錄鏈中的中斷，並排程立即取得備份。 不過，建議您監視狀態及處理需要手動介入的所有錯誤。  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]使用系統預存程序、系統檢視和擴充事件記錄事件和錯誤。 系統檢視和預存程序皆提供[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]組態資訊、備份排程備份的狀態，以及擴充事件所擷取到的錯誤。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會使用擴充事件擷取錯誤，供疑難排解之用。 刪除記錄事件之外，SQL Server Smart Admin 原則會提供電子郵件通知工作所使用的健康情況，以提供通知或錯誤與問題。 如需詳細資訊，請參閱[監視 SQL Server 受控備份至 Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)。  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]也會使用手動備份至 Azure 儲存體時所使用的相同記錄（SQL Server 備份至 URL）。 如需備份至 URL 相關問題的詳細資訊，請參閱[SQL Server 備份至 url 的最佳作法和疑難排解](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)中的疑難排解一節。  
  
### <a name="general-troubleshooting-steps"></a>一般疑難排解步驟  
  
1.  啟用電子郵件通知，開始接收錯誤和警告的電子郵件。  
  
     此外，您也可以定期執行 `smart_admin.fn_get_health_status`，藉以檢查彙總錯誤和計數。 例如，`number_of_invalid_credential_errors` 是智慧型備份嘗試備份，但卻得到無效認證錯誤的次數。 `Number_of_backup_loops` 和 `number_of_retention_loops` 不是錯誤；他們會指出備份執行緒與保留執行緒掃描資料庫清單的次數。 一般而言，當 @begin_time 未提供和時，函式 @end_time 會顯示過去30分鐘內的資訊，因此，通常應該會看到這兩個數據行的非零值。 若出現零值，有可能是系統過載或甚至是系統無回應。 如需詳細資訊，請參閱本主題稍後的針對**系統問題進行疑難排解**一節。  
  
2.  檢閱擴充事件記錄，了解錯誤和其他相關事件的詳細資料。  
  
3.  使用此記錄中的資訊解決問題。  當系統發生問題或錯誤時，可能必須重新啟動服務或 SQL Server Agent。  
  
### <a name="common-causes-of-errors"></a>錯誤常見原因  
 下列清單是導致失敗的常見原因：  
  
1.  **SQL 認證的變更：** 如果所使用的認證名稱已 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 變更，或已被刪除， [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 將無法進行備份。 此變更應套用到[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]組態設定。  
  
2.  **儲存體存取金鑰值的變更：** 如果 Azure 帳戶的儲存體金鑰值已變更，但 SQL 認證並未以新值更新， [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 則在對儲存體進行驗證時將會失敗，而且無法備份設定為使用此帳戶的資料庫。  
  
3.  **Azure 儲存體帳戶的變更：** 刪除或重新命名儲存體帳戶，而不需要對 SQL 認證進行對應的變更，將會導致 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 失敗，而且不會執行任何備份。 如果您刪除儲存體帳戶，請務必為資料庫重新設定有效的儲存體帳戶資訊。 如果儲存體帳戶已重新命名，或已變更金鑰值，請確定這些變更會反映在[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]使用的 SQL 認證上。  
  
4.  **資料庫屬性的變更：** 變更復原模式或變更名稱可能導致備份失敗。  
  
5.  **復原模式的變更：** 如果資料庫的復原模式從完整或大量記錄變更為 simple，備份將會停止，並會略過資料庫 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 。 如需詳細資訊，請參閱[SQL Server 受管理的備份至 Azure：互通性與共存](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
### <a name="most-common-error-messages-and-solutions"></a>最常見的錯誤訊息和解決方案  
  
1.  **啟用或設定時的錯誤 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ：**  
  
     錯誤：「無法存取儲存體 URL ...。請提供有效的 SQL 認證 ...」：您可能會看到此錯誤，以及參考 SQL 認證的其他類似錯誤。  在這種情況下，請檢查您提供的 SQL 認證名稱，以及儲存在 SQL 認證中的資訊-儲存體帳戶名稱和儲存體存取金鑰，並確保它們是最新且有效的。  
  
     錯誤：「.。。無法設定資料庫 ...。因為它是系統資料庫」：如果您嘗試針對系統資料庫啟用，就會看到此錯誤 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 。  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]不支援系統資料庫的備份。  若要設定系統資料庫的備份，請使用其他 SQL Server 備份技術 (例如維護計劃)。  
  
     錯誤：「.。。提供保留期限 ...」：如果您在第一次設定這些值時未指定資料庫或實例的保留期限，您可能會看到關於保留期間的錯誤。 如果您提供的值不是 1 到 30 之間的數字，也可能會看到錯誤。 保留期限的允許值是 1 到 30 之間的數字。  
  
2.  **電子郵件通知錯誤：**  
  
     錯誤：「未啟用 Database Mail ...」-如果您啟用電子郵件通知，但未在實例上設定 Database Mail，就會看到此錯誤。 您必須在執行個體上設定 Database Mail，以接收[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的健康情況通知。 如需有關如何啟用 database mail 的詳細資訊，請參閱[設定 Database Mail](../relational-databases/database-mail/configure-database-mail.md)。 您也必須啟用 SQL Server Agent 以使用 Database Mail 進行通知。 如需詳細資訊，請參閱[開始之前](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md#BeforeYouBegin)。  
  
     下列清單列出和電子郵件通知相關的錯誤號碼：  
  
    -   ErrorNumber：45209  
  
    -   ErrorNumber：45210  
  
    -   錯誤號碼：45211  
  
3.  **連接錯誤：**  
  
    -   **SQL 連線能力的相關錯誤：** 當連接到 SQL Server 實例時發生問題時，就會發生這些錯誤。 擴充的事件會透過管理通道公開這些錯誤類型。 以下是您可能會看到與此種連接問題相關之錯誤的兩個擴充事件：  
  
         FileRetentionAdminXEvent，且 event_type = SqlError。 如需有關此錯誤的詳細資料，請參閱該事件的 error_code、error_message 和 stack_trace。 Error_code 是 SqlException 的錯誤號碼。  
  
         具有下列訊息/訊息前置詞的 SmartBackupAdminXevent：  
  
         *「為實例設定 SQL Server 受管理備份至 Azure 預設值時發生內部錯誤。錯誤可能是暫時性的。」*  
  
         *「可能會遇到 SQL Server 的連線問題。正在略過目前反覆運算中的資料庫」。*  
  
         *「查詢記錄使用量資訊失敗。失敗可能是暫時性的。正在略過目前反覆運算中的資料庫」。*  
  
         *「載入 SSMBackup2WA 代理程式中繼資料時，發生 SQL 例外狀況。失敗可能是暫時性的。將會重試操作。」*  
  
         *「SSMBackup2WA 發生 SQL 例外狀況 .。。"*  
  
    -   **連接至儲存體帳戶時發生錯誤：**  
  
         FileRetentionAdminXEvent 中回報了儲存體例外狀況，且 event_type = XstoreError。 如需有關此錯誤的詳細資料，請參閱該事件的 error_message 和 stack_trace。  
  
         因為 SQL Server Managed Backup 會使用基礎的「備份至 URL」技術，所以與儲存體連接相關的錯誤適用於這兩項功能。 如需疑難排解步驟的詳細資訊，請參閱[SQL Server 備份至 URL 的最佳作法和疑難排解](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)一文中的**疑難排解一節**。  
  
### <a name="troubleshooting-system-issues"></a>疑難排解系統問題  
 下列案例指出系統 (SQL Server、SQL Server Agent) 發生問題的案例及其對[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的影響：  
  
-   **當 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 執行時，sqlservr.exe 停止回應或停止運作：** 如果 SQL Server 停止運作，sql 代理程式將會正常關閉， [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 並會停止，並將事件記錄在 SQL 代理程式中。 out file。  
  
     如果 SQL Server 停止回應，事件會記錄到管理通道。  以下是事件記錄檔的範例：  
  
     *Sql 錯誤（引擎沒有回應或 get sqlException： SqlException：*   
     *錯誤碼、訊息和 stacktrace 會顯示在管理通道 xevent 中，以及一些額外的資訊，例如：*   
    *「可能會遇到 SQL Server 的連線問題。正在略過目前反覆運算中的資料庫」*  
  
-   **當執行時，SQL 代理程式停止回應或停止運作 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ：**  
  
     如果 SQL Agent 停止運作，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]也會停止，並將事件記錄到管理通道。 這與 SQL Server 停止回應的案例類似。  
  
     如果 SQL Agent 停止回應，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]將無法繼續執行備份作業，事件也會記錄到管理通道。 以下是事件記錄檔的範例：  
  
     *作業停止回應：請參閱管理通道 xevents*   
    *「資料庫備份的 DBBackupInfoMsgMaxWaitTime +」小時內，未收到來自 SQL Server 的進度更新。  SSM 雲端備份將繼續等待。」*  
  
 如果您已啟用電子郵件通知，您會收到一則通知，其中包含**備份迴圈的數目**和**保留迴圈的數目**。 如果通知中這兩個資料行的傳回值有一個或兩者皆為零，可能表示系統無回應。  
  
> [!WARNING]  
>  產生報表結果的內部處理序會假設引擎診斷記錄位於 SQL 代理程式錯誤記錄檔的相同位置，此位置預設位在與 SQL Server 執行個體的錯誤記錄檔相同的資料夾。 如果引擎診斷記錄移到非 SQL 代理程式錯誤記錄檔位置的其他位置，系統就會找不到智慧型備份診斷記錄，因此電子郵件通知中的報表可能會不正確。 例如，您可能會在所有報告的欄位中看到值為**0** ，包括備份迴圈的數目和保留迴圈的數目。 在診斷記錄移至不同位置的這個情況下，可能不表示系統不回應，而是系統找不到記錄。 請先確定診斷記錄的位置和 SQL 代理程式錯誤記錄檔位於相同的位置。 若要確認診斷記錄的目前位置，您可以使用[sys.databases dm_os_server_diagnostics_log_configurations](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-server-diagnostics-log-configurations)。 資料行會傳回 `path` 引擎診斷記錄的目前位置。  它應該位於與 SQL Agent 錯誤記錄檔相同的資料夾中。 您可以使用 `dbo.sp_get_sqlagent_properties` 預存程序取得 SQL 代理程式錯誤記錄檔路徑。  
  
 請查看擴充事件記錄中有關錯誤的詳細資料。 修正錯誤或重新啟動 SQL Server Agent，以更正狀態。  
  
  
