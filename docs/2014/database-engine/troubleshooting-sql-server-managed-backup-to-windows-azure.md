---
title: 疑難排解 SQL Server Managed Backup 到 Windows Azure |Microsoft Docs
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
ms.openlocfilehash: a4feb316cf43524fa84734d85bf62631833e26d0
ms.sourcegitcommit: 08b3de02475314c07a82a88c77926d226098e23f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2018
ms.locfileid: "49120065"
---
# <a name="troubleshooting-sql-server-managed--backup-to-windows-azure"></a>針對 SQL Server Managed Backup 到 Windows Azure 進行疑難排解
  本主題說明[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]作業期間，針對其中可能發生的錯誤所使用的工作和工具進行疑難排解。  
  
## <a name="overview"></a>總覽  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]內建有檢查和疑難排解程序，所以在許多情況中，內部失敗會由[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]程序自行處理。  
  
 以刪除備份檔案為例，此作業會造成記錄鏈結中斷，進而影響復原能力；在此情況下，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會找出中斷的記錄鏈結，然後排程備份為立即執行。 不過，建議您監視狀態及處理需要手動介入的所有錯誤。  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]使用系統預存程序、系統檢視和擴充事件記錄事件和錯誤。 系統檢視和預存程序皆提供[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]組態資訊、備份排程備份的狀態，以及擴充事件所擷取到的錯誤。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會使用擴充事件擷取錯誤，供疑難排解之用。 刪除記錄事件之外，SQL Server Smart Admin 原則會提供電子郵件通知工作所使用的健康情況，以提供通知或錯誤與問題。 如需詳細資訊，請參閱[監視 SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)。  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]也會使用手動備份至 Windows Azure 儲存體時所用的同一份記錄 (SQL Server 備份至 URL)。 如需有關備份至 URL 的詳細資訊相關的問題，請參閱疑難排解一節[SQL Server 備份至 URL 的最佳作法和疑難排解](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
### <a name="general-troubleshooting-steps"></a>一般疑難排解步驟  
  
1.  啟用電子郵件通知，開始接收錯誤和警告的電子郵件。  
  
     此外，您也可以定期執行 `smart_admin.fn_get_health_status`，藉以檢查彙總錯誤和計數。 例如，`number_of_invalid_credential_errors` 是智慧型備份嘗試備份，但卻得到無效認證錯誤的次數。 `Number_of_backup_loops` 和 `number_of_retention_loops` 不是錯誤；他們會指出備份執行緒與保留執行緒掃描資料庫清單的次數。 通常，當@begin_time和@end_time我們通常應該會看到這些兩個資料行的非零值則是未提供，此函式會顯示過去 30 分鐘內的資訊。 若出現零值，有可能是系統過載或甚至是系統無回應。 如需詳細資訊，請參閱 <<c0>  **疑難排解系統問題**本主題稍後的章節。  
  
2.  檢閱擴充事件記錄，了解錯誤和其他相關事件的詳細資料。  
  
3.  使用此記錄中的資訊解決問題。  當系統發生問題或錯誤時，可能必須重新啟動服務或 SQL Server Agent。  
  
### <a name="common-causes-of-errors"></a>錯誤常見原因  
 下列清單是導致失敗的常見原因：  
  
1.  **變更 SQL 認證：** 如果使用的認證名稱[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]已變更或刪除它，如果[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]將無法進行備份。 此變更應套用到[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]組態設定。  
  
2.  **對儲存體存取金鑰值：** 儲存體金鑰值變更為 Windows Azure 帳戶，但 SQL 認證未更新為新的值，如果[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]至儲存體中，驗證會失敗，備份會失敗設定為使用此帳戶的資料庫。  
  
3.  **變更 Windows Azure 儲存體帳戶：** 刪除或重新命名儲存體帳戶，沒有 SQL 認證的對應變更會使[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]失敗以及應採取的任何備份。 如果您刪除儲存體帳戶，請務必為資料庫重新設定有效的儲存體帳戶資訊。 如果儲存體帳戶已重新命名，或已變更金鑰值，請確定這些變更會反映在[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]使用的 SQL 認證上。  
  
4.  **資料庫屬性變更：** 變更復原模式，或變更名稱可能會導致備份失敗。  
  
5.  **變更復原模式：** 如果資料庫的復原模式從完整或大量記錄變更為簡單，備份將會停止，並會略過該資料庫，藉由[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 如需詳細資訊，請參閱[SQL Server Managed Backup to Windows Azure： 互通性與共存性](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
### <a name="most-common-error-messages-and-solutions"></a>最常見的錯誤訊息和解決方案  
  
1.  **啟用或設定時的錯誤[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:**  
  
     錯誤：「無法存取儲存體 URL…。 請提供有效的 SQL 認證...」 ： 您可能會看到此錯誤和其他類似的錯誤，指的 SQL 認證。  在此情況下，檢閱您提供的 SQL 認證，以及資訊儲存在 SQL 認證-儲存體帳戶名稱和儲存體存取金鑰的名稱，並確定它們是最新且有效。  
  
     錯誤: 「... 無法設定資料庫...，因為它是系統資料庫 」: 您會看到這個錯誤，如果您嘗試啟用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]系統資料庫。  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]不支援系統資料庫的備份。  若要設定系統資料庫的備份，請使用其他 SQL Server 備份技術 (例如維護計劃)。  
  
     錯誤: 「... 提供的保留期限...」 ： 如果您沒有指定資料庫或執行個體的保留期間當您第一次設定這些值您可能會看到有關保留期限的錯誤。 如果您提供的值不是 1 到 30 之間的數字，也可能會看到錯誤。 保留期限的允許值是 1 到 30 之間的數字。  
  
2.  **電子郵件通知錯誤：**  
  
     錯誤: 「 Database Mail 未啟用...」 – 如果您啟用電子郵件通知，但是執行個體上未設定 Database Mail，您會看到這個錯誤。 您必須在執行個體上設定 Database Mail，以接收[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的健康情況通知。 如需有關如何啟用 database mail 的資訊，請參閱[設定 Database Mail](../relational-databases/database-mail/configure-database-mail.md)。 您也必須啟用 SQL Server Agent 以使用 Database Mail 進行通知。 如需詳細資訊，請參閱 <<c0> [ 在您開始前](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md#BeforeYouBegin)。  
  
     下列清單列出和電子郵件通知相關的錯誤號碼：  
  
    -   錯誤號碼： 45209  
  
    -   錯誤號碼： 45210  
  
    -   錯誤號碼：45211  
  
3.  **連線錯誤：**  
  
    -   **與 SQL 連線相關的錯誤：** 連接到 SQL Server 執行個體的問題時，會發生這些錯誤。 擴充的事件會透過管理通道公開這些錯誤類型。 以下是您可能會看到與此種連接問題相關之錯誤的兩個擴充事件：  
  
         FileRetentionAdminXEvent，且 event_type = SqlError。 如需有關此錯誤的詳細資料，請參閱該事件的 error_code、error_message 和 stack_trace。 error_code 是 SqlException 的錯誤號碼。  
  
         具有下列訊息/訊息前置詞的 SmartBackupAdminXevent：  
  
         *「 設定 SQL Server Managed Backup to Windows Azure 預設設定時，發生內部錯誤執行個體。錯誤可能是暫時性。 」*  
  
         *「 可能會發生與 SQL Server 的連線問題。正在略過目前的反覆項目中的資料庫。 」*  
  
         *「 查詢失敗的記錄檔使用量資訊。失敗可能為暫時性。正在略過目前的反覆項目中的資料庫。 」*  
  
         *「 載入 SSMBackup2WA 代理程式的中繼資料時發生 SQL 例外狀況。失敗可能為暫時性。作業將會重試。 」*  
  
         *「 SSMBackup2WA 遇到 SQL 例外狀況時..."*  
  
    -   **連接至儲存體帳戶時發生錯誤：**  
  
         FileRetentionAdminXEvent 中回報了儲存體例外狀況，且 event_type = XstoreError。 如需有關此錯誤的詳細資料，請參閱該事件的 error_message 和 stack_trace。  
  
         因為 SQL Server Managed Backup 會使用基礎的「備份至 URL」技術，所以與儲存體連接相關的錯誤適用於這兩項功能。 如需有關疑難排解步驟的詳細資訊，請參閱 <<c0>  **疑難排解小節**的[SQL Server 備份至 URL 的最佳作法和疑難排解](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)文章。  
  
### <a name="troubleshooting-system-issues"></a>疑難排解系統問題  
 下列案例指出系統 (SQL Server、SQL Server Agent) 發生問題的案例及其對[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的影響：  
  
-   **Sqlservr.exe 會停止回應或停止運作時[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]正在執行：** 如果 SQL Server 停止運作，SQL 代理程式將會正常關閉，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]也停駐點，並將事件記錄到 SQL Agent.out 檔案中。  
  
     如果 SQL Server 停止回應，事件會記錄到管理通道。  以下是事件記錄檔的範例：  
  
     *Sql 錯誤 (引擎無回應或收到 sqlException: SqlException:*   
     *錯誤碼、 訊息和堆疊追蹤會顯示在管理通道 xevent，外加一些額外的資訊，例如：*   
    *「 可能會發生與 SQL Server 的連線問題。正在略過目前的反覆項目中的資料庫 」*  
  
-   **SQL 代理程式停止回應或停止運作時[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]執行：**  
  
     如果 SQL Agent 停止運作，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]也會停止，並將事件記錄到管理通道。 這與 SQL Server 停止回應的案例類似。  
  
     如果 SQL Agent 停止回應，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]將無法繼續執行備份作業，事件也會記錄到管理通道。 以下是事件記錄檔的範例：  
  
     *作業停止回應： 請參閱管理通道的 xevent*   
    *「 進度更新尚未收到來自 SQL Server 中多個 」 + Constants.DBBackupInfoMsgMaxWaitTime + 「 小時的資料庫備份。 SSM 雲端備份將繼續等候。 」*  
  
 如果您已啟用電子郵件通知，您會收到通知，其中包含**備份迴圈的數目**並**保留迴圈的數目**。 如果通知中這兩個資料行的傳回值有一個或兩者皆為零，可能表示系統無回應。  
  
> [!WARNING]  
>  產生報表結果的內部處理序會假設引擎診斷記錄位於 SQL 代理程式錯誤記錄檔的相同位置，此位置預設位在與 SQL Server 執行個體的錯誤記錄檔相同的資料夾。 如果引擎診斷記錄移到非 SQL 代理程式錯誤記錄檔位置的其他位置，系統就會找不到智慧型備份診斷記錄，因此電子郵件通知中的報表可能會不正確。 例如，您可能會看到的值**0**回報的所有欄位的 包括備份迴圈的數目和保留迴圈的數目。 在診斷記錄移至不同位置的這個情況下，可能不表示系統不回應，而是系統找不到記錄。 請先確定診斷記錄的位置和 SQL 代理程式錯誤記錄檔位於相同的位置。 若要確認診斷記錄檔的目前位置，您可以使用[sys.dm_os_server_diagnostics_log_configurations](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-server-diagnostics-log-configurations)。 `path`資料行會傳回引擎的目前位置診斷的記錄檔。  它應該是相同的 SQL Agent 錯誤記錄檔的資料夾中。 您可以使用 `dbo.sp_get_sqlagent_properties` 預存程序取得 SQL 代理程式錯誤記錄檔路徑。  
  
 請查看擴充事件記錄中有關錯誤的詳細資料。 修正錯誤或重新啟動 SQL Server Agent，以更正狀態。  
  
  
