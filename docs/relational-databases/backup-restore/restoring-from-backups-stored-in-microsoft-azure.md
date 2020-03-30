---
title: 從儲存在 Microsoft Azure 的備份還原 | Microsoft 文件
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6ae358b2-6f6f-46e0-a7c8-f9ac6ce79a0e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cda4fd3fa0bbb66e95d61ec87ff66dee809e2962
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "70155446"
---
# <a name="restoring-from-backups-stored-in-microsoft-azure"></a>從儲存在 Microsoft Azure 的備份還原
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題概要說明使用儲存在 Azure Blob 儲存體服務中的備份來還原資料庫時，所應注意的事項。 本文適用於使用 SQL Server 備份至 URL 備份或 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]所建立的備份。  
  
 如果您預計要還原儲存在 Azure Blob 儲存體服務中的備份，建議您檢閱本主題，然後再檢閱說明如何還原資料庫的步驟 (此程序對於內部部署和 Azure 備份是相同的)。  
  
## <a name="overview"></a>概觀  
 從內部部署備份還原資料庫所使用的工具和方法，適用於從雲端備份還原資料庫。  下列小節描述這些考量，以及當您使用儲存在 Azure Blob 儲存體服務中的備份時，應了解的任何差異。  
  
### <a name="using-transact-sql"></a>使用 TRANSACT-SQL  
  
-   因為 SQL Server 必須連接至外部來源以擷取備份檔案，所以會使用 SQL 認證來驗證儲存體帳戶。 因此，RESTORE 陳述式需要 WITH CREDENTIAL 選項。 如需詳細資訊，請參閱 [SQL Server 備份及還原與 Microsoft Azure Blob 儲存體服務](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
-   如果您是使用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 管理雲端的備份，您可以使用 **smart_admin.fn_available_backups** 系統函數來檢閱儲存體中的所有可用備份。 此系統函數會以資料表傳回資料庫的所有可用備份。 由於結果是以資料表傳回，因此您可以篩選或排序結果。 如需詳細資訊，請參閱 [managed_backup.fn_available_backups &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql.md)。  
  
### <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio  
  
-   此還原工作使用 SQL Server Management Studio 來還原資料庫。 備份媒體頁面現在包含 [URL]  選項，以顯示儲存在 Azure Blob 儲存體服務中的備份檔案。 您也必須提供用來驗證儲存體帳戶的 SQL 認證。 [要還原的備份組]  方格接著會填入 Azure Blob 儲存體中的可用備份。 如需詳細資訊，請參閱[使用 SQL Server Management Studio 從 Azure 儲存體還原](../../relational-databases/backup-restore/sql-server-backup-to-url.md#RestoreSSMS)。  
  
### <a name="optimizing-restores"></a>最佳化還原  
 若要減少還原寫入時間，請將 [執行磁碟區維護工作]  使用者權限加入至 SQL Server 使用者帳戶。 如需詳細資訊，請參閱 [資料庫檔案初始化](https://go.microsoft.com/fwlink/?LinkId=271622)。 如果開啟立即檔案初始化功能之後，還原速度仍然很慢，請查看資料庫備份所在之執行個體上的記錄檔大小。 如果記錄檔大小很大 (數以 GB)，還原速度應該就會很慢。 在還原期間，記錄檔必須歸零，因此需要大量時間。  
  
 若要減少還原時間，建議您使用壓縮的備份。  如果備份大小超過 25 GB，請使用 [AzCopy 公用程式](https://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx) 下載到本機磁碟機，然後執行還原。 如需其他備份最佳做法與建議，請參閱 [SQL Server 備份至 URL 的最佳做法和疑難排解](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)。  
  
 當您執行還原時，也可以開啟追蹤旗標 3051，以產生詳細的記錄檔。 此記錄檔會置於記錄檔目錄中，並使用下列格式命名：BackupToUrl-\<執行個體>-\<資料庫名稱>-action-\<PID>.log。 此記錄檔包含對 Azure 儲存體之每個來回行程的相關資訊 (包括時間點)，有助於診斷問題。  
  
### <a name="topics-on-performing-restore-operations"></a>關於執行還原作業的主題  
  
-   [完整資料庫還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [完整資料庫還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)  
  
-   [檔案還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)  
  
-   [檔案還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)  
  
-   [分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
