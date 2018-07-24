---
title: SQL Server Managed Backup to Microsoft Azure | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: afa01165-39e0-4efe-ac0e-664edb8599fd
caps.latest.revision: 44
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ac4d76ceb3bcbd3042e4fb4d7f1fa42ceda44860
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983380"
---
# <a name="sql-server-managed-backup-to-microsoft-azure"></a>SQL Server Managed Backup to Microsoft Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會管理 SQL Server 備份，並自動備份到 Windows Azure Blob 儲存體。 您可以選擇讓 SQL Server 根據資料庫的交易工作負載來決定備份排程。 或者，您可以使用進階選項來定義排程。 保留設定可決定在 Azure Blob 儲存體中儲存備份的時間長度。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 支援指定保留時間週期的時間點還原。  
  
 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]開始， [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的程序和基礎行為已變更。 如需詳細資訊，請參閱 [Migrate SQL Server 2014 Managed Backup Settings to SQL Server 2016](../../relational-databases/backup-restore/migrate-sql-server-2014-managed-backup-settings-to-sql-server-2016.md)。  
  
> [!TIP]  
>  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 針對在 Windows Azure 虛擬機器上執行的 SQL Server 執行個體建議使用。  
  
## <a name="benefits"></a>優點  
 目前自動份分多個資料庫需要制定備份策略、撰寫自訂程式碼及排程備份。 使用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]，您可以藉由只指定保留期限和儲存體位置，來建立備份計劃。 雖然可以使用進階設定，但它們並非必要。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會排程、執行及維護備份。  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 可以在資料庫層級或 SQL Server 執行個體層級設定。 在執行個體層級設定時，也會自動備份所有新的資料庫。 資料庫層級的設定可用來覆寫個別案例上的執行個體層級預設值。  
  
 您也可以加密備份來提供額外的安全性，並在產生備份時，設定要控制的自訂排程。 如需如何針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份使用 Microsoft Azure Blob 儲存體之優點的詳細資訊，請參閱 [使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
##  <a name="Prereqs"></a> 必要條件  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會使用 Microsoft Azure 儲存體來儲存備份檔案。 下列必要條件是必備的：  
  
|必要條件|Description|  
|------------------|-----------------|  
|**Microsoft Azure 帳戶**|您可以在瀏覽 [購買選項](http://azure.microsoft.com/pricing/free-trial/) 之前，利用 [免費試用版](http://azure.microsoft.com/pricing/purchase-options/)來開始。|  
|**Azure 儲存體帳戶**|備份會儲存在與 Azure 儲存體帳戶相關聯的 Azure Blob 儲存體中。 如需建立儲存體帳戶的逐步指示，請參閱 [關於 Azure 儲存體帳戶](http://azure.microsoft.com/documentation/articles/storage-create-storage-account/)。|  
|**Blob 容器**|Blob 會組織於容器中。 您會指定適用於備份檔案的目標容器。 您可以在 [Azure 管理入口網站](https://manage.windowsazure.com/)中建立一個容器，或者使用 **New-AzureStorageContainer**[Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/) 命令。|  
|**共用存取簽章 (SAS)**|目標容器的存取權是由共用存取簽章 (SAS) 所控制。 如需 SAS 概觀，請參閱 [共用存取簽章，第 1 部分：了解 SAS 模型](http://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)。 您可以在程式碼中或使用 **New-AzureStorageContainerSASToken** PowerShell 命令，建立 SAS 權杖。 如需簡化此程序的 PowerShell 指令碼，請參閱 [在 Azure 儲存體上使用共用存取簽章 (SAS) 權杖搭配 Powershell 簡化 SQL 認證的建立](http://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx)。 SAS 權杖可以儲存在 **SQL 認證** 中，搭配 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]一起使用。|  
|**SQL Server Agent**|SQL Server Agent 必須針對 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 執行，才能運作。 請考慮將自動啟動選項設定為自動化。|  
  
## <a name="components"></a>Components  
 Transact-SQL 是與 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]互動的主要介面。 系統預存程序可用來啟用、設定及監視 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 系統函數可用來擷取現有的組態設定、參數值和備份檔案資訊。 擴充事件可用來呈現錯誤和警告。 警示機制可透過 SQL Agent 作業和 SQL Server 原則式管理加以啟用。 以下是物件清單及其與 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]相關的功能描述。  
  
 PowerShell 指令程式也可用於設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 SQL Server Management Studio 可使用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] [還原資料庫] **工作，還原** 所建立的備份  
  
|||  
|-|-|  
|系統物件|Description|  
|**MSDB**|儲存 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]所建立之所有備份的中繼資料與備份記錄。|  
|[managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)|啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。|  
|[managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)|設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的進階設定，例如加密。|  
|[managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)|建立 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的自訂排程。|  
|[managed_backup.sp_ backup_master_switch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql.md)|暫停和繼續 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。|  
|[managed_backup.sp_set_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql.md)|啟用和設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的監視。 例如：啟用擴充事件、通知的郵件設定。|  
|[managed_backup.sp_backup_on_demand &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql.md)|執行資料庫的隨選備份，這會使用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 來啟用，而不會中斷記錄鏈結。|  
|[managed_backup.fn_backup_db_config &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-backup-db-config-transact-sql.md)|傳回資料庫或執行個體上所有資料庫目前的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 狀態和組態值。|  
|[managed_backup.fn_is_master_switch_on &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-is-master-switch-on-transact-sql.md)|傳回主切換的狀態。|  
|[managed_backup.sp_get_backup_diagnostics &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-get-backup-diagnostics-transact-sql.md)|傳回擴充事件所記錄的事件。|  
|[managed_backup.fn_get_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql.md)|傳回備份系統設定 (例如監視以及警示郵件設定) 的目前值。|  
|[managed_backup.fn_available_backups &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql.md)|擷取指定資料庫或執行個體中所有資料庫的可用備份。|  
|[managed_backup.fn_get_current_xevent_settings &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql.md)|傳回目前的擴充事件設定。|  
|[managed_backup.fn_get_health_status &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-health-status-transact-sql.md)|傳回擴充事件對指定期間所記錄的錯誤彙總計數。|  
  
## <a name="backup-strategy"></a>備份策略  
  
### <a name="backup-scheduling"></a>備份排程  
 您可以使用系統預存程序 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)。 如果您未指定自訂的備份排程，排程的備份類型及備份頻率會取決於資料庫的工作負載。 保留週期設定可用於指定備份檔案保留在儲存體中的時間，以及能否將資料庫復原至保留週期內的時間點。  
  
