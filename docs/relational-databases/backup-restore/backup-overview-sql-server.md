---
title: 備份概觀 (SQL Server) | Microsoft Docs
description: 了解 SQL Server 備份元件，包括備份類型與限制，以及備份裝置和備份媒體。
ms.custom: ''
ms.date: 07/15/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server], backing up data
- backups [SQL Server]
- database backups [SQL Server]
- backup types [SQL Server]
- data backups [SQL Server]
- backing up tables [SQL Server]
- database restores [SQL Server], backups
- backing up [SQL Server], about backing up
- restoring [SQL Server], backup types
- backups [SQL Server], about
- backups [SQL Server], table-level backups unsupported
ms.assetid: 09a6e0c2-d8fd-453f-9aac-4ff24a97dc1f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6cae13ac9137a7c7f47e9574367115d6133338be
ms.sourcegitcommit: 9afb612c5303d24b514cb8dba941d05c88f0ca90
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/28/2020
ms.locfileid: "82220491"
---
# <a name="backup-overview-sql-server"></a>Backup Overview (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題介紹 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份元件。 備份 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫對於保護資料非常重要。 此討論涵蓋備份類型和備份限制。 本主題同時介紹 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份裝置和備份媒體。  
  
  
## <a name="terms"></a>詞彙
 
 **備份 (back up) [動詞]**  
 將資料或記錄檔記錄從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫或其交易記錄複製至備份裝置 (例如磁碟)，以建立資料備份或記錄備份。  
  
**備份 (backup) [名詞]**  
 失敗後可用來還原和復原資料的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料副本。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料備份會在資料庫層級或者一個或多個資料庫檔案或檔案群組層級建立。 無法建立資料表層級備份。 除了資料備份之外，完整復原模式也需要建立交易記錄備份。  
  
**[復原模式](../../relational-databases/backup-restore/recovery-models-sql-server.md)**  
 控制資料庫上交易記錄維護的資料庫屬性。 復原模式共有三種：簡單、完整和大量記錄。 資料庫的復原模式決定其備份和還原需求。  
  
 **[還原](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)**  
 一個多階段的程序，它會將指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份中的所有資料和記錄頁面複製到指定的資料庫中，然後藉由套用所記錄的變更取得前面時段的資料，向前復原備份中記錄的所有交易。  
  
 ## <a name="types-of-backups"></a>備份類型  
  
 **[僅複製備份](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)**  
 不受 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一般備份順序影響的特殊用途備份。  
  
**資料備份**   
 整個資料庫 (資料庫備份)、部分資料庫 (部分備份) 或是一組資料檔案或檔案群組 (檔案備份) 中資料的備份。  
  
**[資料庫備份](../../relational-databases/backup-restore/full-database-backups-sql-server.md)**  
 資料庫的備份。 完整資料庫備份代表備份完成時的整個資料庫。 差異資料庫備份僅包含自其最近的完整資料庫備份以來，對資料庫所做的變更。  
  
 **[差異備份](../../relational-databases/backup-restore/full-database-backups-sql-server.md)**  
 一種資料備份，是以整個或部分資料庫或一組資料檔案或檔案群組 (「差異基底」  ) 的最新完整備份為基礎，而且只包含自差異基底以來變更的資料範圍。  
  
 差異部分備份僅記錄自上一次部分備份後在檔案群組中變更過的資料範圍，稱為差異基底。  
  
**完整備份**  
 一種資料備份，包含特定資料庫或一組檔案群組或檔案中的所有資料，也包含足以讓這個資料復原的記錄。  
  
**[記錄備份](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)**  
 交易記錄的備份，包含先前的記錄備份中未備份的所有記錄。 (完整復原模式)  
  
 **[檔案備份](../../relational-databases/backup-restore/full-file-backups-sql-server.md)**  
 一個或多個資料庫檔案或檔案群組的備份。  
  
 **[部分備份](../../relational-databases/backup-restore/partial-backups-sql-server.md)**  
 僅包含資料庫中某些檔案群組中的資料，包括主要檔案群組、每個讀取/寫入檔案群組，以及任何選擇性指定之唯讀檔案中的資料。  
  
