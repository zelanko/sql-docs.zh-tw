---
title: SQL Server 備份至 URL 的最佳做法和疑難排解 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: de676bea-cec7-479d-891a-39ac8b85664f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6eb2d66203de226cd7ab414c97ecc219717573a0
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154667"
---
# <a name="sql-server-backup-to-url-best-practices-and-troubleshooting"></a>SQL Server 備份至 URL 的最佳作法和疑難排解
  本主題包含 SQL Server 備份和還原至 Azure Blob 服務的最佳做法和疑難排解秘訣。  
  
 如需有關使用 Azure Blob 儲存體服務進行 SQL Server 備份或還原作業的詳細資訊, 請參閱:  
  
-   [使用 Azure Blob 儲存體服務 SQL Server 備份和還原](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
-   [教學課程：SQL Server 備份和還原至 Azure Blob 儲存體服務](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="managing-backups"></a>管理備份  
 下列清單包含管理備份的一般建議：  
  
-   建議針對每個備份使用唯一的檔案名稱，避免不小心覆寫 Blob。  
  
-   建立容器時，建議您將存取層級設定為 [私用]，如此只有能夠提供必要驗證資訊的使用者或帳戶才能讀取或寫入容器中的 Blob。  
  
-   針對在 Azure 虛擬機器中執行 SQL Server 實例上 SQL Server 資料庫, 請使用與虛擬機器位於相同區域中的儲存體帳戶, 以避免區域之間的資料傳輸成本。 使用相同的地區也可以確保備份與還原作業達到最佳效能。  
  
-   失敗的備份活動可能會產生無效的備份檔案。 我們建議您定期識別失敗的備份並刪除 Blob 檔案。 如需詳細資訊，請參閱[刪除擁有使用中租用的備份 Blob 檔案](deleting-backup-blob-files-with-active-leases.md)  
  
-   在備份期間使用 `WITH COMPRESSION` 選項可以將您的儲存體成本和儲存體交易成本降到最低程度。 它也可以減少完成備份程序所需的時間。  
  
## <a name="handling-large-files"></a>處理大型檔案  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]備份作業會使用多個執行緒來優化 Azure Blob 儲存體服務的資料傳輸。  不過，其效能取決於各種因素，例如 ISV 頻寬和資料庫的大小。 如果您計畫要備份內部部署 SQL Server 資料庫中的大型資料庫或檔案群組，建議您先進行一些輸送量測試。 [Azure 儲存體 SLA](https://go.microsoft.com/fwlink/?LinkId=271619)具有 blob 的最長處理時間, 您可以將其納入考慮。  
  
-   備份大型檔案時，務必遵循**管理備份**一節中的建議使用 `WITH COMPRESSION` 選項。  
  
## <a name="troubleshooting-backup-to-or-restore-from-url"></a>疑難排解備份至 URL 或從中還原  
 以下是一些快速的方法, 可在備份至 Azure Blob 儲存體服務或從中還原時, 針對錯誤進行疑難排解。  
  
 為避免由於不支援的選項或限制而發生錯誤, 請參閱[SQL Server 備份和還原與 Azure Blob 儲存體服務](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)一文中的限制清單, 以及支援 BACKUP 和 restore 命令的資訊。  
  
 **驗證錯誤：**  
  
-   WITH CREDENTIAL 是新的選項, 而且需要備份至 Azure Blob 儲存體服務或從中還原。 與認證有關的失敗可能包括：  
  
     `BACKUP` 或 `RESTORE` 命令中指定的認證不存在。 若要避免此問題，您可以在 Backup 陳述式中加入 T-SQL 陳述式來建立認證 (如果認證不存在的話)。 以下是您可以使用的範例：  
  
    ```  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL <credential name> WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key> ;  
  
    ```  
  
-   認證存在，但是用來執行 Backup 命令的登入帳戶沒有存取認證的權限。 請使用具備 **更改任何認證** 權限的 **db_backupoperator** 角色登入帳戶。  
  
-   確認儲存體帳戶名稱與金鑰值。 儲存在認證中的資訊必須符合您在備份和還原作業中使用之 Azure 儲存體帳戶的屬性值。  
  
 **備份錯誤/失敗：**  
  
-   相同 Blob 的平行備份會導致其中一個備份失敗並出現 [初始化失敗] 錯誤。  
  
-   使用下列錯誤記錄來協助疑難排解備份錯誤：  
  
    -   您可以使用下列格式來設定追蹤旗標 3051，以便記錄至特定錯誤記錄：  
  
         BackupToUrl-\<執行個體>-\<資料庫名稱>-action-\<PID>.log 其中 \<action> 是下列其中之一：  
  
        -   `DB`  
  
        -   `FILELISTONLY`  
  
        -   `LABELONLY`  
  
        -   `HEADERONLY`  
  
        -   `VERIFYONLY`  
  
    -   您也可以藉由查看 Windows 事件記錄檔 (位於名為 ' SQLBackupToUrl ' 的應用程式記錄底下) 來尋找資訊。  
  
-   從壓縮備份還原時，您可能會看見下列錯誤：  
  
    -   **發生 SqlException 3284。嚴重性：16狀態:5**  
        **裝置 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak ' 上的訊息標記未對齊。以用來建立 backupset 的相同區塊大小重新發出 Restore 語句:' 65536 ' 看起來像是可能的值。**  
  
         若要解決此錯誤，請重新發出指定 `BACKUP` 的 `BLOCKSIZE = 65536` 陳述式。  
  
-   含有使用中租用的 Blob 導致備份期間發生錯誤：失敗的備份活動可能會產生含有使用中租用的 Blob。  
  
     如果重新嘗試執行 Backup 陳述式，備份作業可能會失敗並出現類似以下的錯誤：  
  
     **Backup to URL 收到遠端端點的例外狀況。例外狀況訊息:遠端伺服器傳回錯誤：(412) blob 目前有租用, 而且要求**中未指定租用識別碼。  
  
     如果針對擁有使用中租用的備份 Blob 檔案執行 Restore 陳述式，還原作業會失敗並出現類似以下的錯誤：  
  
     **例外狀況訊息:遠端伺服器傳回錯誤：(409) 衝突。。**  
  
     發生這類錯誤時，您必須刪除 Blob 檔案。 如需有關此案例以及如何更正這個問題的詳細資訊，請參閱 [刪除擁有使用中租用的備份 Blob 檔案](deleting-backup-blob-files-with-active-leases.md)  
  
## <a name="proxy-errors"></a>Proxy 錯誤  
 如果您使用 Proxy 伺服器存取網際網路，可能會看見下列問題：  
  
 **Proxy 伺服器連線節流：**  
  
 Proxy 伺服器可能有限制每分鐘連接數目的設定。 備份至 URL 處理序是一個多執行緒處理序，因此可能會超出此限制。 如果發生這種情況，Proxy 伺服器會清除該連接。 若要解決這個問題，請變更 Proxy 設定，讓 SQL Server 不使用 Proxy。   以下是您可能在錯誤記錄檔中看到的類型或錯誤訊息的部分範例：  
  
-   "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak " 的寫入失敗:備份至 URL 收到來自遠端端點的例外狀況。 例外狀況訊息:無法從傳輸連線讀取資料:連接已關閉。  
  
-   檔案 "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak: " 上發生無法復原的 I/O 錯誤。無法從遠端端點收集錯誤。  
  
     訊息 3013，層級 16，狀態 1，行 2  
  
     備份資料庫正在異常結束。  
  
-   BackupIoRequest:: ReportIoError: 備份裝置 'http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak ' 上的寫入失敗。 作業系統錯誤。備份至 URL 時收到來自遠端端點的例外狀況。 例外狀況訊息:無法從傳輸連線讀取資料:連接已關閉。  
  
 如果您使用追蹤旗標 3051 開啟詳細資訊記錄，可能也會在記錄檔中看到下列資訊：  
  
 HTTP 狀態碼 502，HTTP 狀態訊息 Proxy 錯誤 (每分鐘 HTTP 要求數目超過設定的限制。 請連絡您的 ISA Server 系統管理員。  )  
  
 **預設 Proxy 設定未收取：**  
  
 有時未收取到預設值，導致 Proxy 驗證錯誤，如下所示：*檔案 "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak: " 上發生無法復原的 I/O 錯誤。備份至 URL 時收到來自遠端端點的例外狀況。例外狀況訊息:遠端伺服器傳回錯誤：(407)**需要 Proxy 驗證。***  
  
 若要解決這個問題，使用下列步驟建立組態檔，讓備份至 URL 處理序可以使用預設 Proxy 設定：  
  
1.  建立具有下列 xml 的組態檔，名稱為 BackuptoURL.exe.config：  
  
    ```  
    <?xml version ="1.0"?>  
    <configuration>   
                    <system.net>   
                                    <defaultProxy enabled="true" useDefaultCredentials="true">   
                                                    <proxy usesystemdefault="true" />   
                                    </defaultProxy>   
                    </system.net>  
    </configuration>  
  
    ```  
  
2.  將組態檔放在 SQL Server 執行個體的 Binn 資料夾。 例如, 如果我的 SQL Server 安裝在電腦的 C 磁片磁碟機上, 請將設定檔放在此處:*C:\Program FILES\MICROSOFT SQL Server\MSSQL12。InstanceName\<> \MSSQL\Binn*。  
  
## <a name="troubleshooting-sql-server-managed-backup-to-azure"></a>針對 SQL Server 受控備份至 Azure 進行疑難排解  
 因為 SQL Server Managed Backup 會建置在「備份至 URL」之上，所以稍早章節所述的疑難排解提示適用於使用 SQL Server Managed Backup 的資料庫或執行個體。  針對[SQL Server 受控備份至 azure](sql-server-managed-backup-to-microsoft-azure.md)中的疑難排解, 會詳細說明針對 SQL Server 受控備份至 azure 進行疑難排解的相關資訊。  
  
## <a name="see-also"></a>另請參閱  
 [從儲存在 Azure 中的備份還原](restoring-from-backups-stored-in-microsoft-azure.md)  
  
  