### <a name="backup-file-naming-conventions"></a>備份檔案命名慣例  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會使用您指定的容器，因此您就能控制容器的名稱。 針對備份檔案，非可用性資料庫的命名慣例是使用資料庫名稱的前 40 個字元，加上不含 '-' 的資料庫 GUID 與時間戳記。 區段之間會插入底線字元做為分隔符號。 完整備份會使用副檔名 **.bak** ，記錄備份則會使用 **.log** 。 對於可用性群組資料庫而言，除了上面所述的檔案命名慣例以外，可用性群組資料庫 GUID 會加在資料庫名稱的 40 個字元之後。 可用性群組資料庫 GUID 值是 sys.databases 中的 group_database_id 值。  
  
### <a name="full-database-backup"></a>完整資料庫備份  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 代理程式會進行完整資料庫備份排程。  
  
-   資料庫是第一次啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ，或是在執行個體層級以預設設定啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。  
  
-   最後一次完整資料庫備份後，記錄成長已等於或大於 1 GB。  
  
-   最後一次完整資料庫備份後，已經過一週的最大時間間隔。  
  
-   記錄鏈結中斷。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會藉由比較備份檔案的第一個和最後一個 LSN，定期檢查記錄鏈結是否保持完整。 如果記錄鏈結因故中斷， [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 就會排程完整資料庫備份。 記錄鏈結中斷的最常見原因可能是使用 Transact-SQL 發出的備份命令，或透過 SQL Server Management Studio 中的備份工作。  其他常見的情況包括備份記錄檔的意外刪除，或意外覆寫備份。  
  
### <a name="transaction-log-backup"></a>交易記錄備份  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會進行記錄備份排程：  
  
-   找不到記錄 (log) 備份記錄 (history)。 第一次啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 時，通常會有此情況。  
  
-   使用的交易記錄空間是 5 MB 或更大。  
  
-   達到最後一次記錄備份後的 2 小時最大時間間隔。  
  
-   交易紀錄備份一律會在完整資料庫備份之後執行。 其目的在保留完整備份之前的記錄檔鏈結。  
  
## <a name="retention-period-settings"></a>保留週期設定  
 啟用備份時，必須設定保留週期的天數：最小值是 1 天，最大值是 30 天。  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會根據保留週期設定，評估能否在指定的時間內，復原到某個時間點，從而決定所要保留的備份檔案，以及指定所要刪除的備份檔案。 備份的 backup_finish_date 會用於指定及比對保留週期設定所指定的時間。  
  
## <a name="important-considerations"></a>重要考量因素  
 當資料庫正在執行完整的資料庫備份作業時， [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會等待目前作業完成，然後再為相同的資料庫執行另一個完整的資料庫備份。 同樣地，在指定的時間內，只可執行一個交易記錄備份。 不過，完整資料庫備份與交易記錄備份可以同時執行。 失敗會記錄為擴充事件。  
  
 如果排程超過 10 個並行完整資料庫備份，會透過擴充事件的偵錯通道發出警告。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會維護其優先順序佇列，直到所有的備份均已排程並完成為止。  

> [!NOTE]
> SQL Server Managed Backup 不支援 Proxy 伺服器。
>
  
##  <a name="support_limits"></a> 可支援性  
 下列支援限制和考量專屬於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]：  
  
-   支援 **master**、 **model**和 **msdb** 系統資料庫的備份。 不支援 **tempdb** 的備份。 
  
-   針對 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，支援所有復原模式 (完整、大量記錄和簡單)。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 代理程式只支援資料庫的完整和記錄備份。 不支援檔案備份自動化。  
  
-   Microsoft Azure Blob 儲存體服務是唯一支援的備份儲存體選項。 不支援備份至磁碟或磁帶。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 使用「備份至區塊 Blob」功能。 區塊 Blob 的大小上限為 200 GB。 但藉由使用等量，個別備份的大小上限可高達 12 TB。 如果您的備份需求超過此大小，請考慮使用壓縮，並在設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]之前測試備份檔案大小。 測試方法有兩種：一種是藉由備份到本機磁碟，另一種則是利用 **BACKUP TO URL** Transact-SQL 陳述式手動備份到 Microsoft Azure 儲存體。 如需詳細資訊，請參閱 [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 時，可能會有一些限制。  
  
## <a name="see-also"></a>另請參閱  
- [啟用 SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)   
- [設定 Microsoft Azure 的 SQL Server 受管理備份進階選項](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md)   
- [停用 SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/disable-sql-server-managed-backup-to-microsoft-azure.md)
- [系統資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)
- [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
  
  