## <a name="backup-media-terms-and-definitions"></a>備份媒體詞彙和定義  
  
 **[備份裝置](../../relational-databases/backup-restore/backup-devices-sql-server.md)**  
 寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份並從中進行還原的磁碟或磁帶裝置。 SQL Server 備份也可以寫入 Azure Blob 儲存體服務，而且會使用 **URL** 格式來指定備份檔案的目的地和名稱。 如需詳細資訊，請參閱 [SQL Server 備份及還原與 Microsoft Azure Blob 儲存體服務](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
 **[備份媒體](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 已寫入一個或多個備份的一個或多個磁帶或磁碟檔案。  
  
 **[備份組](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 透過成功的備份作業，加入至媒體集的備份內容。  
  
 **[媒體家族](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 在單一非鏡像裝置上或媒體集的一組鏡像裝置上所建立的備份。  
  
 **[媒體集](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 按順序排列的備份媒體集合 (磁帶或磁碟檔案)，由一個或多個備份作業使用固定的備份裝置類型與數量寫入。  
  
 **[鏡像媒體集](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)**  
 多份媒體集副本 (鏡像)。  
  
##  <a name="backup-compression"></a><a name="BackupCompression"></a> 備份壓縮  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 和更新版本支援壓縮備份，而 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本可以還原壓縮的備份。 如需詳細資訊，請參閱[備份壓縮 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)。  
  
##  <a name="backup-operations-restrictions"></a><a name="Restrictions"></a>  備份作業限制 
 可在資料庫仍在線上運作以及正在使用中的時候進行備份。 不過，會有下列限制：  
  
### <a name="cannot-back-up-offline-data"></a>無法備份離線資料  
 隱含或明確參考離線資料的任何備份作業都會失敗。 一些典型的例子如下：  
  
-   要求進行完整資料庫備份，但資料庫的一個檔案群組為離線狀態。 因為所有檔案群組是明確納入在完整資料庫備份中，所以此作業會失敗。  
  
     若要備份這個資料庫，您可以使用檔案備份，並且指定只限在線上的檔案群組。  
  
-   您要求進行部分備份，但讀取/寫入檔案群組處於離線狀態。 因為部分備份需要所有的讀取/寫入檔案群組，所以此作業會失敗。  
  
-   要求進行特定檔案的檔案備份，但其中一個檔案不在線上。 該作業會失敗。 若要備份線上檔案，您可以省略檔案清單中的離線檔案，然後重複該作業。  
  
 一般而言，即使有一個或多個資料檔案無法使用，記錄備份都會成功。 不過，如果在大量記錄復原模式下變更任何包含大量記錄的檔案，則必須所有檔案都在線上，才能讓備份成功。  
  
### <a name="concurrency-restrictions"></a>並行限制   
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 利用線上備份處理序，使您能夠在資料庫處於使用狀態時備份資料庫。 在備份期間，您可以執行大部分的作業；例如，在備份作業期間，您可以執行 INSERT、UPDATE 或 DELETE 陳述式。 不過，如果試圖在建立或刪除資料庫檔案過程中啟動備份作業，則備份作業會等候到建立或刪除作業完成，或備份逾時為止。  
  
 資料庫備份或交易記錄備份期間所無法執行的作業包括：  
  
-   檔案管理作業，例如，含有 ADD FILE 或 REMOVE FILE 選項的 ALTER DATABASE 陳述式。  
  
-   壓縮資料庫或壓縮檔案的作業。 其中包括自動壓縮作業。  
  
-   如果在備份作業進行當中試圖建立或刪除資料庫檔案，建立或刪除作業會失敗。  
  
 如果備份作業與檔案管理或壓縮作業重疊，便會發生衝突。 不論哪一個衝突的作業先開始，第二項作業都會等候第一項作業設定的鎖定逾時(逾時期間由工作階段逾時設定控制)。如果在逾時期間解除鎖定，第二項作業就會繼續下去。 如果鎖定逾時，第二項作業就會失敗。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Related tasks  
 **備份裝置和備份媒體**  
  
-   [定義磁碟檔案的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [定義磁帶機的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [指定磁碟或磁帶作為備份目的地 &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [刪除備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [設定備份的到期日 &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [檢視備份磁帶或檔案的內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [檢視備份組中的資料和記錄檔 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [從裝置還原備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
-   [教學課程：SQL Server 備份及還原至 Azure Blob 儲存體服務](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
 **建立備份**  
  
> [!NOTE]  
>  如果是部分備份或只複製備份，就必須分別搭配 PARTIAL 或 COPY_ONLY 選項來使用 [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md) 陳述式。  
  
-   [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [備份檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [建立差異資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [資料庫損毀時備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [在備份或還原期間啟用或停用備份總和檢查碼 &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [指定在發生錯誤後備份或還原作業應該繼續還是停止 &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
-   [使用資源管理員進行備份壓縮，以限制 CPU 使用率 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [教學課程：SQL Server 備份及還原至 Azure Blob 儲存體服務](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="and-more"></a>更多！ 
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [維護計畫](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [復原模式 &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  
